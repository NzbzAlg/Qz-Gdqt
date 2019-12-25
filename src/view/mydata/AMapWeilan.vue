<template>
  <div :class="{'amap-container':true,'amap-container-simple':simple}">
    <div class="amap-header" v-if="!simple">
      <input type="text" ref="mapSerchInput" />搜索：
      <span @click="clearMap">清除覆盖物</span>
    </div>
    <div class="amap-operation" v-if="!simple">
      <button @click="addWeilan">添加</button>
    </div>
    <div class="amap-search" ref="mapSearch" v-if="!simple" ></div>
    <div class="amap-weilan" ref="mapContainer"></div>
  </div>
</template>

<script>
import axios from "axios";
const key = "7b2709273be94bf7782a65c261b84863";

export default {
  props: {
    center: {
      type: Array || String,
      default: function() {
        return [116.46, 39.92];
      }
    },
    points: {
      type: Array,
      default: function() {
        return [];
      }
    },
    gid: String,
    simple: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      map: null,
      mouseTool: null,
      path: null,
      weilan: null,
      lbs: null // [{"lng":116.602295,"lat":39.882411},{"lng":116.56895,"lat":39.989518},{"lng":116.783968,"lat":39.966518},{"lng":116.795467,"lat":39.968287}]
    };
  },
  computed: {},
  mounted() {
    if (!this.simple) {
      this.initMap();
    }
  },
  methods: {
    initMap() {
      // 初始化地图
      this.map = new AMap.Map(this.$refs.mapContainer, {
        center: this.center,
        zoom: 8
      });
      console.log('map', this.map)
      if (!this.simple) {
        // 设置添加多边形
        this.mouseTool = new AMap.MouseTool(this.map);
        this.mouseTool.on("draw", event => {
          // event.obj 为绘制出来的覆盖物对象
          this.path = event.obj.getPath();
          const lbs = this.path.map(item => ({
            lng: item.lng,
            lat: item.lat
          }));
          this.lbs = JSON.stringify(lbs);
        });
        //   if (this.gid) {
        //     this.getWeianByGid();
        //   }
        // 设置搜索
        var autocomplete = new AMap.Autocomplete({
          input: this.$refs.mapSerchInput
        });
        var placeSearch = new AMap.PlaceSearch({
          pageSize: 5, // 单页显示结果条数
          pageIndex: 1, // 页码
          // city: "010", // 兴趣点城市
          // citylimit: true, //是否强制限制在设置的城市内搜索
          map: this.map, // 展现结果的地图实例
          panel: this.$refs.mapSearch, // 结果列表将在此容器中进行展示。
          autoFitView: true // 是否自动调整地图视野使绘制的 Marker点都处于视口的可见范围
        });
        AMap.event.addListener(autocomplete, "select", function(e) {
          //TODO 针对选中的poi实现自己的功能
          placeSearch.search(e.poi.name);
        });
      }
    },
    addWeilan() {
      this.mouseTool.polygon({
        strokeColor: "red",
        strokeOpacity: 1,
        strokeWeight: 2,
        strokeOpacity: 0,
        fillColor: "red",
        fillOpacity: 0.4,
        // 线样式还支持 'dashed'
        strokeStyle: "solid"
        // strokeStyle是dashed时有效
        // strokeDasharray: [30,10],
      });
    },
    saveWeilan() {
      if (this.path) {
        const points = this.path
          .map(item => `${item.lng},${item.lat}`)
          .join(";");
        const req = axios
          .post(`https://restapi.amap.com/v4/geofence/meta?key=${key}`, {
            name: "test1",
            repeat: "Mon,Tues,Wed,Thur,Fri,Sat,Sun",
            points: points
          })
          .then(res => {
            const data = res.data.data;
            if (data.status === "0") {
              // 添加成功
              console.log(data);
            } else {
              // 添加失败
              console.log(data);
            }
          });
      }
    },
    getWeianByGid() {
      axios
        .get(
          `https://restapi.amap.com/v4/geofence/meta?key=${key}&gid=${this.gid}`
        )
        .then(res => {
          const weilan = res.data.data.rs_list[0];
          const path = weilan.points.split(";").map(item => {
            const temp = item.split(",");
            return new AMap.LngLat(temp[0], temp[1]);
          });
          var polyline = new AMap.Polygon({
            path: path,
            borderWeight: 2,
            strokeColor: "red",
            lineJoin: "round",
            fillColor: "#FFFFFF",
            fillOpacity: 0.8
          });
          this.map.add(polyline);
        });
    },
    clearMap() {
      this.map.clearMap();
    },
    loadLbs(lbs) {
      if (!this.map) {
        this.initMap()
      }
      lbs = JSON.parse(lbs);
      console.log("lbs", lbs);
      if (!lbs || !Array.isArray(lbs) || lbs.length === 0) {
        return;
      }
      const path = lbs.map(item => {
        return new AMap.LngLat(item.lng, item.lat);
      });
      var polygon = new AMap.Polygon({
        path: path,
        borderWeight: 2,
        strokeColor: "red",
        lineJoin: "round",
        fillColor: "#FFFFFF",
        fillOpacity: 0.8
      });
      this.map.clearMap();
      this.map.add(polygon);
      this.map.setCenter(polygon.getBounds().getCenter());
      // this.map.setZoom(8);
      // console.log(this.map)
      setTimeout(() => {
        this.map.setFitView([polygon]);
      }, 10)
    }
  }
};
</script>

<style>
.amap-container {
  height: 460px;
  position: relative;
}
.amap-weilan {
  position: relative;
  height: 100%;
  z-index: 0;
}
.amap-operation {
  position: absolute;
  top: 0;
  right: 0;
   z-index: 1;
}
.amap-header {
  width: 300px;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
}
.amap-search{
  width: 300px;
  position: absolute;
  top: 30px;
  left: 0;
  z-index: 1;
}
</style>
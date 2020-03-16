<template>
  <div class="exhibition">
    <p class="headline">
      <b>2020年度教育展专业观众数据</b>
    </p>
    <p class="presell">
      <b>火爆预售中</b>
    </p>
    <div class="content_exibiton">
      <div class="twoZero">
        <div class="year_left">
          <p style="padding: 0 0 ;margin-top:15px">
            <span style="font-size:30px;font-weight:bold;color:rgba(60,115,220,1);">2020</span>
            <span style="font-size:20px;font-weight:bold;color:rgba(60,115,220,1);">年度</span>
          </p>
          <p style="font-size:20px;font-weight:bold;color:rgba(60,115,220,1);padding:0 0;">教育数据</p>
        </div>
        <div class="year_right">
          <div class="examine">
            <p
              style="font-size:18px;font-weight:bold;color:rgba(255,255,255,1);"
              @click="twoZeroYear"
            >
              点击查看
              <i class="el-icon-right"></i>
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="content_center">
      <div class="center_data">
        <el-card shadow="always">
          <p class="data_sizt">全部任务</p>
          <p class="data_num">{{num}}</p>
          <el-progress :percentage="num5" :format="format" style="margin:0px"></el-progress>
        </el-card>
      </div>
      <div class="center_data">
        <el-card shadow="always">
          <p class="data_sizt">已构建</p>
          <p class="data_num" style="color:rgba(76,205,152,1);">{{num1}}</p>
          <el-progress :percentage="num6" :format="format" style="margin:0px;" class="build"></el-progress>
        </el-card>
      </div>
      <div class="center_data">
        <el-card shadow="always">
          <p class="data_sizt">待构建</p>
          <p class="data_num" style="color:rgba(255,142,74,1);">{{num2}}</p>
          <el-progress :percentage="num7" :format="format" style="margin:0px" class="be_built"></el-progress>
        </el-card>
      </div>
      <div class="center_data">
        <el-card shadow="always">
          <p class="data_sizt">数据总量</p>
          <p class="data_num" style="color:rgba(134,97,235,1);">{{num3}}</p>
          <el-progress :percentage="num8" :format="format" style="margin:0px" class="Total_data"></el-progress>
        </el-card>
      </div>
      <div class="center_data" style="margin-right:0px">
        <el-card shadow="always">
          <p class="data_sizt">本月新增</p>
          <p class="data_num" style="color:rgba(191,83,246,1);">{{num4}}</p>
          <el-progress :percentage="num9" :format="format" style="margin:0px" class="montn_new"></el-progress>
        </el-card>
      </div>
    </div>
    <p
      style="padding:0 0;margin-top:45px;font-size:20px;font-family:Adobe Heiti Std;font-weight:bold;color:rgba(255,255,255,1);"
    >支持平台数据投放的主流移动端媒体</p>
    <p style="padding:0 0px;font-size:13px;color:rgba(255,255,255,1);">
      <span>新闻端：今日头条 腾讯新闻 网易新闻 手机百度</span>
      &nbsp;&nbsp;&nbsp;
      <span>社交端：微信朋友圈 抖音 新浪微博</span>
      &nbsp;&nbsp;&nbsp;
      <span>视频端：腾讯视频 优酷 爱奇艺</span>
    </p>
    <br>
    <div class="course">
      <p style="padding:4px;color:#6B67E5;font-size:14px">点击查看数据与媒体应用流程 >></p>
    </div>
    <!-- <div class="content_left" style="margin-top:50px;" @click="twoZeroYear">
          <img src="../../assets/img/2020.png" alt="" style="width:100%;height:100%;cursor: pointer;">
        </div>
        <div class="content_middle" style="margin-top:50px;" @click="oneNineYear">
          <img src="../../assets/img/2019.png" alt="" style="width:100%;height:100%;cursor: pointer;">
    </div>-->
    <!-- <div class="content_right" style="margin-top:50px;" @click="oneEightYear">
          <img src="../../assets/img/2018.png" alt="" style="width:100%;height:100%;cursor: pointer;">
    </div>-->
  </div>
</template>
<script>
export default {
  data() {
    return {
      num: null,
      num1: null,
      num2: null,
      num3: null,
      num4: null,
      num5: 100,
      num6: 0,
      num7: 0,
      num8: 0,
      num9: 0,
    };
  },
  mounted(){
    this.getTask();
  },
  methods: {
    format(percentage) {
      return percentage === 100 ? "" : ``;
    },
    twoZeroYear() {
      this.$router.push("/index/educationTwoZero.vue");
    },
    oneNineYear() {
      this.$router.push("/index/oneNineYear.vue");
    },
    getTask() {
      this.$http.get("pc/task/countExhibitionTask",{params:{
        type:9
      }}).then(res => {
        var { code, data } = res;
        if (data.code === 1000) {
          this.num = data.data.All_NUM;
          this.num1 = data.data.FINISH_NUM;
            this.num2 = data.data.UNFINISH_NUM;
            this.num3 = data.data.DATA_NUM;
            this.num4 = data.data.MONTH_NUM;
          if (this.num1 / this.num5 === 0) {
            this.num6 = 0;
          } else if (this.num1 === this.num) {
            this.num6 = 100;
          } else {
            this.num6 = (this.num1 / this.num5) * 100;
          }
          if (this.num2 / this.num5 === 0) {
            this.num7 = 0;
          } else if (this.num2 === this.num) {
            this.num7 = 100;
          } else {
            this.num7 = (this.num2 / this.num5) * 100;
          }
          if (this.num3 / this.num5 === 0) {
            this.num8 = 0;
          } else if (this.num3 === this.num) {
            this.num8 = 100;
          } else {
            this.num8 = (this.num3 / this.num5) * 100;
          }
          if (this.num4 / this.num5 === 0) {
            this.num9 = 0;
          } else if (this.num3 === this.num) {
            this.num9 = 100;
          } else {
            this.num9 = (this.num4 / this.num5) * 100;
          }
        } else if (code == 2001) {
          this.$message.error(res.data.message);
          window.sessionStorage.clear();
          window.localStorage.clear();
          this.$router.push("/");
        } else {
          this.$message.error(res.data.message);
        }
      });
    }
  }
};
</script>
<style lang='scss'>
.build .el-progress-bar__inner {
  background-color: #4ccd98;
}
.be_built .el-progress-bar__inner {
  background-color: #ff8e4a;
}
.Total_data .el-progress-bar__inner {
  background-color: #8661eb;
}
.montn_new .el-progress-bar__inner {
  background-color: #bf53f6;
}
.el-card__body {
  padding: 4px!important;
  height: 60px;
}
.el-card {
  height: 60px;
}
.el-progress-bar {
  padding-right: 50px;
  width: 100%;
  margin-right: 0px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
.exhibition {
  width: 100%;
  background: url(../../assets/img/背景.png) no-repeat;
  background-size: 100% 100%;
  min-height: 100%;
  // margin-top: 105px;
}
.exhibition .headline {
  padding-top: 80px;
  // font-size: 62px;
  // font-weight: bold;
  // color: rgba(255, 254, 254, 1);
  line-height: 98px;
  padding-bottom: 0px;
}
.headline b {
  color: #fffeff;
  font-size: 52px;
  display: block;
  text-transform: uppercase;
  text-shadow: 0px 5px 0px #1700eb;
  font-family: "Microsoft YaHei UI";
}
.exhibition .presell {
  font-size: 80px;
  font-family: MF BanHei (Noncommercial);
  font-weight: 400;
  color: rgba(255, 222, 36, 1);
  line-height: 88px;
  padding: 0 0;
}
.presell b {
  color: #ffde24;
  font-size: 72px;
  display: block;
  text-transform: uppercase;
  text-shadow: 0px 5px 0px #1700eb;
  font-family: MF BanHei;
}
.content_exibiton {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 30px;
}
.content_exibiton .twoZero {
  width: 400px;
  height: 95px;
  background: rgba(255, 255, 255, 1);
  border-radius: 8px;
  margin-right: 10px;
  color: #3c73dc;
}
.year_left {
  width: 175px;
  height: 100%;
  float: left;
}
.year_right {
  width: 175px;
  height: 100%;
  float: right;
}
.examine {
  width: 135px;
  height: 40px;
  background: rgba(60, 115, 220, 1);
  border-radius: 8px;
  margin-top: 35px;
  cursor: pointer;
}
.examines {
  width: 135px;
  height: 40px;
  background: #d04ffa;
  border-radius: 8px;
  margin-top: 35px;
  cursor: pointer;
}

.content_exibiton .oneNine {
  width: 400px;
  height: 95px;
  background: rgba(255, 255, 255, 1);
  border-radius: 8px;
}
.content_center {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 15px;
}
.content_center .center_data {
  width: 150px;
  height: 60px;
  background: rgba(255, 255, 255, 1);
  border-radius: 8px;
  margin-right: 15px;
}
.data_sizt {
  font-size: 14px;
  color: #3b4859;
  letter-spacing: 0;
  line-height: 24px;
  float: left;
  display: inline-block;
}
.data_num {
  text-align: left;
  font-size: 25px;
  letter-spacing: 0;
  line-height: 24px;
  float: right;
  color: #0088ff;
}
.course {
  width: 360px;
  height: 30px;
  background: rgba(255, 255, 255, 1);
  border-radius: 20px;
  margin:auto ;
  // margin-top: 20px;
  cursor: pointer;
}
</style>
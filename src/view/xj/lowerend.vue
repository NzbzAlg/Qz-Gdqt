<template>
  <div>
    <div :class="$style.f_table">
      <p>下级终端设备</p>
      <div :class="$style.f_row">
        <div :span="1" :class="{'f_fy':xz,'f_fy1':xz1}" @click="qb">全部</div>
        <div :span="1" :class="{'f_fy':xz2,'f_fy1':xz3}" @click="ywc">上传中</div>
        <div :span="1" :class="{'f_fy':xz4,'f_fy1':xz5}" @click="wwc">待采集</div>
        <div :span="1" :class="{'f_fy':xz6,'f_fy1':xz7}" @click="zzrw">已联网</div>
      </div>
      <!-- 表格内容 -->
      <!-- 全部 -->
      <div v-show="xz1===true">
        <div :class="$style.f_bgnr">
          <el-table :data="alltableData" border style="width: 100%">
            <el-table-column type="index" align="center" label="序号" width="50"></el-table-column>
            <el-table-column sortable align="center" label="终端编号" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.code}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="分组" width="180">
              <template slot-scope="scope">
                <span v-if="scope.row.groupName!=''">{{scope.row.groupName}}</span>
                <span v-if="scope.row.groupName===''">未分组</span>
              </template>
            </el-table-column>
            <el-table-column sortable align="center" label="客户名称" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.miName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" sortable label="采集状态">
              <template slot-scope="scope">
                <span v-if="scope.row.status===1">上传中</span>
                <span v-if="scope.row.status===2">未启动</span>
              </template>
            </el-table-column>
            <el-table-column prop="isNet" align="center" sortable label="联网状态">
              <template slot-scope="scope">
                <span v-if="scope.row.isNet===1">在线</span>
                <span v-if="scope.row.isNet===2">离线</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="采集任务">
              <template slot-scope="scope">
                <span
                  @click="sjxq(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.taskName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="固定画像">
              <template slot-scope="scope">
                <span
                  @click="sjxq2(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.fixedName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="位置信息">
              <template slot-scope="scope">
                <span
                  @click="place(scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.formatted_address}}</span>
              </template>
            </el-table-column>
            <el-table-column prop="status" align="center" label="操作">
              <template slot-scope="scope">
                <span
                  @click="open(scope.$index, scope.row)"
                  style="font-size: 14px; cursor: pointer; color: #9013FE; letter-spacing: 0; text-align: center;"
                >解绑</span>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <!-- 上传中 -->
      <div v-show="xz3===true">
        <div :class="$style.f_bgnr">
          <el-table :data="alltableData" border style="width: 100%">
            <el-table-column type="index" align="center" label="序号" width="50"></el-table-column>
            <el-table-column sortable align="center" label="终端编号" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.code}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="分组" width="180">
              <template slot-scope="scope">
                <span v-if="scope.row.groupName!=''">{{scope.row.groupName}}</span>
                <span v-if="scope.row.groupName===''">未分组</span>
              </template>
            </el-table-column>
            <el-table-column sortable align="center" label="客户名称" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.miName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" sortable label="采集状态">
              <template slot-scope="scope">
                <span v-if="scope.row.status===1">上传中</span>
                <span v-if="scope.row.status===2">未启动</span>
              </template>
            </el-table-column>
            <el-table-column prop="isNet" align="center" sortable label="联网状态">
              <template slot-scope="scope">
                <span v-if="scope.row.isNet===1">在线</span>
                <span v-if="scope.row.isNet===2">离线</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="采集任务">
              <template slot-scope="scope">
                <span
                  @click="sjxq(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.taskName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="固定画像">
              <template slot-scope="scope">
                <span
                  @click="sjxq2(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.fixedName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="位置信息">
              <template slot-scope="scope">
                <span
                  @click="place(scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.formatted_address}}</span>
              </template>
            </el-table-column>
            <el-table-column prop="status" align="center" label="操作">
              <template slot-scope="scope">
                <span
                  @click="open(scope.$index, scope.row)"
                  style="font-size: 14px; cursor: pointer; color: #9013FE; letter-spacing: 0; text-align: center;"
                >解绑</span>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <!-- 待采集 -->
      <div v-show="xz5===true">
        <div :class="$style.f_bgnr">
          <el-table :data="alltableData" border style="width: 100%">
            <el-table-column type="index" align="center" label="序号" width="50"></el-table-column>
            <el-table-column sortable align="center" label="终端编号" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.code}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="分组" width="180">
              <template slot-scope="scope">
                <span v-if="scope.row.groupName!=''">{{scope.row.groupName}}</span>
                <span v-if="scope.row.groupName===''">未分组</span>
              </template>
            </el-table-column>
            <el-table-column sortable align="center" label="客户名称" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.miName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" sortable label="采集状态">
              <template slot-scope="scope">
                <span v-if="scope.row.status===1">上传中</span>
                <span v-if="scope.row.status===2">未启动</span>
              </template>
            </el-table-column>
            <el-table-column prop="isNet" align="center" sortable label="联网状态">
              <template slot-scope="scope">
                <span v-if="scope.row.isNet===1">在线</span>
                <span v-if="scope.row.isNet===2">离线</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="采集任务">
              <template slot-scope="scope">
                <span
                  @click="sjxq(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.taskName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="固定画像">
              <template slot-scope="scope">
                <span
                  @click="sjxq2(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.fixedName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="位置信息">
              <template slot-scope="scope">
                <span
                  @click="place(scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.formatted_address}}</span>
              </template>
            </el-table-column>
            <el-table-column prop="status" align="center" label="操作">
              <template slot-scope="scope">
                <span
                  @click="open(scope.$index, scope.row)"
                  style="font-size: 14px; cursor: pointer; color: #9013FE; letter-spacing: 0; text-align: center;"
                >解绑</span>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <!-- 已联网 -->
      <div v-show="xz7===true">
        <div :class="$style.f_bgnr">
          <el-table :data="alltableData" border style="width: 100%">
            <el-table-column type="index" align="center" label="序号" width="50"></el-table-column>
            <el-table-column sortable align="center" label="终端编号" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.code}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="分组" width="180">
              <template slot-scope="scope">
                <span v-if="scope.row.groupName!=''">{{scope.row.groupName}}</span>
                <span v-if="scope.row.groupName===''">未分组</span>
              </template>
            </el-table-column>
            <el-table-column sortable align="center" label="客户名称" width="180">
              <template slot-scope="scope">
                <span>{{scope.row.miName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" sortable label="采集状态">
              <template slot-scope="scope">
                <span v-if="scope.row.status===1">上传中</span>
                <span v-if="scope.row.status===2">未启动</span>
              </template>
            </el-table-column>
            <el-table-column prop="isNet" align="center" sortable label="联网状态">
              <template slot-scope="scope">
                <span v-if="scope.row.isNet===1">在线</span>
                <span v-if="scope.row.isNet===2">离线</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="采集任务">
              <template slot-scope="scope">
                <span
                  @click="sjxq(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.taskName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="固定画像">
              <template slot-scope="scope">
                <span
                  @click="sjxq2(scope.$index, scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.fixedName}}</span>
              </template>
            </el-table-column>
            <el-table-column align="center" label="位置信息">
              <template slot-scope="scope">
                <span
                  @click="place(scope.row)"
                  :class="$style.f_ycsj"
                >{{scope.row.formatted_address}}</span>
              </template>
            </el-table-column>
            <el-table-column prop="status" align="center" label="操作">
              <template slot-scope="scope">
                <span
                  @click="open(scope.$index, scope.row)"
                  style="font-size: 14px; cursor: pointer; color: #9013FE; letter-spacing: 0; text-align: center;"
                >解绑</span>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <!-- 分页 -->
      <div style="text-align: right;margin-top:20px;padding-bottom: 20px;padding-right:10px;">
        <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :current-page.sync="currentPage4"
          :page-sizes="[10, 20, 30, 40]"
          :page-size="100"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total"
        ></el-pagination>
      </div>
      <el-dialog
        title="位置信息"
        :visible.sync="map"
        width="60%"
        class="f_zbxx"
        :before-close="handleClose1"
      >
        <gaode :row="item" />
      </el-dialog>
    </div>
    <div :class="$style.f_jz">
      <footerl />
    </div>
  </div>
</template>

<script>
import footerl from "../footer/footerl";
import gaode from "../map/gaode";
export default {
  components: {
    footerl,
    gaode
  },
  data() {
    return {
      item: {},
      map: false,
      textarea2: "",
      num: 2000,
      num1: 500,
      num2: 500,
      num3: 500,
      num4: 500,
      num5: 100,
      num6: 0,
      num7: 0,
      input: "",
      value1: "",
      xz: false,
      xz1: true,
      xz2: true,
      xz3: false,
      xz4: true,
      xz5: false,
      xz6: true,
      xz7: false,
      xz8: true,
      xz9: false,
      tableData: [],
      tableData1: [],
      alltableData: [],
      currentPage4: 1,
      sjxq1: false,
      value3: [],
      value2: [],
      options: [],
      age: "",
      nl: "",
      zy: "",
      gzdd: "",
      pt: "",
      ikon: false,
      input1: "",
      jzdd: "",
      ysjl: 1000,
      moeny: "1000VKT",
      textarea2: "",
      dgdata: false,
      dgmoney: null,
      btname: "任务详情",
      btmatter: "数据回购任务",
      bangding: false,
      jiebang: false,
      jbname: "",
      total: null,
      sizes: 10,
      formatted_address: "",
      Grouping: {},
      center: {},
      show: true,
      formatted_address: "",
      row: {},
      index: "",
      hackReset: true
    };
  },
  mounted() {
    this.qb();
  },
  methods: {
    handleClose1() {
      this.gaocenter = [0, 0];
      this.formatted_address = "";
      this.map = false;
    },

    getdata(item) {
      let that = this;
      that.center = [0, 0]; //初始化时候的赋值
      return new Promise(function(resolve, reject) {
        if (item.lng) {
          let locations = item.lng + "," + item.lat;
          that
            .$jsonp(
              "https://restapi.amap.com/v3/assistant/coordinate/convert?locations=" +
                item.lng +
                "," +
                item.lat +
                "&coordsys=gps&output=json&key=7b2709273be94bf7782a65c261b84863"
            )
            .then(function(res) {
              // console.log(res)
              locations = res.locations;
              item.lng = locations.split(",")[0];
              item.lat = locations.split(",")[1];
              that.center = [item.lng, item.lat];
              that
                .$jsonp(
                  "https://restapi.amap.com/v3/geocode/regeo?output=json&location=" +
                    locations +
                    "&key=7b2709273be94bf7782a65c261b84863&radius=1000&extensions=all"
                )
                .then(function(res) {
                  // console.log(res);
                  let d = res.regeocode;
                  that.address = "";
                  // console.log(d.formatted_address);
                  if (d) {
                    that.address = d.formatted_address; //点击选择新地址并获取地址的名称
                  }
                  resolve({
                    lng: item.lng,
                    lat: item.lat,
                    formatted_address: that.address
                  });
                })
                .catch(function(error) {
                  console.log(error);
                });
            })
            .catch(function(error) {
              console.log(error);
            });
        } else {
          console.log("error");
        }
      });
    },
    async generateData(item) {
      let that = this;
      let _result = await that.getdata(item);
      return _result;
    },
    qb() {
      let that = this;
      this.xz1 = true;
      this.xz = false;
      this.xz2 = true;
      this.xz3 = false;
      this.xz4 = true;
      this.xz5 = false;
      this.xz6 = true;
      this.xz7 = false;
      this.xz8 = true;
      this.xz9 = false;
      this.currentPage4 = 1;
      this.$http
        .get(`pc/device/list`, {
          params: {
            size: this.sizes,
            type: 0
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.alltableData = [];
            this.total = data.total;
            data.content.forEach(item => {
              if (item.lng) {
                that.generateData(item).then(function(result) {
                  // console.log(result);
                  item.formatted_address = result.formatted_address;
                  item.lng = result.lng;
                  item.lat = result.lat;
                  // console.log(item.formatted_address)
                  that.alltableData.push(item);
                });
              } else {
                that.alltableData.push(item);
              }
            });
          } else if (code == 2001) {
            this.$message.error(res.data.message);
            window.sessionStorage.clear();
            window.localStorage.clear();
            this.$router.push("/");
          } else {
            this.$message.error(res.data.message);
          }
        })
        .catch(err => {
          console.log("错误信息" + err);
        });
    },
    // 上传中
    ywc() {
      let that = this;
      this.xz1 = false;
      this.xz = true;
      this.xz2 = false;
      this.xz3 = true;
      this.xz4 = true;
      this.xz5 = false;
      this.xz6 = true;
      this.xz7 = false;
      this.xz8 = true;
      this.xz9 = false;
      this.currentPage4 = 1;
      this.$http
        .get(`pc/device/list`, {
          params: {
            size: this.sizes,
            type: 1
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.alltableData = [];
            this.total = data.total;
            data.content.forEach(item => {
              if (item.lng) {
                that.generateData(item).then(function(result) {
                  // console.log(result);
                  item.formatted_address = result.formatted_address;
                  item.lng = result.lng;
                  item.lat = result.lat;
                  // console.log(item.formatted_address)
                  that.alltableData.push(item);
                });
              } else {
                that.alltableData.push(item);
              }
            });
          } else if (code == 2001) {
            this.$message.error(res.data.message);
            window.sessionStorage.clear();
            window.localStorage.clear();
            this.$router.push("/");
          } else {
            this.$message.error(res.data.message);
          }
        })
        .catch(err => {
          console.log("错误信息" + err);
        });
    },
    // 待机中
    wwc() {
      let that = this;
      this.xz1 = false;
      this.xz = true;
      this.xz2 = true;
      this.xz3 = false;
      this.xz4 = false;
      this.xz5 = true;
      this.xz6 = true;
      this.xz7 = false;
      this.xz8 = true;
      this.xz9 = false;
      this.currentPage4 = 1;
      this.$http
        .get(`pc/device/list`, {
          params: {
            size: this.sizes,
            type: 2
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.alltableData = [];
            this.total = data.total;
            data.content.forEach(item => {
              if (item.lng) {
                that.generateData(item).then(function(result) {
                  // console.log(result);
                  item.formatted_address = result.formatted_address;
                  item.lng = result.lng;
                  item.lat = result.lat;
                  // console.log(item.formatted_address)
                  that.alltableData.push(item);
                });
              } else {
                that.alltableData.push(item);
              }
            });
          } else if (code == 2001) {
            this.$message.error(res.data.message);
            window.sessionStorage.clear();
            window.localStorage.clear();
            this.$router.push("/");
          } else {
            this.$message.error(res.data.message);
          }
        })
        .catch(err => {
          console.log("错误信息" + err);
        });
    },
    // 已联网
    zzrw() {
      let that = this;
      this.xz1 = false;
      this.xz = true;
      this.xz2 = true;
      this.xz3 = false;
      this.xz4 = true;
      this.xz5 = false;
      this.xz6 = false;
      this.xz7 = true;
      this.xz8 = true;
      this.xz9 = false;
      this.currentPage4 = 1;
      this.$http
        .get(`pc/device/list`, {
          params: {
            size: this.sizes,
            type: 3
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.alltableData = [];
            this.total = data.total;
            data.content.forEach(item => {
              if (item.lng) {
                that.generateData(item).then(function(result) {
                  // console.log(result);
                  item.formatted_address = result.formatted_address;
                  item.lng = result.lng;
                  item.lat = result.lat;
                  // console.log(item.formatted_address)
                  that.alltableData.push(item);
                });
              } else {
                that.alltableData.push(item);
              }
            });
          } else if (code == 2001) {
            this.$message.error(res.data.message);
            window.sessionStorage.clear();
            window.localStorage.clear();
            this.$router.push("/");
          } else {
            this.$message.error(res.data.message);
          }
        })
        .catch(err => {
          console.log("错误信息" + err);
        });
    },
    handleSizeChange(val) {
      let that = this;
      this.sizes = val;
      if (this.xz1 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: val,
              type: 0
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz3 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: val,
              type: 1
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz5 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: val,
              type: 2
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz7 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: val,
              type: 3
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      }
    },
    handleCurrentChange(val) {
      let that = this;
      this.pages = val;
      if (this.xz1 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: this.sizes,
              page: val - 1,
              type: 0
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz3 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: this.sizes,
              page: val - 1,
              type: 1
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz5 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: this.sizes,
              page: val - 1,
              type: 2
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      } else if (this.xz7 === true) {
        this.$http
          .get(`pc/device/list`, {
            params: {
              size: this.sizes,
              page: val - 1,
              type: 3
            }
          })
          .then(res => {
            var { code, data } = res.data;
            if (code === 1000) {
              this.alltableData = [];
              this.total = data.total;
              data.content.forEach(item => {
                if (item.lng) {
                  that.generateData(item).then(function(result) {
                    // console.log(result);
                    item.formatted_address = result.formatted_address;
                    item.lng = result.lng;
                    item.lat = result.lat;
                    // console.log(item.formatted_address)
                    that.alltableData.push(item);
                  });
                } else {
                  that.alltableData.push(item);
                }
              });
            } else if (code == 2001) {
              this.$message.error(res.data.message);
              window.sessionStorage.clear();
              window.localStorage.clear();
              this.$router.push("/");
            } else {
              this.$message.error(res.data.message);
            }
          })
          .catch(err => {
            console.log("错误信息" + err);
          });
      }
    },
    infoWindowClose() {
      this.show = false;
    },
    infoWindowOpen() {
      this.show = true;
    },
    gb() {
      this.hackReset = false;
      this.$nextTick(() => {
        this.hackReset = true;
      });
      this.center = {};
      this.ikon = false;
    },
    place(row) {
      console.log(row);
      if (row.lng == null || row.lng == "") {
        this.$message({
          message: "此设备暂时没有位置信息",
          type: "warning"
        });
      } else {
        this.item = row;
        this.map = true;
      }
      console.log("this.item", this.item);
    }
  }
};
</script>

<style lang='scss' module>
.f_table {
  background: #fff;
  margin-top: 35px;
  box-shadow: 0 2px 4px 0 #eff2f7;
  border-radius: 10px;
  text-align: left;
  p {
    padding: 30px 0;
    padding-left: 10px;
  }
  .f_row {
    padding-left: 20px;
  }
  .f_bgnr {
    padding-top: 39px;
    padding-left: 34px;
    padding-right: 34px;
  }
  .f_fy {
    float: right;
  }
}
.f_jz {
  margin-top: 20px;
  text-align: center;
}
.f_ycsj {
  cursor: pointer;
  color: #9013fe;
}
.f_tit {
  text-align: left;
}
.f_sjbg {
  margin-top: 20px;
}
.f_jb,
.f_sjxx {
  width: 100%;
  font-size: 16px;
  color: #1f2e4d;
  line-height: 14px;
  text-align: left;
  padding-bottom: 20px;
  border-bottom: 1px solid #e6e9f0;
}
.f_sjxx {
  margin-top: 30px;
}
.f_hxrow {
  margin-top: 20px;
  text-align: left;
  .f_ddname {
    font-size: 14px;
    color: #3d4966;
    line-height: 14px;
  }
  .f_hxinpt {
    width: calc(100% - 60%);
  }
  .f_hxinpt1 {
    width: calc(100% - 20%);
    padding-left: 1%;
  }
}
.f_chaxun {
  background: #d9b4fa;
  border: 1px solid #9013fe;
  border-radius: 4px;
  font-size: 14px;
  color: #5800a0;
  letter-spacing: 0;
}
.f_chaxun:hover {
  background: #9013fe;
  color: #fff;
  border: 1px solid #9013fe;
}
.f_inpt {
  width: calc(100% - 66%);
}
.f_btn {
  width: 80px;
  height: 36px;
  line-height: 36px;
  background: #d9b4fa;
  border: 1px solid #9013fe;
  color: #5800a0;
  border-radius: 4px;
  margin-right: 10px;
  text-align: center;
  font-size: 14px;
  letter-spacing: 0;
  cursor: pointer;
}
.f_btn:hover {
  background: #9013fe;
  color: #fff;
  border: 1px solid #9013fe;
}
.f_btn1 {
  width: 80px;
  background: #d9b4fa;
  border: 1px solid #9013fe;
  color: #5800a0;
  border-radius: 4px;
  margin-right: 10px;
  text-align: center;
  font-size: 14px;
  letter-spacing: 0;
  cursor: pointer;
}
.f_btn1:hover {
  background: #9013fe;
  color: #fff;
  border: 1px solid #9013fe;
}
.f_s5 {
  margin-right: 10px;
  width: calc(100% - 76%);
}
.f_point {
  cursor: pointer;
  color: #3b7cff;
}
.f_z {
  font-size: 12px;
  color: #3b4859;
  letter-spacing: 0;
  line-height: 24px;
  float: left;
}
.f_y,
.f_y1,
.f_y2 {
  font-size: 12px;
  letter-spacing: 0;
  line-height: 24px;
  float: right;
}
.f_y {
  color: #fb745b;
}
.f_y1 {
  color: #77c12b;
}
.f_y2 {
  color: #9013fe;
}
.f_zd,
.f_zd1,
.f_zd2 {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  display: inline-block;
  margin-right: -21%;
}
.f_zd {
  background: #fb745b;
}
.f_zd1 {
  background: #77c12b;
}
.f_zd2 {
  background: #9013fe;
}
.f_zx {
  font-size: 11px;
  color: #8a99ad;
  letter-spacing: 0;
  line-height: 24px;
  float: left;
}
.f_yl {
  padding-top: 0 !important;
  padding-bottom: 5px !important;
  font-size: 12px;
}
</style>
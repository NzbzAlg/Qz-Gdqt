<template>
  <el-dialog title="访客请注册" :visible.sync="compiles" width="30%" :before-close="handleClose">
    <el-form :label-position="labelPosition" label-width="100px">
      <el-row>
        <el-col :span="12">
          <el-form-item label="姓名:">
            <div>
              <el-input v-model="name" placeholder="请输入姓名" style="width:260px"></el-input>
            </div>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="12">
          <el-form-item label="公司名称:">
            <div>
              <el-input v-model="companyName" placeholder="请输入公司名称" style="width:260px"></el-input>
            </div>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="12">
          <el-form-item label="联系方式:">
            <div>
              <el-input v-model="phone" placeholder="请输入联系方式" style="width:260px"></el-input>
            </div>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="12">
          <el-form-item label="省：">
            <el-select
              v-model="province"
              @change="provinceevent"
              placeholder="请选择"
              style="width:260px"
            >
              <el-option
                v-for="item in Provinceoptions"
                :key="item.id"
                :label="item.name"
                :value="item.id"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col :span="12">
          <el-form-item label="市：">
            <el-select v-model="city" placeholder="请选择" style="width:260px">
              <el-option
                v-for="item in Cityoptions"
                :key="item.id"
                :label="item.name"
                :value="item.id"
              ></el-option>
            </el-select>
          </el-form-item>
        </el-col>
      </el-row>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="compiles = false">取 消</el-button>
      <el-button type="primary" @click="submit">提 交</el-button>
    </span>
  </el-dialog>
</template>

<script>
export default {
  data() {
    return {
      compiles: true,
      labelPosition: "right",
      name: "",
      companyName: "",
      phone: "",
      city: "",
      province: "",
      visitingTime: "",
      status: "",
      province: "",
      city: "",
      Provinceoptions: [],
      Cityoptions: [],
      setinterName:null,
    };
  },
  mounted() {
    this.stamp();
  },
  methods: {
    handleClose() {
      this.full = false;
      this.compiles = false;
    },

    submit() {
      this.compiles = false;
      let info = {
        name: this.name,
        companyName: this.companyName,
        phone: this.phone,
        province: this.province,
        city: this.city
      };
      this.$http
        .post(`pc/visitor/visitor`, info)
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.$message({
              dangerouslyUseHTMLString: true,
              duration: 3000,
              offset: 200,
              type: "success",
              showClose: true,
              message:
                "<p>平台已接受您的注册信息</p><p>客服人员稍后与您联系</p><p>请您耐心等待</p>"
            });
            // setTimeout(function () { 
            //   // alert("Hello"); 
            //   this.$router.push("/login");
            // }, 3000);
            this.setinterName = setInterval(() => {
              this.$router.push("/");
            }, 3000);
          } else {
            this.$message.error(res.data.message);
          }
        })
        .catch(err => {
          console.log("错误信息" + err);
        });
    },
    stamp() {
      this.$http
        .get(`modules/area/areaByPid`, {
          params: {
            pid: 1
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.Provinceoptions = data;
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

    provinceevent() {
      this.$http
        .get(`modules/area/areaByPid`, {
          params: {
            pid: this.province
          }
        })
        .then(res => {
          var { code, data } = res.data;
          if (code === 1000) {
            this.Cityoptions = data;
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
  beforeDestroy(){
    clearInterval(this.setinterName)
  },
};
</script>

<style>
p {
  text-align: center;
}
.el-message.is-closable .el-message__content {
  padding-left: 53px;
}
</style>
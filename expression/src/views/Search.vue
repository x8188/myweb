<!--
 * @Autor: Sakurag1_LSJ
 * @LastEditors: Sakurag1_LSJ
-->
<template>
  <div class="result">
    <!-- <div class="top wrap1">
      <div class="box box1">
        <h1 style="font-size: 30px">Statistics of Data Used in PlantDeepSEA</h1>
      </div>
    </div>
    <div class="contain" style="text-align: center">
      <a-row :gutter="24" style="font-size: 20px; font-weight: bold">
        <a-col :span="5">ID</a-col>
        <a-col :span="4">Methyl_Type</a-col>
        <a-col :span="4">Methyl_Level</a-col>
        <a-col :span="4">SuppReads_Methyl</a-col>
        <a-col :span="6">SuppReads_ALL</a-col>
      </a-row>
      <a-row
        :gutter="24"
        style="font-size: 15px"
        v-for="item in DataList"
        :key="item.id"
      >
        <a-col :span="5">{{ item.name }}</a-col>
        <a-col :span="4">{{ item.name }}</a-col>
        <a-col :span="4">{{ item.name }}</a-col>
        <a-col :span="4">{{ item.name }}</a-col>
        <a-col :span="6">{{ item.description }}</a-col>
      </a-row>
    </div>
    <div class="top">
      <h1 style="font-size: 30px">Statistics of Result</h1>
    </div>
    <div class="contain">
      <h3 style="margin-top: 20px; margin-left: 10px">
        We counted the experimental data
      </h3>
      <div style="text-align: center">
        <img src="../img/statistic.png" style="width: 40%" />
        <img src="../img/statistic.png" style="width: 40%" />
        <img src="../img/statistic.png" style="width: 40%" />
        <img src="../img/statistic.png" style="width: 40%" />
      </div>
    </div>
    <div class="top">
      <h1 style="font-size: 30px">Evaluations of Models</h1>
    </div>
    <div class="contain">
      <h3 style="margin-top: 20px; margin-left: 10px">We get ROC curve</h3>
      <div style="text-align: center">
        <img src="../img/roc.png" style="width: 65%" />
      </div>
    </div> -->
    <Steps :steps1="3" :steps2="steps2"></Steps>
 
    <h1 style="color:#1D58B3; font-size: 30px;">Result retrieval</h1>
    <el-divider></el-divider>
    <p style=" font-size: 20px;">NOTE: The result files will be kept for 30 days on our server. Please download and save your files on time.</p>
    <div style="text-align: center">
      <el-input placeholder="Input job identifier here" style="width: 50%; margin: 20px 0px;">
        <el-button slot="append" icon="el-icon-search"></el-button>
      </el-input>
      <p style="color:#1D58B3; font-size: 20px;text-align: left">Job queue monitor (update in 10 seconds):</p>

      <el-table :data="DataList">
        <el-table-column prop="key" label="?????????" width="150">
        </el-table-column>
        <el-table-column prop="name" label="?????????"> </el-table-column>
        <el-table-column label="????????????">
          <template slot-scope="{ row }">
            <div id="status">
              <i class="el-icon-success" style="color:#0DBC79" v-show="row.status == 'success'"></i>
              <i class="el-icon-error" style="color:#D32F2F"  v-show="row.status == 'error'"></i>
              <i class="el-icon-loading"  v-show="row.status == 'wait'"></i>
            </div>
          </template>
        </el-table-column>
        <el-table-column prop="time" label="????????????"> </el-table-column>
        <el-table-column label="??????" width="300">
          <template slot-scope="{ row }">
            <el-button
              type="primary"
              icon="el-icon-edit"
              size="mini"
              @click="visTask(row)"
              style="margin: 0px 10px"
              >????????????</el-button
            >
            <el-popconfirm title="??????????????????" @onConfirm="deleteTask(row)">
              <el-button
                type="danger"
                icon="el-icon-delete"
                size="mini"
                slot="reference"
              ></el-button>
            </el-popconfirm>
          </template>
        </el-table-column>
      </el-table>
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="getPageList"
        :current-page="page"
        :page-sizes="[5, 10, 50, 100]"
        :page-size="limit"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
      >
      </el-pagination>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

// require??????????????????????????????????????????????????????????????????????????????
const data = [
  {
    key: 1,
    name: "John Brown",
    age: 32,
    status: "success",
    time: "2022-11-30",
  },
  {
    key: 2,
    name: "John Brown",
    age: 32,
    status: "wait",
    time: "2022-11-30",
  },
  {
    key: 3,
    name: "John Brown",
    age: 32,
    status: "success",
    time: "2022-11-30",
  },
  {
    key: 4,
    name: "John Brown",
    age: 32,
    status: "error",
    time: "2022-11-30",
  },
  {
    key: 5,
    name: "John Brown",
    age: 32,
    status: "success",
    time: "2022-11-30",
  },
  {
    key: 6,
    name: "John Brown",
    age: 32,
    status: "success",
    time: "2022-11-30",
  },
];

export default {
  name: "Result",
  components: {},
  data() {
    return {
      page: 1,
      limit: 5,
      total: data.length,

      DataList: data,
      isShowImg: false,

      visid: undefined,
      img_chg: "",
      img_seq: "",
      steps2:0
    };
  },
  methods: {
    deleteTask(row) {
      // ?????????????????????????????????????????????
    },
    visTask(row) {
      if (row.status != "success") {
        this.$alert("This mission has not been successful", "ERROR!", {
          confirmButtonText: "confrim",
          type: "error",
        });
        return;
      } else {
        // this.visid = row.key;
        // this.img_chg = row.imgurl.chg;
        // this.img_seq = row.imgurl.seq;
        this.$router.push({
          path:`/show/${row.key}`,
        })
        return;
      }
    },
    getPageList(pager = 1) {
      this.page = pager;
      // ????????????????????????????????????page limit
      // ????????????????????????????????????????????????????????????
    },
    handleSizeChange(limit) {
      this.limit = limit;
      this.getPageList();
    },
  },
  created() {},
};
</script>
<style scoped>
/* .result {
  height: 2000px;
  width: 80%;
  margin: 0 auto;
}
.top {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 15px;
  margin: 0 auto;
  height: 75px;
  margin-top: 50px;
  background-color: #f0f8ff;
}
.contain {
  border-style: solid;
  border-color: #f5f5f5;
} */
.result {
  width: 80%;
  margin: 0 auto;
}

#status i{
  font-size: 25px;
}
</style>
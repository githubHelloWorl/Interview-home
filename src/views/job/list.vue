<template>
  <div class="page_notice" id="notice_list">
    <div class="warp">
      <div class="container">
        <el-row :gutter="4">
          <el-col :span="8">
            <el-button type="textarea" @click="dialogFormVisible = true">发表看法</el-button>
          </el-col>
          <el-col :span="8">
            <el-input
                placeholder="请输入内容"
                prefix-icon="el-icon-search"
                v-model="content">
            </el-input>
            <el-button @click="handleRetrieval">确认</el-button>
          </el-col>
        </el-row>

        <el-dialog title="面试经验分享" :visible.sync="dialogFormVisible">
          <el-form :model="form" label-position="left">
            <el-form-item label="标题" :label-width="formLabelWidth">
              <el-input v-model="form.title" autocomplete="off" style="width: 240px;"></el-input>
            </el-form-item>
            <el-form-item label="公司" :label-width="formLabelWidth">
              <el-input v-model="form.company" autocomplete="off" style="width: 240px;"></el-input>
            </el-form-item>
            <el-form-item label="职位" :label-width="formLabelWidth">
              <el-input v-model="form.position" autocomplete="off" style="width: 240px;"></el-input>
            </el-form-item>
            <el-form-item label="内容" :label-width="formLabelWidth">
              <el-input type="textarea" v-model="form.content" :rows="3" autocomplete="off"
                        style="width: 240px;"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button @click="submit">提交</el-button>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">取 消</el-button>
            <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
          </div>
        </el-dialog>

        <div class="row">
          <div class="col-12">
            <div class="car_notice">
              <div class="notice_list">
                <div class="notice_list_title">
                  <span class="title">{{ "面试经验分享" }}</span>
                </div>

                <el-card class="box-card" v-for="li of tempList">
                  <!--                                    <div slot="header" class="clearfix">-->
                  <span style="font-weight: bold; font-size: 24px;">{{ li.title }}</span>
                  <br/>
                  {{ li.createBy }}
                  &nbsp;&nbsp;&nbsp;&nbsp;
                  <span style="color: lightgray;">面试了职位: {{ li.position }}</span>
                  &nbsp;&nbsp;&nbsp;&nbsp;
                  <!--                  <span><el-tag :type="li.status[1]">{{ li.status[0] }}</el-tag></span>-->
                  <p style="font-size: 12px;color: lightgray;">{{ li.createTime | formatDate }}</p>
                  <!--                    <el-button style="float: right; padding: 3px 0" type="text">操作按钮</el-button>-->
                  <!--                  </div>-->
                  <!--                  <div>-->
                  <div>
                    <p class="cLine" v-for="l of handleLine(li.content)">
                      &nbsp;&nbsp;&nbsp;&nbsp;
                      {{ l }}
                    </p>
                  </div>
                  <!--                  </div>-->
                </el-card>
              </div>
            </div>
          </div>
        </div>
        <div class="row">
          <!-- 分页器 -->
          <div class="col overflow-auto flex_cc">
            <b-pagination
                v-model="query.page"
                :total-rows="count"
                :per-page="query.size"
                @change="goToPage"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import mixin from "@/mixins/page.js";
import user from "@/store/user";

export default {
  mixins: [mixin],
  data() {
    return {
      url_get_obj: "~/api/user/get_obj?",
      // 全部的数据
      listAll: [],
      // 全部数据的列数
      count: 0,
      // 检索的内容
      content: '',
      obj: {},
      tempList: [],
      query: {
        title: "",
        page: 1,
        size: 3,
        user_id: this.$store.state.user.user_id,
      },
      // 限制字符数
      limitNum: 10,
      // 页面数
      count_pages: 1,
      // 发表主题的flag
      dialogFormVisible: false,
      // 宽度
      formLabelWidth: "500",
      // 输入的数据
      form: {
        userId: '',
        title: '',
        createBy: '',
        position: '',
        content: '',
        company: '',
      },
    };
  },
  methods: {
    /**
     * 获取公告后
     * @param {Object} json 响应对象
     */
    get_list_after(json) {
      this.count_pages = Math.ceil(json.result.count / this.query.size);
    },
    goToPage(v) {
      this.query.page = v;
      this.goToNew()
    },
    /**
     * 处理页码
     */
    goToNew() {
      console.log("页码")
      console.log(this.listAll);
      this.tempList.splice(0);
      let start = (this.query.page - 1) * 3;
      let end = start + 3;
      this.tempList.push(...this.listAll.slice(start, end))
    },
    /**
     * 给过滤数据 => listAll
     * @param liData
     */
    handleFilterData(liData) {
      this.listAll.splice(0);
      liData.forEach((i) => {
        let form = {
          content: i.attachment.content,
          company: i.company,
          createBy: i.createBy,
          id: i.id,
          position: i.position,
          title: i.title,
          createTime: i.createTime,
        };
        this.listAll.push(form);
      })
    },
    /**
     * 得到所有的数据
     */
    handleGetFileAll() {
      this.$get("~/api/ES/getFileAll?", {}, (res) => {
        console.log(res.data);
        this.count = res.data.length;
        this.handleFilterData(res.data);
        this.goToNew();
      });
    },
    /**
     * 检索关键字
     */
    handleRetrieval() {
      this.$get("~/api/ES/getFile?content=" + this.content, {}, (res) => {
        console.log(res.data);
        this.count = res.data.length;
        this.handleFilterData(res.data);
        this.goToNew();
      });
    },
    // 处理换行
    handleLine(str) {
      var li = str.split("\n")
      return li;
    },
    // 提交用户发表主题信息
    submit() {
      var form = this.form;
      form.userId = this.obj.user_id;
      form.createBy = this.obj.nickname;
      console.log(form)
      this.$post("~/api/ES/insertFile?", form, (res) => {
        if (res) {
          console.log(res);
          this.$message.success("成功！");
          this.handleGetFileAll();
        } else if (res.error) {
          console.log(res.error);
          this.$message.error(res.error.message);
        }
      });
    }
  },
  created() {
    this.handleGetFileAll();
    // this.goToNew();
  },
  filters: {
    /**
     * @description 日期时间转换
     * @param {String} date 时间戳
     */
    formatDate(date) {
      var date = new Date(date);
      var YY = date.getFullYear() + '-';
      var MM = (date.getMonth() + 1 < 10 ? '0' + (date.getMonth() + 1) : date.getMonth() + 1) + '-';
      var DD = (date.getDate() < 10 ? '0' + (date.getDate()) : date.getDate());
      var hh = (date.getHours() < 10 ? '0' + date.getHours() : date.getHours()) + ':';
      var mm = (date.getMinutes() < 10 ? '0' + date.getMinutes() : date.getMinutes()) + ':';
      var ss = (date.getSeconds() < 10 ? '0' + date.getSeconds() : date.getSeconds());
      return YY + MM + DD + " " + hh + mm + ss;
    },
  },
  // computed: {
  //   count() {
  //     return this.listAll.length;
  //   }
  // }
};
</script>

<style scoped>
.flex_cc {
  display: flex;
  justify-content: center;
  align-items: center;
}

.ellipsis_2 {
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.container {
  min-height: 800px;
  margin: auto;
  width: 60%;
}

.box-card {
  margin-bottom: 10px;
  border-radius: 20px;
}

.cLine {
  line-height: 1.1;
}

.notice_block {
  display: flex;
  justify-content: space-between;
  padding: 10px;
  margin: 5px;
}

.notice_title {
  text-overflow: ellipsis;
  white-space: nowrap;
}

.notice_list_title {
  margin: 0 0.5rem;
  background-color: #d2d2d2;
  color: white;
  display: flex;
  height: 4rem;
  align-items: center;
  justify-content: space-between;
  border-radius: 0.5rem;
}

.title {
  font-size: 1.5rem;
  font-weight: bold;
  padding-left: 1rem;
}
</style>

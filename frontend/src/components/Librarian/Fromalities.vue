<template>
  <div>
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item>图书管理员首页</el-breadcrumb-item>
      <el-breadcrumb-item>办理借还手续</el-breadcrumb-item>
    </el-breadcrumb>

    <el-card class="searchbook-card" shadow="hover">
      <el-row :gutter="20">
        <el-col :span="20">
          <el-input placeholder="请输入 图书名 / 作者 / 出版社 / ISBN ">
          </el-input>
        </el-col>
        <el-col :span="4">
          <el-button type="primary">搜索书籍</el-button>
        </el-col>
      </el-row>
      <el-divider></el-divider>
      <el-table stripe max-height="500" :data="booklist">
        <el-table-column label="#" type="index"></el-table-column>
        <el-table-column label="图书名" prop="bookname"></el-table-column>
        <el-table-column label="作者" prop="author"></el-table-column>
        <el-table-column label="出版社" prop="publisher"></el-table-column>
        <el-table-column label="ISBN" prop="isbn"></el-table-column>
        <el-table-column label="状态">
          <template slot-scope="scope">
            <el-tag :type="judgeType(scope.row.status)" effect="dark">{{scope.row.status}}</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="操作" fixed="right">
          <template slot-scope="scope">
            <el-button-group>
              <el-button type="primary" :disabled="judgeButtonDisabled1(scope.row.status)">借出</el-button>
              <el-button type="primary" :disabled="judgeButtonDisabled2(scope.row.status)">归还</el-button>
            </el-button-group>
          </template>
        </el-table-column>
      </el-table>

      <el-pagination
        layout="total, prev, pager, next, jumper"
        @current-change="handleCurrentChange"
        :current-page="pagenum"
        :total="total"
        page-size="5"
      ></el-pagination>
    </el-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      booklist: [],
      pagenum: 1,
      total: 0
    };
  },
  created() {
    this.getBookList();
  },
  methods: {
    getBookList() {
      // 修改这里以从后端调取信息
      if (this.pagenum == 1) {
        this.booklist = [
          {
            bookname: "大雪中的山庄",
            author: "东野圭吾",
            publisher: "北京十月文艺出版社",
            isbn: "9787530216835",
            status: "在馆"
          },
          {
            bookname: "三生三世 十里桃花",
            author: "唐七公子",
            publisher: "沈阳出版社",
            isbn: "9787544138000",
            status: "在馆"
          },
          {
            bookname: "何以笙箫默",
            author: "顾漫",
            publisher: "朝华出版社",
            isbn: "9787505414709",
            status: "遗失"
          },
          {
            bookname: "人类简史",
            author: "[以色列] 尤瓦尔·赫拉利",
            publisher: "中信出版社",
            isbn: "9787508647357",
            status: "在馆"
          },
          {
            bookname: "明朝那些事儿",
            author: "当年明月",
            publisher: "中国海关出版社",
            isbn: "9787801656087",
            status: "已借出"
          }
        ];
      }
      if (this.pagenum == 2) {
        this.booklist = [
          {
            bookname: "少有人走的路",
            author: "M·斯科特·派克",
            publisher: "吉林文史出版社",
            isbn: "9787807023777",
            status: "在馆"
          },
          {
            bookname: "追寻生命的意义",
            author: "[奥] 维克多·弗兰克",
            publisher: "新华出版社",
            isbn: "9787501162734",
            status: "在馆"
          },
          {
            bookname: "秘密花园",
            author: "乔汉娜·贝斯福",
            publisher: "北京联合出版公司",
            isbn: "9787550252585",
            status: "在馆"
          }
        ];
      }
      this.total = 8;
      this.$message.success("获取书籍列表成功");
    },
    judgeType(status) {
      if (status == "在馆") return "success";
      if (status == "遗失") return "danger";
      else return "info";
    },
    judgeButtonDisabled1(status) {
      if (status == "在馆") return false;
      if (status == "已借出") return true;
      return true;
    },
    judgeButtonDisabled2(status) {
      if (status == "在馆") return true;
      if (status == "已借出") return false;
      return true;
    },
    handleCurrentChange(newPage) {
      this.pagenum = newPage;
      this.getBookList();
    }
  }
};
</script>

<style scoped>
.el-breadcrumb {
  margin-bottom: 15px;
}
.searchbook-card {
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.15);
  /* width: 700px; */
  margin: 0 auto;
}
.el-pagination {
  margin-top: 15px;
}
</style>


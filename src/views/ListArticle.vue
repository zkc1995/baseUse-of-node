<template>
  <div>
    <el-table :data="articles">
      <el-table-column prop="title" label="文章标题" width="140">
      </el-table-column>
      <el-table-column prop="body" label="文章内容" width="120">
      </el-table-column>
      <el-table-column label="操作">
        <template slot-scope="scope">
          <el-button @click="edit(scope.row._id)" type="text" size="small">编辑</el-button>
          <el-button @click="remove(scope.row._id)" type="text" size="small">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
    data() {
      return {
        articles:[]
      }
    },
    methods:{
      fetchData(){
        this.$http.get("articles").then(res=>{
          this.articles = res.data;
        })
      },
      edit(id){
        // console.log(id);
        this.$router.push(`/articles/${id}/edit`)
      },
      remove(id){
        // eslint-disable-next-line
        this.$http.delete(`articles/${id}`).then(res => {
          this.$message({
            message:'文章删除成功',
            type:"success"
          });
          this.fetchData()
        })
      }
    },
    created(){
      this.fetchData()
    }
  };
</script>


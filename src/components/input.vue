<template>
  <el-autocomplete :minlength="2" v-model="searchName" :fetch-suggestions="querySearchAsync" placeholder="请输入内容"
                @select="handleSelect"></el-autocomplete>
</template>

<script>
export default {

  methods: {
     querySearchAsync(queryString, cb) {
                if (queryString && queryString.length > 2) {
                    let params = { name: queryString }
                    this.axios.get("/api/search/name", { params }).then(res => {
                        if (res.data.code == 200) {
                            cb(res.data.data);
                        }
                    })
                }
            },
            handleSelect(item) {
                console.log(this.searchName, item);
            }
  }

}
</script>

<style>
  .el-row {
    margin-bottom: 20px;
    &:last-child {
      margin-bottom: 0;
    }
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>

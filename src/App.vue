<template>
  <div id="app">
    <p>可自动滚动表格</p>
    <scrollTable
            class="scroll-table"
            :tableRef="'scrollTable'"
            :tableData="tableData"
            :intervalCallback="intervalCallback"
            :isAutoScroll="true"
            :intervalTime="5000"
            :isShowIndex="true"
            :isHighlight="true"
            :moveDistance="48"
            style="width: 100%; height: 495px; overflow-y: hidden">
      <el-table-column
              prop="date"
              label="日期"
              width="180">
      </el-table-column>
      <el-table-column
              prop="name"
              label="姓名"
              width="180">
      </el-table-column>
      <el-table-column
              prop="address"
              label="地址">
      </el-table-column>
    </scrollTable>
  </div>
</template>

<script>
import scrollTable from './components/scroll-table'
export default {
    name: 'app',
    data () {
      return {
          tableData: [{
              date: '2016-05-02',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1518 弄'
          }, {
              date: '2016-05-04',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1517 弄'
          }, {
              date: '2016-05-01',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1519 弄'
          }, {
              date: '2016-05-03',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1516 弄'
          }, {
              date: '2016-05-01',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1519 弄'
          }, {
              date: '2016-05-03',
              name: '王小虎',
              address: '上海市普陀区金沙江路 1516 弄'
          }]
      }
    },
    components: {
        scrollTable
    },
    methods: {
        intervalCallback () {
            // 每次滚动回调函数，如果有需要可以用
            // 比如涉及到分页的时候，可以在这里进行计算

        }
    }
}
</script>

<style type="text/css">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  .scroll-table {
    width: 1000px !important;
    margin: 0 auto;
  }
  /*滚动的较关键css代码 防止向上的行溢出*/
  .scroll-table .el-table__body-wrapper {
    /*自定义滚动*/
    position: relative;
    /*向上移动间隔时间和方向*/
    transition: top 0.825s;
    margin-top: 45px;
  }
  .scroll-table .el-table__header-wrapper {
    position: absolute;
    z-index: 999;
  }
  .highlight-bg {
    color: #000 !important;
    background: rgba(146, 204, 236, 0.6) !important
  }
</style>

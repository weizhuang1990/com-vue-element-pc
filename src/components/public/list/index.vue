<template>
  <div class="list">
    <el-table
      :data="model.data"
      style="width: 100%"
      :row-style="tableRowStyle"
      :header-cell-style="tableHeaderColor"
    >
      <el-table-column
        v-for="(value, index) in model.showlabal"
        :key="index"
        :label="value.name"
        :width="index === '__$__' ? 100 : ''"
      >
        <template slot-scope="scope">
          {{ value.type ? scope.row[index] : null }}
          <slot :name="index" :data="scope.row" :index="scope.$index" v-if="!value.type"></slot>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  props: {
    model: {
      type: Object,
      require: true,
    },
  },
}
</script>

<style scoped lang='scss'>
.list {
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 1.5rem;
  /deep/.el-table__body {
    width: 100% !important;
  }
  /deep/ .el-table__footer {
    width: 100% !important;
  }
  /deep/ .el-table__header {
    width: 100% !important;
  }
  /deep/.el-table td{
    text-align: center;
  }
}
</style>
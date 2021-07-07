<template>
  <div class="page" v-if="total">
    <el-pagination
      background
      @current-change="(val) => $emit('changePage', val)"
      :current-page="currentPage"
      layout="total, prev, pager, next, jumper"
      :total="total"
      :page-size="size"
    >
    </el-pagination>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      default: () => {
        return 0
      },
    },
    total: {
      type: Number,
      require: true,
    },
    size: {
      type: Number,
      default: () => {
        return 10
      },
    },
  },

  watch: {
    total(val) {
      if (val && Math.ceil(val / this.size) < this.currentPage) {
        this.$emit('changePage', Math.ceil(val / this.size))
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.page {
  padding-left: 1.5rem;
  padding-right: 1.5rem;
  padding-top: 1rem;
  display: flex;
  justify-content: flex-end;
  /deep/.el-pagination.is-background .el-pager li:not(.disabled).active {
    background: linear-gradient(180deg, #6b73ff 0%, #484eed 100%);
  }
  /deep/.el-pagination.is-background {
    color: #484eed;
  }
  padding-bottom: 1rem;
}
</style>
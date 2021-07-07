<template>
  <el-dialog
    v-if="isshow"
    :close-on-click-modal="clickModalClose"
    :title="title"
    :visible.sync="isshow"
    :append-to-body="true"
    :width="width"
    @close="$emit('closeEnd')"
  >
    <div class="dialogContent">
      <slot />
    </div>
    <div slot="footer" class="dialog-footer">
      <slot name="buttonList">
        <el-button v-if="showQuit" size="mini" class="dialog-footer-button" @click="isshow = false"
          >取 消</el-button
        >
        <el-button
          type="primary"
          size="mini"
          class="dialog-footer-button othersButton"
          :disabled="!isCheck"
          @click="check"
          >{{ checkText }}</el-button
        >
      </slot>
    </div>
  </el-dialog>
</template>

<script>
export default {
  name: 'Dialog',
  components: {},
  props: {
    width: {
      type: String,
      default: '60%',
    },
    title: {
      type: String,
      default: 'dialog',
    },
    clickModalClose: {
      type: Boolean,
      default: false,
    },
    showQuit: {
      type: Boolean,
      default: true,
    },
    checkText: {
      type: String,
      default: '保 存',
    },
  },
  data() {
    return {
      isCheck: true, // 判定是否可以提交（用于阻止延时提交方案）
      isshow: false,
    }
  },
  computed: {},
  methods: {
    openDialog() {
      this.isshow = true
      // eslint-disable-next-line promise/param-names
      return new Promise((res) => {
        res()
      })
    },
    closeDialog() {
      this.isshow = false
    },
    check() {
      this.isCheck = false
      this.$emit('checkFn')
      setTimeout(() => {
        this.isCheck = true
      }, 1000)
    },
  },
}
</script>
<style lang="scss">
.el-dialog {
  position: absolute;
  left: 0;
  right: 0;
  margin-top: 9vh !important;
}
.el-dialog__body {
  padding: 16px 20px 0 20px;
  overflow: auto;
}
.el-dialog__header {
  border: 1px solid #f0f0f0;
}
</style>
<style lang="scss" scoped>
.dialogContent {
  width: 100%;
  max-height: 65vh;
}
.othersButton {
  background: linear-gradient(180deg, #ffddb7 0%, #d5966b 100%);
  border: none;
  font-weight: 500;
  font-size: 0.88rem;
  margin: 0 0.75rem;
}
/deep/.el-button--primary {
  background: linear-gradient(180deg, #6b73ff 0%, #484eed 100%);
  border: 1px solid;
}
/deep/.el-dialog__title {
  line-height: 1.5rem;
  font-size: 1rem;
  color: #262626;
  font-weight: 500;
}
</style>
<template>
  <div class="page-toast">
    <h1 class="page-title">Toast</h1>
    <div class="page-toast-wrapper">
      <mt-button @click.native="openToast" size="large">点击弹出 Toast</mt-button>
      <mt-button @click.native="openToastWithIcon" size="large">点击弹出带有 icon 的 Toast</mt-button>
      <mt-button @click.native="openBottomToast" size="large">自定义 Toast 位置</mt-button>
    </div>
  </div>
</template>

<style>
.page-toast {}
.page-toast-wrapper {
    padding: 0 20px;
    top: 50%;
    position: absolute;
    width: 100%;
    -webkit-transform: translateY(-50%);
            transform: translateY(-50%);
}
.page-toast-wrapper button:not(:last-child) {
    margin-bottom: 20px;
}


</style>

<script type="text/babel">
  import { Toast } from 'mint-ui';

  export default {
    methods: {
      openToast() {
        Toast('提示信息');
      },

      openToastWithIcon() {
        Toast({
          message: '操作成功',
          iconClass: 'mintui mintui-success'
        });
      },

      openBottomToast() {
        Toast({
          message: '提示信息',
          position: 'bottom'
        });
      }
    }
  };
</script>

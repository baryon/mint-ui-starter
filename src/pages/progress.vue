<template>
  <div class="page-progress">
    <h1 class="page-title">Progress</h1>
    <mt-cell title="默认">
      <mt-progress></mt-progress>
    </mt-cell>
    <mt-cell title="设置 value">
      <mt-progress :value="20"></mt-progress>
    </mt-cell>
    <mt-cell title="左右文字">
      <mt-progress :value="40">
        <div slot="start">0%</div>
        <div slot="end">100%</div>
      </mt-progress>
    </mt-cell>
    <mt-cell title="定义线宽">
      <mt-progress :value="60" :bar-height="5"></mt-progress>
    </mt-cell>
    <div class="page-progress-wrapper">
      <mt-button size="large" type="primary" @click.native="uploadFile">上传文件</mt-button>
      <mt-progress :value="value" v-if="progressVisible" transition="progress-fade">
        <div slot="end">{{ value }}%</div>
      </mt-progress>
    </div>
  </div>
</template>

<style>

.mt-progress {
    position: relative;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    height: 30px;
    line-height: 30px
}
.mt-progress > * {
    display: -ms-flexbox;
    display: flex;
    display: -webkit-box
}
.mt-progress *[slot="start"] {
    margin-right: 5px
}
.mt-progress *[slot="end"] {
    margin-left: 5px
}
.mt-progress-content {
    position: relative;
    -webkit-box-flex: 1;
        -ms-flex: 1;
            flex: 1
}
.mt-progress-runway {
    position: absolute;
    -webkit-transform: translate(0, -50%);
            transform: translate(0, -50%);
    top: 50%;
    left: 0;
    right: 0;
    background-color: #ebebeb;
    height: 3px
}
.mt-progress-progress {
    position: absolute;
    display: block;
    background-color: #26a2ff;
    top: 50%;
    -webkit-transform: translate(0, -50%);
            transform: translate(0, -50%);
    width: 0
}


</style>

<script type="text/babel">
  import { Toast } from 'mint-ui';

  export default {
    data() {
      return {
        progressVisible: false,
        value: 0,
        uploading: false,
        timer: null
      };
    },

    watch: {
      value(val) {
        if (val >= 100) {
          this.uploading = false;
          this.progressVisible = false;
          setTimeout(() => Toast({ message: '上传成功', position: 'bottom', duration: 1000 }), 200);
          clearTimeout(this.timer);
        }
      }
    },

    methods: {
      uploadFile() {
        if (!this.uploading) {
          this.value = 0;
          this.progressVisible = true;
          this.uploading = true;
          this.timer = setInterval(() => this.value++, 10);
        }
      }
    }
  };
</script>
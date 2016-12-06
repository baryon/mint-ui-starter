<template>
  <div class="page-popup">
    <h1 class="page-title">Popup</h1>
    <div class="page-popup-wrapper">
      <mt-button @click.native="popupVisible1 = true" size="large" ref="button">中部弹出 popup</mt-button>
      <mt-button @click.native="popupVisible2 = true" size="large">上侧弹出 popup</mt-button>
      <mt-button @click.native="popupVisible3 = true" size="large">右侧弹出 popup</mt-button>
      <mt-button @click.native="popupVisible4 = true" size="large">下侧弹出 popup</mt-button>
    </div>
    <mt-popup v-model="popupVisible1" popup-transition="popup-fade" class="mint-popup-1" :style="{ top: buttonBottom + 10 + 'px' }">
      <h1>popup</h1>
      <p>/ ˈpɑpˌʌp /</p>
      <p>n. 弹出式; [棒]内野飞球; 自动起跳式装置</p>
      <p>adj. 弹起的; 有自动起跳装置的</p>
    </mt-popup>
    <mt-popup v-model="popupVisible2" position="top" class="mint-popup-2" :modal="false">
      <p>更新成功</p>
    </mt-popup>
    <mt-popup v-model="popupVisible3" position="right" class="mint-popup-3" :modal="false">
      <mt-button @click.native="popupVisible3 = false" size="large" type="primary">关闭 popup</mt-button>
    </mt-popup>
    <mt-popup v-model="popupVisible4" position="bottom" class="mint-popup-4">
      <mt-picker :slots="dateSlots" @change="onDateChange" :visible-item-count="5" :show-toolbar="false"></mt-picker>
    </mt-popup>
  </div>
</template>

<style>

.page-popup .mint-popup-1 {
    width: 200px;
    border-radius: 8px;
    padding: 10px;
    -webkit-transform: translate(-50%, 0);
            transform: translate(-50%, 0);
}
.page-popup .mint-popup-1 h1 {
    font-size: 20px;
    color: #26a2ff;
}
.page-popup .mint-popup-1 p {
    margin-bottom: 10px;
}
.page-popup .mint-popup-1::before {
    display: inline-block;
    width: 0;
    height: 0;
    border: solid transparent;
    border-width: 10px;
    border-bottom-color: #fff;
    content: '';
    position: absolute;
    top: -20px;
    right: 50px;
}
.page-popup .mint-popup-2 {
    width: 100%;
    height: 50px;
    text-align: center;
    background-color: rgba(0,0,0,.7);
    -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
}
.page-popup .mint-popup-2 p {
    line-height: 50px;
    color: #fff;
}
.page-popup .mint-popup-3 {
    width: 100%;
    height: 100%;
    background-color: #fff;
}
.page-popup .mint-popup-3 .mint-button {
    position: absolute;
    width: 90%;
    top: 50%;
    left: 5%;
    -webkit-transform: translateY(-50%);
            transform: translateY(-50%);
}
.page-popup .mint-popup-4 {
    width: 100%;
}
.page-popup .mint-popup-4 .picker-slot-wrapper, .page-popup .mint-popup-4 .picker-item {
    -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
}
.page-popup-wrapper {
    padding: 0 20px;
    top: 50%;
    position: absolute;
    width: 100%;
    -webkit-transform: translateY(-50%);
            transform: translateY(-50%);
}
.page-popup-wrapper button:not(:last-child) {
    margin-bottom: 20px;
}

</style>

<script type="text/babel">
  export default {
    data() {
      return {
        popupVisible1: false,
        popupVisible2: false,
        popupVisible3: false,
        popupVisible4: false,
        buttonBottom: 0,
        dateSlots: [
          {
            flex: 1,
            values: ['2016-01', '2016-02', '2016-03', '2016-04', '2016-05', '2016-06'],
            className: 'slot1',
            textAlign: 'right'
          }, {
            divider: true,
            content: '-',
            className: 'slot2'
          }, {
            flex: 1,
            values: ['2016-01', '2016-02', '2016-03', '2016-04', '2016-05', '2016-06'],
            className: 'slot3',
            textAlign: 'left'
          }
        ]
      };
    },

    watch: {
      popupVisible2(val) {
        if (val) {
          setTimeout(() => {
            this.popupVisible2 = false;
          }, 2000);
        }
      }
    },

    methods: {
      onDateChange(picker, values) {
        if (values[0] > values[1]) {
          picker.setSlotValue(1, values[0]);
        }
        this.dateStart = values[0];
        this.dateEnd = values[1];
      }
    },

    mounted() {
      this.buttonBottom = this.$refs.button.$el.getBoundingClientRect().bottom;
    }
  };
</script>

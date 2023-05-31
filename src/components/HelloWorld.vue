<template>
  <div class="container">
    <div ref="cir" class="main">
      <svg viewBox="0 0 1040 1040">
        <path
          style="fill: none; stroke: #e6e9f1; stroke-width: 40px"
          d="M 520 520 m 0 -500 a 500 500 0 1 1 0 1000 a 500 500 0 1 1 0 -1000"
        ></path>
        <path
          style="
            fill: none;
            stroke: #8e6bf0;
            stroke-width: 40px;
            stroke-linecap: round;
            stroke-dasharray: 0px, 3140px;
          "
          d="M 520 520 m 0 -500 a 500 500 0 1 1 0 1000 a 500 500 0 1 1 0 -1000"
        ></path>
      </svg>
      <div class="progress-text">
        <span class="text-value"
          ><span class="value-num">{{ sliderValue }}</span
          >%</span
        >
        <span class="text-word">异常分数</span>
      </div>
    </div>
    <a-slider v-model="sliderValue" @change="changeSlider" />
    <div class="bottom">
      <div>
        <img class="bottom-pic" v-if="isUnkown" src="../assets/weizhi@3x.png" />
        <img
          class="bottom-pic"
          v-if="isNormal"
          src="../assets/zhengchang@3x.png"
        />
        <img
          class="bottom-pic"
          v-if="isWarning"
          src="../assets/baojing@3x.png"
        />
      </div>
      <div class="bottom-word">
        <span class="status-key">检测状态</span>
        <div class="status-value">
          <span v-if="isUnkown">未知</span>
          <span class="status-normal" v-if="isNormal">正常</span>
          <span class="status-warning" v-if="isWarning">报警</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "ant-design-vue/dist/antd";
export default {
  name: "HelloWorld",
  data() {
    return {
      sliderValue: 0, // 百分比值
      cir: "",
      paths: "",
    };
  },
  mounted() {
    this.cir = this.$refs.cir;
    this.paths = this.cir.children[0].children;
  },
  computed: {
    isUnkown: function () {
      return this.sliderValue === 0;
    },
    isNormal: function () {
      return this.sliderValue > 0 && this.sliderValue < 50;
    },
    isWarning: function () {
      return this.sliderValue >= 50;
    },
  },
  methods: {
    changeSlider(value) {
      this.sliderValue = value;
      this.computedTime();
    },
    computedTime() {
      let sum = (3104 * this.sliderValue) / 100; //计算进度条的长度
      this.paths[1].style.strokeDasharray = `${sum},3104`; //设置进度条长度
    },
  },
};
</script>

<style scoped>
.container {
  width: 300px;
  margin: 0 auto;
}

.main {
  position: relative;
}

.progress-text {
  width: 128px;
  position: absolute;
  top: 26%;
  left: 30%;
  display: flex;
  flex-direction: column;
}

.text-value {
  color: #7566f6;
  font-size: 36px;
}

.value-num {
  font-size: 56px;
}

.text-word {
  color: #565685;
  font-size: 24px;
}

.bottom {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 40px;
}

.bottom-pic {
  width: 92px;
}

.bottom-word {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  margin-left: 18px;
}

.status-key {
  font-size: 24px;
  color: #9393b1;
}

.status-value {
  font-size: 24px;
  color: #9191b0;
}

.status-normal {
  color: #80c6fa;
}

.status-warning {
  color: #e0615b;
}
</style>

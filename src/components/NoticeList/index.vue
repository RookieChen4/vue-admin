<template>
  <div class="container-scroll">
    <div class="textBox">
      <transition name="slide">
        <p :key="text.id" class="text">{{ text.val }}</p>
      </transition>
    </div>
    <div v-for="(item, index) in textArr2" :key="index">
      <p>{{ item }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Scroll',
  data() {
    return {
      textArr: [
        '1 第一条公告',
        '2 第二条公告第二条公告',
        '3 第三条公告第三条公告第三条公告'
      ],
      textArr2: [],
      number: 0
    }
  },
  computed: {
    text() {
      return {
        id: this.number,
        val: this.textArr[this.number]
      }
    }
  },
  mounted() {
    this.textArr2 = [
      '1 第一条公告',
      '2 第二条公告第二条公告',
      '3 第三条公告第三条公告第三条公告'
    ]
    this.startMove()
  },
  methods: {
    startMove() {
      // eslint-disable-next-line
      let temp = [...this.textArr]
      // eslint-disable-next-line no-unused-vars
      let timer = setTimeout(() => {
        if (this.number === this.textArr.length - 1) {
          this.textArr2 = [...temp]
          this.number = 0
        } else {
          this.textArr2.splice(this.number, 1)
          this.number += 1
        }
        timer = null
        this.startMove()
      }, 2000) // 滚动不需要停顿则将2000改成动画持续时间
    }
  }
}
</script>

<style scoped>
.container-scroll {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
  h2 {
    padding: 20px 0
  }
  .textBox {
    width: 100%;
    height: 40px;
    margin: 0 auto;
    overflow: hidden;
    position: relative;
    text-align: center;
  }
  .text {
    width: 100%;
    position: absolute;
    bottom: 0;
  }
  .slide-enter-active, .slide-leave-active {
    transition: all 0.5s linear;
  }
  .slide-enter{
    transform: translateY(20px) scale(1);
    opacity: 1;
  }
  .slide-leave-to {
    transform: translateY(-20px) scale(0.8);
    opacity: 0;
  }
</style>

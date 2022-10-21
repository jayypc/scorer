<template>
  <div>
    <div class="numBox">

       <div class="numBox">
            <div v-for="(item, index) in dayData" :key="index" class="numItem">
              <div class="tranNum">
                <i class="visNum" ref="numberItem">0123456789</i>
              </div>
            </div>
          </div>
      <!-- <div class="numItem" v-for="(item, index) in dayData" :key="index">
        <div class="trans">
          <div ref="numberItem" class="visNum">0123456789~</div>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data () {
    return {
      dayData: []
    }
  },
  created () {},
  mounted () {
    this.toOrderNum(123121)
    setTimeout(() => {
      this.toOrderNum(5467451)
    }, 3000)
  },
  methods: {
    toOrderNum (val) {
      let num = val.toString()
      this.dayData = num

      this.orderNum = num.split('')
      this.$nextTick(() => {
        this.setNumberTransform()
      })
    },
    // 设置文字滚动
    setNumberTransform () {
      const numberItems = this.$refs.numberItem

      const numberArr = this.orderNum.filter((item) => item)

      // const elem = numberItems[index];
      // elem.style.transform = `translate(0%, -${numberArr[index] * 10}%)`;
      for (let index = 0; index < numberItems.length; index++) {
        const elem = numberItems[index]

        elem.style.transform = `translate(0%, -${numberArr[index] * 10}%)`
      }
    }
  }
}
</script>

<style scoped>
.numBox {
  display: flex;
  flex-wrap: nowrap;
  margin-top: 300px;
  margin-left: 100px;
  /* border: 1px solid blue; */
}

.numItem {
  width: 35px;
  height: 40px;
  padding: 2px;
  margin-right: 2%;
  font-size: 32px;
  font-weight: 900;
  text-align: center;
  box-sizing: border-box;
  /* border: 1px solid #e6e6e6; */
  /* box-shadow: 0 0 5px #a9cad4 inset; */
  /* position: relative; */
}
.tranNum {
  position: relative;
  width: 100%;
  height: 100%;
  writing-mode: vertical-rl;
  text-orientation: upright;
  overflow: hidden;
}
.visNum {
  font-style: normal;
  position: absolute;
  top: -4px;
  left: -12px;
  font-weight: 700;
  color: #2d7cff;
  /* transform: translate(-50%, 0); */
  transition: transform 3s ease-in-out;
  letter-spacing: 10px;
}
</style>

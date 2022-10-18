<template>
  <div id="app">
    <v-touch v-on:swipeleft="pointClick(-1)" v-on:swiperight="pointClick(1)" v-on:swipeup="pointClick(2)" v-on:swipedown="pointClick(-2)" v-on:doubletap="pointClick(0)">
      <div class="container-fluid">
        <div class="row">
          <div class="col-6 buleb" :style="{ height: screenHeight + 'px' }">
            <div style="height:10%">
              <auto-size-span object-fit="contain" class="autosize" text="蓝队"></auto-size-span>
            </div>
            <div style="height:90%" @click="pointClick(1)">
              <auto-size-span object-fit="contain" class="autosize" :text="bluePoint"></auto-size-span>
            </div>
          </div>
          <div class="col-6 redb" :style="{ height: screenHeight + 'px' }">
            <div style="height:10%">
              <auto-size-span object-fit="contain" class="autosize" text="红队"></auto-size-span>
            </div>
            <div style="height:90%" @click="pointClick(2)">
              <auto-size-span object-fit="contain" class="autosize" :text="redPoint"></auto-size-span>
            </div>
          </div>
        </div>
      </div>
      <div class="mainIcon" @click="pointClick(0)">
        <b-icon icon="arrow-counterclockwise" style="color:white" font-scale="4"></b-icon>
      </div>
    </v-touch>
  </div>
</template>

<script>
import autoSizeSpan from 'auto-size-span'

export default {
  name: 'App',
  components: {
    autoSizeSpan
  },
  data () {
    return {
      screenWeight: 0,
      screenHeight: 0,
      bluePoint: 0,
      redPoint: 0
    }
  },
  mounted () {
    this.screenWeight = document.documentElement.clientWidth
    this.screenHeight = document.documentElement.clientHeight

    var _this = this
    window.onresize = function () {
      _this.screenHeight = document.documentElement.clientHeight
    }
  },
  methods: {
    pointClick (type) {
      if (type === 0) {
        this.bluePoint = 0
        this.redPoint = 0
      } else if (type === 1) {
        this.bluePoint = this.bluePoint + 1
      } else if (type === 2) {
        this.redPoint = this.redPoint + 1
      } else if (type === -1) {
        this.bluePoint = this.bluePoint - 1
      } else if (type === -2) {
        this.redPoint = this.redPoint - 1
      }
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100%;
}

.buleb {
  background-color: #5990ea;
}

.redb {
  background-color: #e35549;
}

.buleb,.redb{
  color: white;
}

.autosize{
  height: 100%;
  width: 100%;
}

.mainIcon{
  width: 8%;
  height: 8%;
  position: absolute;
  left: 50%;
  top: 10%;
  margin-left: -4%;
  margin-top: -4%;
}
</style>

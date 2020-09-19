<template>
  <div class="home">
    <div class="flex flex-col w-full h-full justify-center items-center">
      <h1 class="text-4xl">{{time.min}} : {{time.sec}} : {{time.milsec}}</h1>
      <a v-if="isFreshLoad" @click="this.start">START</a>
      <div v-show="!isFreshLoad">
        <a v-show="isPause" @click="this.start">RESUME</a>
        <a v-show="isPause" @click="this.reset">RESET</a>
        <a v-show="!isPause" @click="this.pause">PAUSE</a>
      </div>
      <h1 class="text-2xl name self-end">Stopwatch by {{name}}</h1>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue';

export default {
  name: 'Home',
  components: {
    // HelloWorld,
  },
  data() {
    return {
      name: 'Malcolm',
      time: {
        sec: 0,
        milsec: 0,
        min: 0,
      },
      isFreshLoad: true,
      isPause: false,
      interval: null,
    };
  },
  mounted() {},
  computed: {
    // startOrResume: function(){
    //   return this.isFreshLoad ? 'START' : 'RESUME';
    // },
  },
  methods: {
    start() {
      this.isFreshLoad = false;
      this.isPause = false;
      const self = this;
      this.interval = setInterval(() => {
        if (self.time.milsec + 1 < 100) {
          self.time.milsec += 1;
        } else if (self.time.sec + 1 < 60) {
          self.time.milsec = 0;
          self.time.sec += 1;
        } else {
          self.time.sec = 0;
          self.time.min += 1;
        }
      }, 10);
    },
    pause() {
      this.isPause = true;
      clearInterval(this.interval);
    },
    reset() {
      clearInterval(this.interval);
      this.isFreshLoad = true;
      this.time.sec = 0;
      this.time.milsec = 0;
      this.time.min = 0;
    },
  },
};
</script>

<style lang="scss" scoped>
a {
  background-color: #ccd5ff;
}
.name {
  background-color: #c884a6;
}
// body {
  // background-color: #23C9FF;
// }
// https://coolors.co/23c9ff-7cc6fe-ccd5ff-e7bbe3-c884a6
</style>

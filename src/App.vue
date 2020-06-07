<template lang="pug">
  #app
    .hitbox
      .imgbox
        img(src="./assets/normal.png" ref="face")
        img.con(src="./assets/con.png" v-if="hit")
      h1 {{say}} {{hittimes}}
      .hitme(v-on:touchstart="hitdown($event)",@touchend="hitup($event)"  @touchcancel="stop"  @mousedown="hitdown" @mouseleave="hitup" @mouseup="hitup", unselectable="on" onselectstart="return false;" ) 壓住開始揍人
</template>

<script>
export default {
  name: 'App',
  components: {},
  data() {
    return {
      hit: false,
      hittimes: 0,
      interval: false,
    };
  },
  computed: {
    say() {
      if (this.hittimes > 30) {
        switch (Math.floor(this.hittimes / 30)) {
          case 1:
            return '知道錯了啦啦';
          case 2:
            return '我以後會乖乖';
          case 3:
            return '不會惹你生氣';
          case 4:
            return '你看看臉很腫了啦';
          case 5:
            return '要出人命了！！';
          case 6:
            return '有話好好說';
          case 7:
            return '小的知錯';
          case 8:
            return '我是討厭鬼';
          case 9:
            return '最想要的還是你開心';
          case 10:
            return '不想被你討厭';
          case 11:
            return '真的真的';
          case 12:
            return '原諒我嘛';
          case 15:
            return '我真的很欠揍誒 揍很久..';
          case 16:
            return '不氣不氣！！！';

          default:
            return '原諒我嘛';
        }
      }
      return '是我不對啦';
    },
  },
  methods: {
    hitdown(e) {
      console.log('down');
      this.hit = true;
      e.target.style.transform = 'scaleY(.8)';
      this.$refs.face.setAttribute('src', `${require('./assets/hit.png')}`);
      console.log(this.$refs.face);
      this.hittimes++;
      var vm = this;
      if (!this.interval) {
        this.interval = setInterval(() => vm.hittimes++, 30);
      }
    },
    stop() {
      clearInterval(this.interval);
      this.interval = false;
    },
    hitup(e) {
      this.hit = false;
      e.target.style.transform = 'scaleY(1)';
      if (this.hittimes > 1000) {
        this.$refs.face.setAttribute('src', `${require('./assets/omg.png')}`);
      } else if (this.hittimes > 300) {
        this.$refs.face.setAttribute(
          'src',
          `${require('./assets/crycry.png')}`
        );
      } else if (this.hittimes > 100) {
        this.$refs.face.setAttribute('src', `${require('./assets/cry.png')}`);
      } else {
        this.$refs.face.setAttribute(
          'src',
          `${require('./assets/normal.png')}`
        );
      }
      this.stop();
    },
  },
};
</script>

<style lang="scss">
html,
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
  width: 100vw;
  justify-content: center;
  align-items: center;
  display: flex;
  background-color: #ed966a;

  @keyframes hit {
    0% {
      left: -90px;
    }
    30% {
      left: -30px;
    }
    100% {
      left: -90px;
    }
  }
  .hitbox {
    width: 50%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    align-items: center;
    .hitme {
      max-width: 300px;
      margin-top: 2rem;
      width: 100%;
      height: 60px;
      background-color: #fff;
      text-align: center;
      line-height: 60px;
      border-radius: 15px;
      font-weight: bold;
      border: black solid 4px;
      box-shadow: inset 0 -10px 0px #cfd8f0;
      transform: 0.3s;
    }
    .imgbox {
      position: relative;
      .con {
        position: absolute;
        width: 60%;
        left: 0;
        top: 50%;
        animation-name: hit;
        animation-duration: 0.2s;
        animation-direction: alternate;
        animation-iteration-count: infinite;
        animation-timing-function: ease-in-out;
      }
    }
    .hit {
      transform: scaleY(0.8);
    }
  }
  img {
    width: 100%;
    max-width: 250px;
  }
}
</style>

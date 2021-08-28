<template>
  <div class="home">
    <div class="theme-bg">
      <img class="bg05" :src="bg05" alt="bg03">
    </div>

    <div class="theme-text">
      <p class="text">送个可爱的</p>
      <p class="text">李婧同学❤</p>

      <div class="title">
        <h3>今天是认识你的第 {{day}} 天 {{hour}} 小时 {{minute}} 分钟 {{second}} 秒，祝你今天愉快。你明天的愉快留着我明天再祝。</h3>
      </div>
    </div>

    <div class="bottom-bg">
      <img class="bg bg03" :src="bg03" alt="bg03">
      <img class="bg bg02" :src="bg02" alt="bg02">
      <img class="bg bg01" :src="bg01" alt="bg01">

      <img class="peopel peopel-l" :src="peopel01" alt="bg01">
      <img class="peopel peopel-r" :src="peopel02" alt="bg01">
    </div>
    <audio :src="bgm" autoplay>您的浏览器不支持 audio 标签。</audio>
  </div>
</template>

<script>
// @ is an alias to /src
import a01 from '@/assets/image/bg-bottom-0.png'
import a02 from '@/assets/image/bg-bottom-1.png'
import a03 from '@/assets/image/bg-bottom-2.png'
import a05 from '@/assets/image/bg-bottom-5.png'
import peopel01 from '@/assets/image/bg-bottom-3.png'
import peopel02 from '@/assets/image/bg-bottom-4.png'
import bgm from '@/assets/bgm/bgm.mp3'


export default {
  name: 'Home',
  data() {
    return {
      bg01: a01,
      bg02: a02,
      bg03: a03,
      bg05: a05,
      bgm: bgm,
      peopel01: peopel01,
      peopel02: peopel02,
      day: '',// 天
      hour: '',// 小时
      minute: '',// 分钟
      second: '',// 秒
    }
  },
  components: {},
  methods:{
    clock(){
      setInterval(timeRow.bind(this), 1000)


      function timeRow(){
        let startTime = new Date('2021-04-15')
        let nowTime = new Date()
        let time = getInterval(startTime, nowTime)

        this.day = time.day
        this.hour = time.hour
        this.minute = time.minute
        this.second = time.second

        function getInterval(start, end) {
          // 两个日期对象，相差的毫秒数
          let interval = end - start;
          // 求 相差的天数/小时数/分钟数/秒数
          let day = ''
          let hour = ''
          let minute = ''
          let second = ''

          // 两个日期对象，相差的秒数
          // interval = interval / 1000;
          interval /= 1000;

          day = parseInt(interval / 60 / 60 / 24);
          hour = parseInt(interval / 60 / 60 % 24);
          minute = parseInt(interval / 60 % 60);
          second = parseInt(interval % 60);

          return {
            day: day,
            hour: hour,
            minute: minute,
            second: second
          }
        }
      }
    },
  },
  mounted() {
    this.clock()
  }
}
</script>

<style lang="scss" scoped>
@function vw($px) {
  //这里是以移动端PSD设计稿 宽为750px，高为1334px为例，所以这里 除以750，以便在使用时，不用去计算倍数， PSD设计稿中的尺寸是多少，我们样式就是多少！！！
  @return ($px / 750) * 100vw;
}

@font-face {
  font-family: 'LOVE';
  /* 重命名字体名 */
  src: url('../assets/font/FangZhengKeAiDeKeAi-2.ttf');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

.theme-text{
  position: absolute;
  width: 100%;
  top: vw(200);
  left: 50%;
  transform: translateX(-50%);
  z-index: 99;
  opacity: 0;
  animation: text 1s linear;
  animation-delay: 5s;
  animation-fill-mode: forwards;
}

.title{
  font-family: 'LOVE';
  font-size: vw(30);
  padding: vw(180) vw(30);
}

.text{
  font-family: 'LOVE';
  font-size: vw(80);
  font-weight: bold;
  margin: 0;
}

.home {
  max-width: 750px;
  height: 100vh;
  overflow: hidden;
  margin: 0 auto;
  position: relative;
  > .bottom-bg {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;

    > .bg {
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;

      animation: offset 2s linear;
    }

    > .peopel {
      position: absolute;
      bottom: 0;
      height: vw(400);
    }

    > .peopel-l {
      left: vw(-300);
      animation: peopelOffsetL 3s linear;
      animation-delay: 2s;
      animation-fill-mode: forwards;
    }

    > .peopel-r {
      right: vw(-300);
      animation: peopelOffsetR 3s linear;
      animation-delay: 2s;
      animation-fill-mode: forwards;
    }
  }

  > .theme-bg{
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    > .bg05{
      width: 100%;
      transform: translateY(-100%);
      animation: themeBg 3s linear;
      animation-delay: 2s;
      animation-fill-mode: forwards;
    }
  }
}

@keyframes offset {
  from {
    transform: translateY(100%)
  }
  to {
    transform: translateY(0)
  }
}

@keyframes peopelOffsetL {
  from {
    left: vw(-300)
  }
  to {
    left: vw(20)
  }
}

@keyframes peopelOffsetR {
  from {
    right: vw(-300)
  }
  to {
    right: vw(20)
  }
}

@keyframes themeBg {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0);
  }
}

@keyframes text {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

</style>

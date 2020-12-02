<template>
  <div id="app">
    <Head>大数据预警平台</Head>
    <div class="container">
      <div class="left-wrapper">
        <div style="height:320px; margin-bottom: 16px">
          <Card :title="'数据统计'">
            <div class="today-count">
              <span class="title">今日军营人数</span>
              <span class="count" :style="{paddingLeft: allPersonLeft + 'px'}">{{ allPerson }}</span>
            </div>
            <div class="split"></div>
            <div class="today-count warning">
              <span class="title">今日报警总数</span>
              <span class="count" :style="{paddingLeft: warningPersonLeft + 'px'}">{{ warningPerson }}</span>
            </div>
            <div class="total-wrapper">
              <div class="total-item">
                <span>违规APP使用预警</span>
                <span>42</span>
              </div>
              <div class="split2"></div>
              <div class="total-item">
                <span>违规出行预警</span>
                <span>12</span>
              </div>
            </div>
          </Card>
        </div>
        <div style="height: 485px">
          <Card :title="'违规情况'">
            <ThreeDBar />
          </Card>
        </div>
      </div>
      <div class="center-wrapper">
        <div style="height: 320px; margin-bottom: 16px">
          <Card :title="'地图围栏'">
            <CityMap />
          </Card>
        </div>
      </div>
      <div class="right-wrapper">
        <div style="height: 320px; margin-bottom: 16px">
          <Card :title="'违规APP'">

          </Card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { Head, Card, ThreeDBar, CityMap } from '@/components'

export default {
  name: 'App',
  components: {
    Head,
    Card,
    ThreeDBar,
    CityMap
  },
  data () {
    return {
      allPerson: 1635,
      warningPerson: 455
    }
  },
  mounted() {
    console.log(this.allPerson.toString().length)
    console.log(this.warningPerson.toString().length)
  },
  computed: {
    allPersonLeft () {
      const numLength = this.allPerson.toString().length;
      return 9 + (4 - numLength) * 29;
    },
    warningPersonLeft () {
      const numLength = this.warningPerson.toString().length;
      return 9 + (4 - numLength) * 29;
    }
  }
}
</script>

<style lang="scss">
html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
#app {
  width: 100%;
  height: 100%;
  font-family: 'Microsoft YaHei';
  background-image: url('./assets/bg.png');
  background-position: center center;
  background-repeat: no-repeat;
}

.container{
  width: 100%;
  box-sizing: border-box;
  padding: 16px;
  display: flex;
  justify-content: space-between;

  .left-wrapper, .right-wrapper{
    width: 408px;
    height: 100%;
  }

  .center-wrapper{
    width: calc(100% - 816px);
    padding: 0px 16px;
    height: 100%;
  }
}

.today-count{
  width: 250px;
  display: flex;
  align-items: center;

  .title{
    width: 50%;
    padding: 0px 8px;
    font-size: 16px;
    box-sizing: border-box;
    color: #fff;
    font-family: Source Han Sans CN;
    text-shadow:  0 0 10px #fff,
                0 0 20px  #fff,
                0 0 30px  #fff;
  }
  
  .count {
    width: 116px;
    height: 44px;
    line-height: 44px;
    font-size: 20px;
    box-sizing: border-box;
    background-image: url('./assets/k1.png');
    background-repeat: repeat-x;
    color: #fff;
    text-shadow:  0 0 5px #fff,
                0 0 10px  #fff,
                0 0 15px  #fff;
    letter-spacing: 17px;
  }

  &.warning{

    .title{
      color:#fff;
      text-shadow:  0 0 5px #ff0000,
            0 0 10px  #ff0000,
            0 0 15px  #ff0000;
    }

    .count{
      text-align: right;
      background-image: url('./assets/k2.png');
    }
  }
}

.split{
  position:relative;
  width: 400px;
  height: 1px;
  margin: 20px 0px;
}
.split::before{
  content: '';
  position:absolute;
  background: linear-gradient(-90deg, #007EFB 0%, rgba(1, 118, 236, 0) 100%);
  width: 200px;
  height: 1px;
  top:0;
  left:0;
}
.split::after{
  content: '';
  position:absolute;
  background: linear-gradient(90deg, #007EFB 0%, rgba(1, 118, 236, 0) 100%);
  width: 200px;
  height: 1px;
  top: 0;
  right: 0;
}

.split2{
  position:relative;
  width: 1px;
  height: 76px;
}
.split2::before{
  content: '';
  position:absolute;
  background: linear-gradient(0deg, #007EFB 0%, rgba(1, 118, 236, 0) 100%);
  width: 1px;
  height: 38px;
  top:0;
  left:0;
}
.split2::after{
  content: '';
  position:absolute;
  background: linear-gradient(180deg, #007EFB 0%, rgba(1, 118, 236, 0) 100%);
  width: 1px;
  height: 38px;
  top: 38px;
  left: 0;
}

.total-wrapper{
  width: 100%;
  display: flex;
  margin: 30px 0px 48px 0px;

  .total-item{
    width: 49%;
    display: flex;
    flex-direction: column;
    align-items: center;

    & > span:nth-of-type(1) {
      font-size: 16px;
      color:#fff;
      text-shadow:  0 0 5px #FBC019,
            0 0 10px  #FBC019,
            0 0 15px  #FBC019;
      margin-bottom: 4px;
    }
    & > span:nth-of-type(2) {
      font-size: 30px;
      color:#FBC019;
      text-shadow:  0 0 5px #FBC019,
            0 0 10px  #FBC019,
            0 0 15px  #FBC019;
    }
  }
}
</style>

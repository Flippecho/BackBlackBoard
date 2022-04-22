<template>
  <div class="safety-report">
    <div class="left">
      <div id="map"></div>
      <div class="btn-container">
        <button class="btn-spin"
                :disabled="isPosValid"
                @click="clockIn"
                :data-content-default="this.posStatus"
                data-content-spinning="稍等片刻">
        </button>
      </div>
    </div>

    <div class="right">
      <div class="card align-middle box-shadow">
        <div class="card-header" @click="askForLeaveForAll" :data-bs-toggle="isAnyClickable"
             data-bs-target="#staticBackdrop">
          {{ this.dormitoryStatus.name }}
        </div>
        <div class="card-body">
          <div @click="pushToAskForLeave(curUser)" :data-bs-toggle="isClickable(curUser)"
               data-bs-target="#staticBackdrop" :key="curUser.id">
            <img :src="require('../assets/'+ curUser.name +'.jpg')" alt="">
            <p :class="dynamicColor(curUser)">{{ curUser.name }}</p>
          </div>
          <div v-for="person in roommateList" @click="pushToAskForLeave(person)" :data-bs-toggle="isClickable(person)"
               data-bs-target="#staticBackdrop" :key="person.id">
            <img :src="require('../assets/'+ person.name +'.jpg')" alt="">
            <p :class="dynamicColor(person)">{{ person.name }}</p>
          </div>
        </div>
        <div class="card-footer text-muted">点击头像即可上报外出情况哦！</div>
      </div>
      <button class="test btn-spin" @click="flag=!flag">{{ testContext }}</button>
      <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1"
           aria-labelledby="staticBackdropLabel" aria-hidden="true">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title m-auto" id="staticBackdropLabel">外出情况上报</h5>
            </div>
            <div class="modal-body">
              <div class="input-group mb-3">
                <span class="input-group-text">请假人</span>
                <input type="text" class="form-control" :placeholder="this.askForLeaveString" aria-label="Username"
                       aria-describedby="basic-addon1" readonly>
              </div>

              <div class="form-floating mb-3">
                <input type="text" class="form-control" id="floatingAddress" placeholder="外出地址">
                <label for="floatingAddress">外出地址</label>
              </div>

              <div class="form-floating">
                <input type="text" class="form-control" id="floatingReason" placeholder="外出事由">
                <label for="floatingReason">外出事由</label>
              </div>
            </div>
            <div class="input-group" style="margin: 1rem; width: calc(100% - 2rem)">
              <span class="input-group-text">预计返校时间</span>
              <input type="datetime-local" id="return-time" class="form-control"
                     name="return-time" :value="this.curTime"
                     :min="this.curTime">
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-primary" data-bs-dismiss="modal" @click="commitAskForLeave()">确认并提交
              </button>
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">取消并关闭</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AMapLoader from '@amap/amap-jsapi-loader';

export default {
  name: "SafetyReport",
  created() {
    const _this = this;

    AMapLoader.load({
      "key": "eb79d9afd5f0186d2e81a4a6693ee25a",              // 申请好的Web端开发者Key，首次调用 load 时必填
      "version": "2.0",                                       // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
      "plugins": ['AMap.Geolocation'],                        // 需要使用的的插件列表
    }).then((AMap) => {
      const map = new AMap.Map('map', {
        zoom: 13,  //设置地图显示的缩放级别
        center: [120.44, 30.52],//设置地图中心点坐标
        viewMode: '2D',  //设置地图模式
        lang: 'zh_cn',  //设置地图语言类型
      });
      AMap.plugin(['AMap.Geolocation'], function () {//异步同时加载多个插件
        const geolocation = new AMap.Geolocation();
        map.addControl(geolocation);
      });

      // 构造点标记
      const marker = new AMap.Marker({
        title: '寝室',
        position: this.dormitoryStatus.position
      });
      // 构造矢量圆形
      const circle = new AMap.Circle({
        center: new AMap.LngLat("120.44", "30.52"), // 圆心位置
        radius: _this.reasonableOffset,  //半径
        strokeColor: "#F33",  //线颜色
        strokeOpacity: 1,  //线透明度
        strokeWeight: 3,  //线粗细度
        fillColor: "#ee2200",  //填充颜色
        fillOpacity: 0.35 //填充透明度
      });

      // 将以上覆盖物添加到地图上
      // add方法可以传入一个覆盖物数组，将点标记和矢量圆同时添加到地图上
      map.add([marker, circle]);

      const geolocation = new AMap.Geolocation();

      geolocation.getCurrentPosition(function (status, result) {
        if (status === 'complete') {
          const p1 = marker.getPosition();
          const p2 = result.position;
          console.log(p1);
          console.log(p2);
          _this.distance = Math.round(p1.distance(p2));
          _this.curUser.position = p2;
          console.log(_this.distance);
        }
      });

    }).catch(e => {
      console.log(e);
    });
  },
  data() {
    return {
      distance: -1,
      reasonableOffset: 1000,
      curUser: {
        name: "张岩峰",
        id: 8208200003,
        clockIn: false,
        askForLeave: false,
        position: []
      },
      dormitoryStatus: {
        name: '不醒人室',
        clockIn: false,
        askForLeave: false,
        position: [120.44, 30.52]
      },
      roommateList: [
        {
          name: "秦伟卿",
          id: 8208200001,
          clockIn: false,
          askForLeave: false
        },
        {
          name: "张顺哲",
          id: 8208200002,
          clockIn: false,
          askForLeave: false
        },
        {
          name: "祝礼祥",
          id: 8208200004,
          clockIn: false,
          askForLeave: false
        }
      ],
      askForLeaveList: [],
      askForLeaveString: '',
      flag: false
    }
  },
  computed: {
    posStatus() {
      if (this.curHour < 21) return '21:00 后才能打卡哦！'
      else if (this.curUser.clockIn) return '打卡完成!';
      else if (this.distance < 0) return '正在获取定位...';
      // else if (this.distance <= this.reasonableOffset) return '好耶，可以打卡喽！';
      else if (this.flag === true || this.distance <= this.reasonableOffset) return '好耶，可以打卡喽！';
      else return '似乎你不在寝室呢?';
    },
    isPosValid() {
      if (this.curHour >= 21 && this.flag === true) return false;
      return this.curHour < 21 || !(this.distance >= 0 && this.distance <= this.reasonableOffset) || this.curUser.clockIn;
    },
    curTime() {
      let timestamp = Date.now();
      let timezoneOffset = new Date().getTimezoneOffset();
      let curTime = new Date(timestamp - timezoneOffset * 60 * 1000);
      return curTime.toJSON().slice(0, 16);
    },
    isAnyClickable() {
      if (!this.curUser.askForLeave) return 'modal';
      for (const person of this.roommateList)
        if (!person.askForLeave) return 'modal';
      return '';
    },
    curHour() {
      return new Date().getHours();
    },
    testContext() {
      if (this.flag) return "丢弃金手指";
      else return "一键无视距离";
    }
  },
  methods: {
    clockIn() {
      this.curUser.clockIn = true;
      this.curUser.askForLeave = false;
    },
    pushToAskForLeave(person) {
      this.askForLeaveList = [];
      if (!person.askForLeave) this.askForLeaveList.push(person);
      this.updateAskForLeaveString();
    },
    askForLeaveForAll() {
      this.askForLeaveList = [];
      if (!this.curUser.askForLeave) this.askForLeaveList.push(this.curUser);
      for (const person of this.roommateList) {
        if (!person.askForLeave) this.askForLeaveList.push(person);
      }
      this.updateAskForLeaveString();
    },
    updateAskForLeaveString() {
      let str = '';
      for (const person of this.askForLeaveList) str += person.name + '、';
      str = str.slice(0, -1);
      this.askForLeaveString = str;
    },
    dynamicColor(person) {
      if (person.clockIn) return 'text-success';
      else if (person.askForLeave) return 'text-warning';
      else if (this.curHour < 22) return 'text-dark'
      else return 'text-danger';
    },
    isClickable(person) {
      if (!person.askForLeave) return 'modal';
      else return '';
    },
    commitAskForLeave() {
      for (const person of this.askForLeaveList) {
        person.clockIn = false;
        person.askForLeave = true;
      }
    },
    changeVal(val) {
      this.dormitoryStatus.position = val;
    }
  }
}

</script>


<style scoped>

.safety-report {
  display: grid;
  grid-template-columns: calc(100vw - 9rem - 28rem) 28rem;
}

.left {
  display: grid;
  grid-template-rows: calc(100vh - 9rem) 9rem;
}

#map {
  margin: var(--gap-y) 7rem 0 7rem;
  height: calc(100vh - 12rem);
  border-radius: 2.5rem;
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  box-shadow: 7px 7px 21px #d6d6d6,
  -7px -7px 21px #ffffff;
}

.btn-container {
  margin: var(--gap-y) var(--gap-x);
}

.btn-spin {
  font-size: 1.4rem;
  padding: 0.8rem;
  color: #3C374A;
  border-radius: 1.5rem;
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  box-shadow: 7px 7px 21px #d6d6d6,
  -7px -7px 21px #ffffff;
}

.card {
  --card-height: 38.25rem;
  --half-card-y: calc((100vh - var(--card-height)) / 2);
  /*margin: var(--half-card-y) var(--gap-x) var(--half-card-y) 0;*/
  margin: 3rem var(--gap-x) 3rem 0;
}

.card-header {
  font-size: 2rem;
  padding: 1rem;
}

.card-body {
  margin: 2rem;
  padding: 0;
  display: grid;
  grid-template-columns: 10rem 10rem;
}

.card-body > div {
  width: 8rem;
  margin: 1rem;
}

.card-body > div > img {
  width: 6rem;
  border-radius: 50%;
  padding: 0;
  margin: 1rem;
}

.card-body > div > p {
  font-size: 1.5rem;
  padding: 0.5rem;
  margin: 0;
  text-align: center;
}

.card-footer {
  font-size: 1rem;
  padding: 0.5rem;
  margin: 0;
}

.modal-content {
  border-radius: 25px;
  background: #ffffff;
  box-shadow: inset 16px 16px 32px #e8e8e8,
  inset -16px -16px 32px #ffffff;
}

.modal-footer {
  display: grid;
  grid-template-columns: 50% 50%;
}

.modal-footer > button {
  margin: 0 1.5rem;
  border-radius: 1.5rem;
}

.test {
  border: 0;
  border-radius: 7px;
  background: linear-gradient(145deg, #e6e6e6, #ffffff);
  box-shadow: 35px 35px 70px #e6e6e6,
  -35px -35px 70px #ffffff;
  margin-right: var(--gap-x);
  font-size: 1.2rem;
  text-align: left;
  padding: 0.5rem 2rem;
}

</style>
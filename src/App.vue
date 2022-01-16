<template>
  <div id="app" class="noSelect">
    <ul id="dock">
      <li class="icon" v-for="tab in tabs" :key="tab.id" @click="change(tab)" @animationend="reset(tab.id)"
          :class="{'loading':showAnimate[tab.id]}">
        <img :src="require('./assets/'+ tab.title +'.svg')" alt="" :title="tab.title" data-bs-toggle="tooltip"
             data-bs-placement="right">
      </li>
    </ul>
    <transition name="slide-fade" mode="out-in" appear>
      <keep-alive>
        <component id="panel" :is="currentTab"></component>
      </keep-alive>
    </transition>
  </div>
</template>

<script>
import InfoFlow from "@/components/InfoFlow";
import SafetyReport from "@/components/SafetyReport";
import YouthStudy from "@/components/YouthStudy";
import Curriculum from "@/components/Curriculum";
import EmptyClassrooms from "@/components/EmptyClassrooms";
import Personalization from "@/components/Personalization";

export default {
  name: 'App',
  data() {
    return {
      currentTab: InfoFlow,
      tabs: [
        {
          id: 1,
          title: "信息流",
          component: {InfoFlow},
          name: InfoFlow
        },
        {
          id: 2,
          title: "报寝",
          component: {SafetyReport},
          name: SafetyReport
        },
        {
          id: 3,
          title: "青年大学习",
          component: {YouthStudy},
          name: YouthStudy
        },
        {
          id: 4,
          title: "课表",
          component: {Curriculum},
          name: Curriculum
        },
        {
          id: 5,
          title: "空教室",
          component: {EmptyClassrooms},
          name: EmptyClassrooms
        },
        {
          id: 6,
          title: "个性化",
          component: {Personalization},
          name: Personalization
        }
      ],
      showAnimate: [false, false, false, false, false, false, false]
    }
  },
  methods: {
    change(tab) {
      if(tab.name != this.currentTab) {
        this.currentTab = tab.name;
        this.showAnimate[tab.id] = true;
      }
    },
    reset(id) {
      this.showAnimate[id] = false;
    }
  },
  mounted() {
    document.getElementById('dock').onmousemove = function (e) {
      e.currentTarget.querySelectorAll('img').forEach((img) => {
        const centroidY = img.offsetTop + img.offsetHeight / 2;
        const y = e.clientY - centroidY;
        img.style.setProperty("width", Math.exp(-y * y / 64 / 64) * 2 + 3 + 'rem');
      })
    }

    document.getElementById('dock').onmouseleave = function (e) {
      e.currentTarget.querySelectorAll('img').forEach((img) => {
        img.style.setProperty("width", 3 + 'rem');
      })
    }

    const tooltipTriggerList = [].slice.call(document.querySelectorAll('[data-bs-toggle="tooltip"]'));
    const tooltipList = tooltipTriggerList.map(function (tooltipTriggerEl) {
      // eslint-disable-next-line no-undef
      return new bootstrap.Tooltip(tooltipTriggerEl)
    });

  }
};
</script>

<style>
#app {
  background-image: linear-gradient(transparent 98%, #BDBDBD 98%),
  linear-gradient(to right, transparent 98%, #BDBDBD 98%);
  background-size: 2rem 2rem;
  background-repeat: repeat;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
}

#dock {
  width: 5rem;
  height: 34rem;
  padding: 0;
  margin: calc((100vh - 34rem) / 2) 0 calc((100vh - 34rem) / 2) 3rem;
  float: left;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border-radius: 2.5rem;
  background: linear-gradient(145deg, #ffffff, #e6e6e6);
  box-shadow: 7px 7px 21px #d6d6d6,
  -7px -7px 21px #ffffff;
}

.icon {
  list-style: none;
  margin: 1rem;
}

.icon > img {
  width: 3rem;
  overflow: hidden;
}

#panel {
  width: calc(100vw - 11rem);
  height: calc(100vh - 3rem);
  padding: 0;
  margin: 3rem 3rem 0 0;
  float: right;
}

.loading {
  animation: 0.5s loading ease-in;
}

@keyframes loading {
  0%, 100% {
    transform: translateX(0px);
  }
  60% {
    transform: translateX(-40px);
  }
}

</style>

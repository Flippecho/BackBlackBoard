<template>
  <div id="the-content">
    <div id="the-sidebar">
      <div id="tab-container">
        <div v-for="tab in tabs"
             :key="tab.id"
             :title="tab.title"
             @click="change(tab.name)"
             class="tab-item">
          <button class="particles-button"
                  :style="tab.style">{{ tab.title }}
          </button>
        </div>
      </div>
    </div>
    <div id="the-panel" :is="currentTab" keep-alive></div>
  </div>
</template>

<script>
import TheContentInfoFlow from "@/components/TheContentInfoFlow";
import TheContentSafetyReport from "@/components/TheContentSafetyReport";
import TheContentYouthStudy from "@/components/TheContentYouthStudy";
import TheContentCurriculum from "@/components/TheContentCurriculum";
import TheContentEmptyClassrooms from "@/components/TheContentEmptyClassrooms";
import TheContentSetting from "@/components/TheContentSetting";

export default {
  name: "TheContent",
  data() {
    return {
      currentTab: TheContentInfoFlow,
      tabs: [
        {
          id: 1,
          title: "信息流",
          style: {
            background: '#99b998',
            width: '116px'
          },
          component: {TheContentInfoFlow},
          name: TheContentInfoFlow
        },
        {
          id: 2,
          title: "报寝",
          style: {
            background: '#E4B794',
            width: '92px'
          },
          component: {TheContentSafetyReport},
          name: TheContentSafetyReport
        },
        {
          id: 3,
          title: "青年大学习",
          style: {
            background: '#f4837d',
            width: '148px'
          },
          component: {TheContentYouthStudy},
          name: TheContentYouthStudy
        },
        {
          id: 4,
          title: "课表",
          style: {
            background: '#ea495f',
            width: '92px'
          },
          component: {TheContentCurriculum},
          name: TheContentCurriculum
        },
        {
          id: 5,
          title: "空教室",
          style: {
            background: '#f8B500',
            width: '116px'
          },
          component: {TheContentEmptyClassrooms},
          name: TheContentEmptyClassrooms
        },
        {
          id: 6,
          title: "设置",
          style: {
            background: '#777bce',
            width: '92px'
          },
          component: {TheContentSetting},
          name: TheContentSetting
        }
      ]
    }
  },
  methods: {
    change(tabName) {
      this.currentTab = tabName;
    }
  }
}
</script>

<style scoped>

#the-panel {
  display: flex;
  align-items: center;
  justify-content: center;
  float: right;
  position: relative;
  width: 80%;
  height: 80vh;
  top: 5vh;
}

#the-sidebar {
  display: flex;
  align-items: center;
  float: left;
  position: relative;
  width: 20%;
  top: 5vh;
  height: 80vh;
  overflow: hidden;
}

.tab-item {
  position: relative;
  display: grid;
  overflow: hidden;
  height: 56px;
  margin-top: 11px;
  border-radius: 11px;
}

.particles-button {
  height: 56px;
  cursor: pointer;
  overflow: hidden;
  border: 0;
  border-left: 12px solid rgba(0, 0, 0, 0.12);
  border-radius: 11px;
  color: #3c374a;
  font-size: 18px;
}
</style>
<template>
  <div class="card align-middle box-shadow" id="Curriculum" style="height: 90vh">
    <div class="card-header"><h1>第 {{ temp_week }} 周课表</h1></div>
    <div class="table-responsive">
      <table class="table table-bordered table-hover">
        <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">周一</th>
          <th scope="col">周二</th>
          <th scope="col">周三</th>
          <th scope="col">周四</th>
          <th scope="col">周五</th>
        </tr>
        </thead>
        <tbody v-if="this.temp_week % 2 === 1">
        <tr>
          <th>01-02</th>
          <td v-for="course in courses_single[0]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>03-04</th>
          <td v-for="course in courses_single[1]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>05-06</th>
          <td v-for="course in courses_single[2]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>07-08</th>
          <td v-for="course in courses_single[3]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>09-10</th>
          <td v-for="course in courses_single[4]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        </tbody>
        <tbody v-else>
        <tr>
          <th>01-02</th>
          <td v-for="course in courses_even[0]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>03-04</th>
          <td v-for="course in courses_even[1]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>05-06</th>
          <td v-for="course in courses_even[2]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>07-08</th>
          <td v-for="course in courses_even[3]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        <tr>
          <th>09-10</th>
          <td v-for="course in courses_even[4]" :key="`${courses_single}-${course}`">
            {{course}}
          </td>
        </tr>
        </tbody>
      </table>
    </div>
    <br>
    <br>
    <div id="control-panel">
      <div id="liveAlertPlaceholder"></div>
      <BaseButton content="上周" @click.native="preWeek" style="background:#DC6561;"></BaseButton>
      <button class="btn-spin"
              @click="curWeek"
              data-content-default="回到本周"
              data-content-spinning="稍等片刻">
      </button>
      <BaseButton content="下周" @click.native="nextWeek" style="background: #94C35C"></BaseButton>
    </div>
    <br>
    <br>
    <div>
      <a href="https://cdn.jsdelivr.net/gh/Flippecho/pic@master/大二下.ics"><BaseButton content="下载 ICS 文件" style="background: #dd7694"></BaseButton></a>
      <BaseButton id="foo" class="btn" data-clipboard-target="#foo" content="复制 ICS 订阅链接" data-clipboard-text="https://cdn.jsdelivr.net/gh/Flippecho/pic@master/大二下.ics" style="background: #906c4a"></BaseButton>

    </div>
  </div>
</template>

<script>
import BaseButton from "@/components/BaseButton";
import ClipboardJS from "clipboard";

new ClipboardJS('.btn');

export default {
  name: "Curriculum",
  components: {BaseButton},
  data() {
    return {
      cur_week: 9,
      temp_week: 9,
      courses_single: [
          ["","", "Python数据处理编程@C座510","",""],
          ["人工智能@b座503", "算法分析与设计@B座505","数据库原理@B座102", "", "数据库原理@C座510"],
          ["操作系统原理@B座507", "计算机网络@B座507", "", "体育(四)", "操作系统原理@B座502"],
          ["马克思主义基本原理概论@B座413", "", "", "", "算法分析与设计@B座506"],
          ["", "", "", "敦煌的艺术", ""]
      ],
      courses_even: [
        ["","", "Python数据处理编程@C座510","计算机网络@B座508",""],
        ["人工智能@b座503", "算法分析与设计@B座505","", "", "数据库原理@C座510"],
        ["操作系统原理@B座507", "计算机网络@B座507", "", "体育(四)", ""],
        ["马克思主义基本原理概论@B座413", "", "", "", ""],
        ["", "", "", "敦煌的艺术", ""]
      ]
    }
  },
  methods: {
    curWeek() {
      this.temp_week = this.cur_week;
      this.$forceUpdate();
    },
    nextWeek() {
      this.temp_week++;
      this.$forceUpdate();
    },
    preWeek() {
      this.temp_week--;
      this.$forceUpdate();
    }
  }
}
</script>

<style scoped>
.card {
  width: 86%;
  left: 7%;
  top: 5%;
}
</style>
<template>
  <div class="card align-middle box-shadow" id="empty-classrooms" style="height: 80vh">
    <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1"
         aria-labelledby="staticBackdropLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title m-auto" id="staticBackdropLabel">第 {{ temp_week }} 周空教室</h5>
          </div>
          <div class="modal-body">
            <div class="table-responsive">
              <table class="table table-bordered table-hover">
                <thead>
                <tr>
                  <th scope="col">一楼</th>
                  <th scope="col">二楼</th>
                  <th scope="col">三楼</th>
                  <th scope="col">四楼</th>
                </tr>
                </thead>
                <tbody>
                <tr>
                  <td></td>
                  <td>202</td>
                  <td>301</td>
                  <td>413</td>
                </tr>
                <tr>
                  <td></td>
                  <td>208</td>
                  <td>306</td>
                  <td>415</td>
                </tr>
                <tr>
                  <td></td>
                  <td>221</td>
                  <td>307</td>
                  <td></td>
                </tr>
                </tbody>
              </table>
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">取消并关闭</button>
          </div>
        </div>
      </div>
    </div>
    <div class="card-header"><h1>第 {{ temp_week }} 周空教室</h1></div>
    <div class="table-responsive">
      <table class="table table-bordered table-hover">
        <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">周日</th>
          <th scope="col">周一</th>
          <th scope="col">周二</th>
          <th scope="col">周三</th>
          <th scope="col">周四</th>
          <th scope="col">周五</th>
          <th scope="col">周六</th>
        </tr>
        </thead>
        <tbody>
        <tr>
          <th>01-02</th>
          <td v-for="count in unoccupied_counts[this.temp_week][0]" :key="`${unoccupied_counts}-${count}`">
            {{ count * 4 + 1 }}
          </td>
        </tr>
        <tr>
          <th>03-04</th>
          <td v-for="count in unoccupied_counts[this.temp_week][1]" :key="`${unoccupied_counts}-${count}`"
              data-bs-toggle="modal"
              data-bs-target="#staticBackdrop">{{ count * 4 + 2 }}
          </td>
        </tr>
        <tr>
          <th>05-06</th>
          <td v-for="count in unoccupied_counts[this.temp_week][2]" :key="`${unoccupied_counts}-${count}`">
            {{ count * 4 + 3 }}
          </td>
        </tr>
        <tr>
          <th>07-08</th>
          <td v-for="count in unoccupied_counts[this.temp_week][3]" :key="`${unoccupied_counts}-${count}`">
            {{ count * 4 + 4 }}
          </td>
        </tr>
        <tr>
          <th>09-10</th>
          <td v-for="count in unoccupied_counts[this.temp_week][4]" :key="`${unoccupied_counts}-${count}`">
            {{ count * 4 + 5 }}
          </td>
        </tr>
        </tbody>
      </table>
    </div>
    <br>
    <br>
    <div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1" value="option1">
        <label class="form-check-label" for="inlineRadio1">A座</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2" value="option2">
        <label class="form-check-label" for="inlineRadio2">B座</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio3" value="option1">
        <label class="form-check-label" for="inlineRadio1">C座</label>
      </div>
      <div class="form-check form-check-inline">
        <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio4" value="option2">
        <label class="form-check-label" for="inlineRadio2">D座</label>
      </div>
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
  </div>
</template>

<script>
import BaseButton from "@/components/BaseButton";

export default {
  name: "EmptyClassrooms",
  components: {BaseButton},
  data() {
    return {
      cur_week: 9,
      temp_week: 9,
      unoccupied_counts: [
        [],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]],
        [[68, 24, 22, 14, 16, 19, 68], [68, 14, 15, 10, 8, 14, 66], [69, 18, 17, 61, 21, 23, 66], [68, 19, 18, 62, 24, 22, 66], [69, 30, 28, 33, 41, 36, 69]]
      ],
      unoccupied_A: [[[[101, 102, 103, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [113, 115, 123, 202, 203, 208, 210, 211, 212, 213, 214, 215, 217, 219, 220, 222, 306, 307, 313, 410, 412, 413, 415, 419], [111, 124, 202, 207, 208, 210, 212, 213, 217, 218, 220, 302, 303, 306, 307, 323, 324, 412, 413, 415, 417, 419], [202, 207, 208, 210, 212, 217, 302, 304, 322, 323, 324, 411, 413, 415], [103, 111, 113, 115, 124, 210, 217, 218, 219, 220, 306, 307, 313, 412, 413, 415], [114, 210, 212, 213, 217, 220, 301, 302, 303, 306, 307, 315, 323, 324, 411, 413, 415, 417, 419], [102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421]], [[101, 102, 103, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [113, 203, 207, 208, 210, 213, 214, 215, 306, 307, 412, 413, 419, 420], [203, 208, 210, 212, 214, 302, 303, 306, 307, 323, 324, 410, 412, 413, 415], [204, 208, 210, 302, 323, 324, 401, 413, 419, 421], [202, 208, 221, 301, 306, 307, 413, 415], [208, 210, 217, 302, 303, 304, 306, 307, 323, 324, 413, 415, 417, 419], [102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421]], [[101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [115, 207, 208, 210, 212, 217, 221, 302, 303, 323, 324, 404, 411, 412, 413, 415, 417, 420], [112, 113, 202, 203, 206, 207, 208, 210, 211, 217, 221, 302, 303, 323, 411, 413, 420], [103, 104, 110, 111, 112, 113, 114, 115, 119, 122, 123, 124, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 311, 312, 313, 314, 315, 317, 318, 319, 320, 322, 323, 324, 401, 404, 410, 412, 413, 415, 417, 419, 420, 421], [113, 114, 115, 202, 207, 208, 210, 214, 220, 223, 301, 302, 303, 306, 307, 323, 324, 401, 412, 413, 415], [111, 114, 202, 203, 206, 208, 211, 218, 219, 302, 303, 306, 307, 323, 324, 401, 410, 411, 412, 413, 415, 417, 421], [101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 415, 417, 419]], [[101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [202, 206, 207, 208, 210, 217, 218, 302, 303, 304, 306, 307, 323, 324, 404, 410, 413, 415, 419], [108, 202, 206, 208, 210, 217, 218, 219, 221, 302, 303, 318, 320, 323, 411, 413, 415, 421], [103, 108, 111, 112, 113, 114, 115, 117, 119, 123, 124, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [111, 115, 119, 202, 207, 208, 210, 211, 212, 215, 217, 219, 223, 302, 303, 306, 307, 323, 324, 404, 410, 411, 412, 413], [115, 202, 203, 207, 208, 210, 218, 219, 220, 224, 302, 303, 304, 321, 323, 324, 411, 412, 413, 415, 420, 421], [101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 415, 417, 419]], [[101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421], [112, 113, 114, 115, 202, 207, 208, 210, 211, 212, 214, 215, 217, 218, 220, 302, 303, 306, 307, 321, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417], [112, 113, 114, 115, 122, 201, 202, 206, 207, 208, 211, 213, 214, 218, 219, 220, 301, 302, 303, 306, 307, 323, 324, 401, 411, 412, 413, 415], [110, 111, 112, 113, 114, 202, 203, 206, 207, 208, 210, 211, 212, 217, 218, 219, 223, 301, 302, 303, 306, 307, 312, 323, 324, 404, 410, 411, 412, 413, 415, 417, 419], [102, 103, 115, 123, 124, 202, 203, 206, 207, 208, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 302, 303, 306, 307, 311, 312, 315, 319, 321, 322, 323, 324, 401, 404, 410, 412, 413, 415, 419, 421], [108, 111, 112, 113, 114, 201, 202, 203, 207, 208, 210, 213, 214, 215, 217, 218, 220, 221, 224, 302, 303, 304, 306, 307, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 421], [101, 102, 103, 104, 108, 110, 111, 112, 113, 114, 115, 117, 119, 122, 123, 124, 201, 202, 203, 204, 206, 207, 208, 210, 211, 212, 213, 214, 215, 217, 218, 219, 220, 221, 222, 223, 224, 301, 302, 303, 304, 306, 307, 308, 310, 311, 312, 313, 314, 315, 317, 318, 319, 320, 321, 322, 323, 324, 401, 404, 410, 411, 412, 413, 415, 417, 419, 420, 421]]]]
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
  width: 80%;
  left: 10%;
  top: 10%;
}
</style>
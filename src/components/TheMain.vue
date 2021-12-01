<template>
  <div class="card align-middle box-shadow">
    <div class="card-header"><h1>主要内容页面</h1></div>
  </div>
</template>

<script>

export default {
  name: "TheMain",
}
</script>

<style scoped>
.card {
  float: right;
  width: 60vw;
  right: 5vw;
  height: 80vh;
  top: 5vh;
}

#control-panel {
  margin-top: 1em;
  margin-bottom: 1em;
}

td {
  font-size: 21px;
  color: #515151;
  white-space: nowrap;
  overflow: auto;
}

td > span {
  font-size: 11px;
  display: inline-block;
}
</style>
<template>
  <div id="entrance">
    <ul class="card-stacks grid swipe-right" id="grid">
      <li class="stack stack-1">
        <ul class="cards-down">
          <li class="card card-2"><img src="img/05.jpg"/>
            <div class="content">
              <h1>怀旧人</h1>
              <p>归档</p>
            </div>
          </li>
          <li class="card card-3"><img src="img/09.jpg"/>
            <div class="content">
              <h1>拖延人</h1>
              <p>所有通知</p>
            </div>
          </li>
        </ul>
      </li>
      <li class="stack stack-2">
        <ul class="cards-down">
          <li class="card card-2"><img src="img/04.jpg"/>
            <div class="content">
              <h1>从容人</h1>
              <p>重要但不紧急</p>
            </div>
          </li>
          <li class="card card-3"><img src="img/03.jpg"/>
            <div class="content">
              <h1>压力人</h1>
              <p>重要且紧急</p>
            </div>
          </li>
        </ul>
      </li>
      <li class="stack stack-3">
        <ul class="cards-down">
          <li class="card card-2"><img src="img/08.jpg"/>
            <div class="content">
              <h1>无用人</h1>
              <p>不重要不紧急</p>
            </div>
          </li>
          <li class="card card-3"><img src="img/01.jpg"/>
            <div class="content">
              <h1>工具人</h1>
              <p>紧急但不重要</p>
            </div>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "TheContentEntrance"
}
</script>

<style scoped>

</style>
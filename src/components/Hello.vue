<template>
  <p>{{greeting}} World!</p>
</template>

<script>
export default {
  name: "Hello",
  data: function () {
    return {
      greeting: 'Hello'
    }
  }
}
</script>

<style scoped>
p {
  font-size: 2em;
  text-align: center;
}
</style>
<template>
  <li>
    {{ title }}
    <button @click="$emit('remove')">Remove</button>
  </li>
</template>

<script>
export default {
  name: "TodoListItem",
  props: ['title'],
  emits: ['remove']
}
</script>

<style scoped>

</style>
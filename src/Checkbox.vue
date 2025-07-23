<template>
  <label>
    <input type="checkbox" @change="onChange" />
    {{ label }}
  </label>
</template>

<script setup>
const model = defineModel()
defineProps({
  label: String,
})
const emits = defineEmits(['check', 'uncheck'])
const onChange = (event) => {
  if (event.currentTarget.checked) {
    emits('check', event.currentTarget)
  } else {
    emits('uncheck', event.currentTarget)
  }
}
</script>
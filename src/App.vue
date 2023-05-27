<template>
  <template v-if="markup">
    <MarkupComponent :element="markup" />
  </template>
</template>
<script setup lang="ts">
import { ref, onMounted } from 'vue'
import MarkupComponent from './components/MarkupComponent.vue'
const markup = ref({})
onMounted(() => {
  fetchData()
})
const fetchData = async() => {
  try {
    const response = await fetch(
      'https://raw.githubusercontent.com/JasonWandrag/website-builder/main/templates/default_template.json'
    )
    if (response.ok) {
      const markupObject = await response.json()
      markup.value = markupObject 
    } else {
      console.error('Error:', response.statusText)
    }
  } catch (error) {
    console.error('Error:', error)
  }
}
</script>

<template>
  <div v-if="contentIsPrimitive">
      {{ itemKey }} : {{ itemContent }}
  </div>

  <div v-else-if="!contentIsArray">
    <TreeTest
      v-for="(itemKey, index) in Object.keys(itemContent)"
      :key="index"
      :itemKey="itemKey"
      :itemContent="itemContent[itemKey]"
    />
  </div>

  <div v-else>
    <TreeTest
      v-for="(viewItem, index) in itemContent"
      :key="index"
      :itemContent="viewItem"
    />
  </div>
</template>

<script setup>
import { computed } from 'vue';


const props = defineProps({
  itemKey: {
    type: String,
    default: ""
  },
  itemContent: {
    default: null
  }
});

const contentIsArray = computed(() => {
  return Array.isArray(props.itemContent)
})

const contentIsObject = computed(() => {
  return (props.itemContent !== null && typeof props.itemContent === 'object')
})

const contentIsPrimitive = computed(() => {
  return !(contentIsArray.value || contentIsObject.value)
})

</script>
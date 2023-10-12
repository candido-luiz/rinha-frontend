<template>
  
    <li v-if="contentIsPrimitive">
        {{ contentText }}
    </li>

    <li v-else-if="!contentIsArray">
        {{ itemKey }}
        <ul>
          <TreeTest
            v-for="(itemKey, index) in Object.keys(itemContent)"
            :key="index"
            :itemKey="itemKey"
            :itemContent="itemContent[itemKey]"
          />
        </ul>
    </li>

    <ul v-else>
      
        <TreeTest
          v-for="(viewItem, index) in itemContent"
          :key="index"
          :itemContent="viewItem"
          :itemIndex="index"
        />
    </ul>
  
</template>

<script setup>
import { computed, defineComponent } from 'vue';

defineComponent({
  name: "TreeTeste"
})
const props = defineProps({
  itemKey: {
    type: String,
    default: ""
  },
  itemContent: {
    default: null
  },
  itemIndex: {
    type: Number,
    default: 0
  },
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

const contentText = computed(() => {
  if(contentIsPrimitive.value) {
    return props.itemKey ? `${props.itemKey}: ${props.itemContent}` : `${props.itemContent}`
  }
  return ""
})

</script>
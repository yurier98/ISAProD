<script setup lang="ts">
import uiColors from '#ui-colors'

const props = defineProps({
  title: { type: String },
  icon: { type: String },
  color: { type: String as PropType<(typeof uiColors)[number]> },
  to: { type: String }
})

const target = computed(() => (props.to?.startsWith('https://') ? '_blank' : ''))
</script>

<template>
  <Callout :icon="icon" :color="color" :to="to" :target="target" class="font-medium">
    <ContentSlot :use="$slots.default" unwrap="p" />
  </Callout>
</template>

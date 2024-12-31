<script setup lang="ts">
import type {NavItem} from '@nuxt/content'

const links = computed(() => headerLinks.value.find(link => link.to === '/docs')?.children ?? [])

const navigation = inject<Ref<NavItem[]>>('navigation')

const navigationLinks = computed(() => {
  const path = ['/docs', route.params.slug?.[0]].filter(Boolean).join('/')

  return mapContentNavigation(navPageFromPath(path, navigation.value)?.children || [])
})

</script>

<template>
  <UContainer>
    <UPage>
      <template #left>
        <UAside>
          <UNavigationTree :links="mapContentNavigation(navigation)" :multiple="false" class="pb-10"/>
        </UAside>
      </template>

      <slot/>
    </UPage>
  </UContainer>
</template>

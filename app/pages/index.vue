<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryContent('/').findOne())

useSeoMeta({
  titleTemplate: '%s · Home',
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description
})
</script>

<template>
  <div>
    <ULandingHero
      v-if="page.hero"
      v-bind="page.hero"
    >
      <template #headline>
        <UBadge
          v-if="page.hero.headline"
          variant="subtle"
          size="lg"
          class="relative rounded-full font-semibold"
        >
          <NuxtLink
            :to="page.hero.headline.to"
            target="_blank"
            class="focus:outline-none"
            tabindex="-1"
          >
            <span
              class="absolute inset-0"
              aria-hidden="true"
            />
          </NuxtLink>

          {{ page.hero.headline.label }}

          <UIcon
            v-if="page.hero.headline.icon"
            :name="page.hero.headline.icon"
            class="ml-1 w-4 h-4 pointer-events-none"
          />
        </UBadge>
      </template>

      <template #title>
        <div class="text-5xl">
          <MDC :value="page.hero.title" />
        </div>
      </template>

      <ClientOnly>
        <video
          ref="/1.mp4"
          autoplay
          loop
          muted
          class="w-full rounded-xl shadow-xl ring-1 ring-gray-300 dark:ring-gray-700"
        >
          <source
            src="/2.mp4"
            type="video/mp4"
          >
          Your browser does not support the video tag.
        </video>
      </ClientOnly>
    </ULandingHero>

    <ULandingSection
      :title="page.features.title"
      :links="page.features.links"
      :description="page.features.description"
    >
      <UPageGrid>
        <ULandingCard
          v-for="(item, index) of page.features.items"
          :key="index"
          v-bind="item"
        />
      </UPageGrid>
    </ULandingSection>

    <ULandingSection
      v-for="(section, index) in page.sections"
      :key="index"
      :title="section.title"
      :description="section.description"
      :align="section.align"
      :features="section.features"
    >
      <template #title>
        <div class="text-5xl">
          <span v-html="section.title" />
        </div>
      </template>

      <ClientOnly>
        <video
          v-if="section.video"
          ref="/1.mp4"
          :src="section.video"
          autoplay
          loop
          muted
          class="w-full rounded-xl shadow-xl ring-1 ring-gray-300 dark:ring-gray-700"
        >
          <source
            v-if="section.video"
            :src="section.video"
            type="video/mp4"
          >
          Your browser does not support the video tag.
        </video>
      </ClientOnly>

      <img
        v-if="section.image"
        :src="section.image"
        class="w-full rounded-xl shadow-xl ring-1 ring-gray-300 dark:ring-gray-700"
      >
    </ULandingSection>

    <div id="experts">
      <ULandingSection
        :title="page.experts.title"
        :description="page.experts.description"
      >
        <UPageGrid>
          <ExpertCard
            v-for="(item, index) in page.experts.members"
            :key="index"
            v-bind="item"
          />
        </UPageGrid>
      </ULandingSection>
    </div>

    <ULandingSection
      :title="page.faq.title"
      :description="page.faq.description"
    >
      <ULandingFAQ
        :items="page.faq.items"
        multiple
        class="max-w-4xl mx-auto"
      />
      <ULandingCTA
        v-bind="page.cta"
        class="bg-gray-100/50 dark:bg-gray-800/50"
      />
    </ULandingSection>
  </div>
</template>

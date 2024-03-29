<script lang="ts" setup>
// Components
  import { vElementVisibility } from '@vueuse/components'
  import BaseNextSection from './common/BaseNextSection.vue'
  import BaseBtn from './common/BaseBtn.vue'
  import TheSignature from './features/TheSignature.vue'
  import TheQuote from './features/TheQuote.vue'

  // Composables
  import { useVisibility } from '../composables/useVisibility'

  const [isTextBlockVisible, onTextBlockVisibility] = useVisibility()
  const [isLinkVisible, onLinkVisibility] = useVisibility()

  // calculate current age
  const birthDate = new Date('1990-04-21') 
  const currentDate = new Date()
  const diffInMilliseconds = currentDate.getTime() - birthDate.getTime()
  const ageInMilliseconds = new Date(diffInMilliseconds)

  // Subtract 1970 since that's the epoch year
  const currentAge = Math.abs(ageInMilliseconds.getUTCFullYear() - 1970)
</script>

<template>
  <section class="tw-relative tw-mx-auto">
    <TheQuote />

    <div
      v-element-visibility="onTextBlockVisibility"
      :class="{
        'animate__animated animate__fadeIn animate__delay-1s': isTextBlockVisible,
        'tw-will-change': isTextBlockVisible,
      }"
      class="tw-container tw-flex tw-flex-row xl:tw-mx-0 xl:tw-max-w-none xl:tw-justify-end xl:tw-pr-20 2xl:tw-pr-[15%]"
    >
      <div class="tw-my-12 md:tw-my-10 xl:tw-my-20 xl:tw-w-3/5 2xl:tw-w-1/2">
        <p
          class="tw-text-sm tw-font-semibold tw-uppercase tw-text-indigo-400 dark:tw-text-indigo-400 xl:tw-text-l"
        >
          Laura,
          {{ $t('about.pronouns') }}
          &middot; {{ currentAge }} &middot;
          {{ $t('general.location') }}
        </p>
        <div class="tw-hyphens-auto tw-text-justify">
          <p class="tw-my-6">
            <span class="tw-text-m tw-font-semibold dark:tw-text-indigo-100 sm:tw-text-l md:tw-text-xl">
              {{ $t('about.tldr') }}
            </span>
          </p>
          <p>
            {{ $t('about.text1') }}
            <br><br>
            {{ $t('about.text2') }}
          </p>
          <TheSignature
            id="signature"
            class="tw-relative tw-inline-block tw-w-2/3 tw-fill-none tw-stroke-white tw-pt-10 sm:tw-w-1/3"
          />
        </div>
      </div>
    </div>

    <div
      ref="link"
      v-element-visibility="onLinkVisibility"
      :class="{
        'animate__animated animate__fadeInUp animate__delay-2s': isLinkVisible,
        'tw-will-change': isLinkVisible,
      }"
      class="tw-container tw-mb-20 tw-text-center md:tw-mb-32 xl:tw-absolute xl:-tw-bottom-10 xl:-tw-left-40 xl:tw-mx-5 xl:tw-w-auto xl:tw-px-0"
    >
      <div
        class="tw-hidden tw-justify-center tw-rounded-full tw-py-4 tw-align-middle tw-transition-all xl:tw-m-16 xl:tw-flex xl:tw-h-96 xl:tw-w-96 2xl:tw-px-16"
      >
        <router-link
          to="/vita"
          class="tw-flex-column tw-left-0 tw-top-0 tw-flex tw-h-full tw-flex-col tw-justify-end tw-rounded-full tw-border-4 tw-border-indigo-700 tw-bg-indigo-700 tw-px-10 tw-py-3 tw-align-middle tw-transition-all focus-visible:tw-outline-none focus-visible:tw-ring-4 focus-visible:tw-ring-purple-500 dark:tw-text-purple-200 dark:hover:tw-text-white md:tw-py-4 xl:tw-absolute xl:tw-w-full xl:tw-border-[240px] xl:tw-border-amber-500 xl:tw-bg-transparent xl:tw-px-0 xl:tw-text-indigo-800 xl:hover:tw-border-[90px] xl:hover:tw-border-amber-500 xl:hover:tw-bg-indigo-600 xl:hover:tw-text-white xl:dark:tw-border-indigo-900"
        >
          <span
            class="tw-flex tw-flex-row tw-items-center tw-justify-center tw-font-semibold xl:tw-block xl:tw-px-40 xl:tw-text-2xl xl:tw-font-bold xl:tw-uppercase xl:tw-leading-tight xl:tw-tracking-widest"
          >
            <span>
              {{ $t('about.vita') }}
            </span>
            <wbr>
            <span
              aria-hidden="true"
              class="tw-i-ph-arrow-right-bold tw-ml-2 tw-inline-block xl:tw-ml-0 xl:tw-mt-3 xl:tw-h-8 xl:tw-w-8"
            />
          </span>
        </router-link>
      </div>

      <div class="tw-inline-block xl:tw-hidden">
        <BaseBtn
          :has-arrow="true"
          :text="$t('about.vita')"
          to="/vita"
        />
      </div>
    </div>

    <BaseNextSection
      container-class="tw-block md:tw-mt-40"
      target="#expertise"
      :title="$t('nav.skills-long')"
    />
  </section>
</template>

<template>
  <div>
    <section class="min-h-screen md:min-h-750 bg-work flex flex-col justify-center items-center">
      <h1 class="text-center text-4xl md:text-6xl font-normal text-rains-lighter capitalize mt-16 md:mt-32 mb-4 md:mb-0">
        {{ $t('work.index.heading') }}
      </h1>
      <h2 class="font-normal text-center text-rains-lighter text-xl md:text-3xl w-4/5">
        {{ $t('work.index.subheading') }}
      </h2>
    </section>
    <div class="flex flex-wrap justify-center">
      <work-preview
        v-for="(info, i) in $options.projects"
        :key="i"
        :odd="!!(i % 2)"
        v-bind="info"/>
    </div>
    <div class="bg-white shadow w-full py-32 flex flex-col items-center">
      <h3 class="text-2xl text-center">{{ $t('work.appendix.heading') }}</h3>
      <p class="w-full md:w-1/2 p-8 md:p-3">{{ $t('work.appendix.subheading') }}</p>
      <div class="w-full md:w-3/4 flex flex-col lg:flex-row items-center lg:justify-around mt-16">
        <div
          v-observe-visibility="!i ? handleVisibility : () => {}"
          v-for="({duration, to, prefix}, i) in $options.numbers"
          :key="i"
          class="my-8 lg:my-0 mx-4 text-xl">
          <animated-number
            :duration="duration"
            :should-start="isVisible"
            :to="to"
            class="text-2xl font-bold"/>
          <span>{{ prefix }} {{ $t('work.appendix.statistics')[i] }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { deterministicRotate } from '~/shared/helpers'
import WorkPreview from '~/components/work/WorkPreview'

export default {
  scrollToTop: true,
  components: {
    WorkPreview,
    AnimatedNumber: () => import('~/components/work/AnimatedNumber')
  },
  data() {
    return {
      isVisible: false
    }
  },
  methods: {
    handleVisibility(isVisible) {
      if (isVisible) {
        this.isVisible = true
      }
    }
  },
  projects: deterministicRotate([
    {
      slug: 'addism',
      url: 'https://addism.de/'
    },
    {
      slug: 'itexia',
      url: 'https://itexia.com/'
    },
    {
      slug: 'hid',
      url: 'https://hochschulinitiative-deutschland.de/'
    },
    {
      slug: 'lichter-io',
      url: 'https://lichter.io/'
    },
    {
      slug: 'nuxt',
      url: 'https://nuxtjs.org/',
      svg: () => import('~/assets/img/work/nuxt.svg')
    },
    {
      slug: 'ostseeferien-binz',
      url: 'https://ostseeferien-binz.de/'
    },
    {
      slug: 'association-manager',
      url: ''
    }
  ]),
  numbers: [
    {
      duration: 1000,
      to: 30,
      prefix: '+'
    },
    {
      duration: 3500,
      to: 100000,
      prefix: '+'
    },
    {
      duration: 2500,
      to: 100,
      prefix: '%'
    }
  ],
  head() {
    return this.$createSeo('work')
  }
}
</script>

<style lang="scss">
  .bg-work {
    background-size: cover;
    background-image: linear-gradient(config('colors.rains-dark'), rgba(11, 7, 16, 0.6)), url("~assets/img/bg/work_sm.jpg");
    background-position: bottom;
    @screen md {
      background-image: linear-gradient(config('colors.rains-dark'), rgba(11, 7, 16, 0.6)), url("~assets/img/bg/work.jpg");
      background-position: center;
    }
  }
</style>

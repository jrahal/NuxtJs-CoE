<template lang="pug">
doctype
#MetroStack
  .inner
<<<<<<< HEAD
    VertBorder
    .title(v-in-viewport) Barriers to New Apartments
    .copy(v-in-viewport) Based on specific factors like local regulations and available land to develop, the Barriers to Apartment Construction Index ranks 50 metro areas on how hard it is to build new apartments. See how your city stacks up. 
    .copy2(v-in-viewport) Multifamily supply restrictions index
    HeatChart(v-if="choice.type === 'metro'",:metro="this.choice.value")
    .copy3.has-text-centered(v-if="choice.type === 'metro'") {{ choice.value }}
=======
    .title(v-in-viewport) Stacking up the Metros
    .copy(v-in-viewport) Based on specific factors like local regulations and available land to develop, the Barriers to Apartment Construction Index ranks 50 metro areas on how hard it is to add new apartments. See how your city stacks up.  Barriers to Apartment Construction Index is a HAS composite of methodology using the Wharton Residential Land Use Restrictions Index overall and the portion of it based on only the developable land sub-index. This index ranges from 19.5 (Honolulu, most difficult to build) to –6.0 (New Orleans, easiest to build) with a Metro average of 2.0.
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
    .metros(v-in-viewport)
      .list
        .metro(v-for="value, key in metros")
          i-count-up.value(:start=0,:end="metros[key]", :class="{ value_grey: loading === true, value_red: value > 5.0, value_orange: value < 5.0 && value > 1.6, value_green: value <= 1.6 }")
          router-link.name(:to="'/data/metro/' + key.trim().toLowerCase().replace(/ /g, '-')") {{ key }}
</template>

<script>
import restrictIndex from '~/static/Metro Restriction Index.json'
import ICountUp from 'vue-countup-v2'
import inViewportDirective from 'vue-in-viewport-directive'
import inViewport from 'vue-in-viewport-mixin'
import VertBorder from '~/components/VertBorder'
import HeatChart from '~/components/HeatChart'
export default {
  props: [ 'choice' ],
  components: { ICountUp, VertBorder, HeatChart },
  directives: { 'in-viewport': inViewportDirective },
  mixins: [ inViewport ],
  methods: {
    sort (object) {
      let sortable = []
      let sorted = {}
      for (let key in object) {
        sortable.push([key, object[key]])
      }
      sortable.sort((a, b) => {
        return b[1] - a[1]
      })
      for (let key in sortable) {
        sorted[sortable[key][0]] = object[sortable[key][0]]
      }
      return sorted
    },
    populate () {
      this.loading = false
      let sorted = this.sort(restrictIndex.data)
      for (let key in sorted) {
        this.metros[key] = Number(sorted[key].toFixed(2))
      }
    },
    zeros () {
      this.loading = true
      let sorted = this.sort(restrictIndex.data)
      for (let key in sorted) {
        this.metros[key] = 0
      }
    }
  },
  created () {
    if (this.browser) {
      this.zeros()
    } else {
      this.populate()
    }
  },
  watch: {
    'inViewport.now' (visible) {
      if (!this.browser) {
        return true
      }
      if (visible) {
        setTimeout(() => {
          this.populate()
        }, 1000)
      } else {
        this.zeros()
      }
    }
  },
  data () {
    return {
      metros: this.sort(restrictIndex.data),
      end: 0,
      loading: true,
      browser: process.BROWSER_BUILD,
    }
  }
}
</script>

<style lang="stylus">
json('../assets/colors.json')
json('../assets/fonts.json')
#MetroStack
  padding 90px 0
  > .inner
    > .title
      font h1
      text-align center
      padding 30px 0 0 0
      &.below-viewport
        opacity 0
        transform translate(0, 20px)
      &.in-viewport
        opacity 1
        transform translate(0, 0)
        transition opacity 1s ease-in-out 0s, transform 1s ease-in-out 0s
    > .copy
      text-align center
      color grey
      width 560px
      margin auto
      padding 30px 0 0 0
      &.below-viewport
        opacity 0
        transform translate(0, 20px)
      &.in-viewport
        opacity 1
        transform translate(0, 0)
        transition opacity 1s ease-in-out 0.1s, transform 1s ease-in-out 0.1s
    > .copy2
      font c1b
      text-transform uppercase
      text-align center
      padding 30px 0
      &.below-viewport
        opacity 0
        transform translate(0, 20px)
      &.in-viewport
        opacity 1
        transform translate(0, 0)
        transition opacity 1s ease-in-out 0.1s, transform 1s ease-in-out 0.1s
    > .metros
      width 900px
      margin auto
      padding-top 60px
      &.below-viewport
        opacity 0
        transform translate(0, 20px)
      &.in-viewport
        opacity 1
        transform translate(0, 0)
        transition opacity 1s ease-in-out 0s, transform 1s ease-in-out 0s
      > .list
        column-count 4
        column-gap 30px
        > .metro
          > .value
            float left
            width 50px
            font c1b
            transition color 1s linear 0s
            &.value_red
              color red
            &.value_orange
              color orange
            &.value_green
              color green
            &.value_grey
              color grey !important
          > .name
            color black
            text-decoration none
            transition color 0.1s ease 0s, text-decoration 0.1s ease 0.05s
            &:hover
              color blue
              text-decoration underline
@media all and (min-width: 1px) and (max-width: 1000px)
  #MetroStack
    padding 60px 20px
    > .inner
      > .copy
        width auto
      > .metros
        width auto
        > .copy
          font c1sb
        > .list
          column-count 2
          column-gap 16px
          > .metro
            > .name, > .value
              font c1s
</style>

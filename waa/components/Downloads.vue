<template lang="pug">
doctype
#Downloads
  .blackline
  .inner
    .block.left
      .inner
        .copy The Report
        .copy NMHC and NAA partnered with Hoyt Advisory Services to identify the demand for apartments through 2030. Download their analysis of the apartment industry.
<<<<<<< HEAD
        a.cta(href="/NMHC-NAA-US-Apartment-Demand-in-2030.pdf") download
=======
        a.cta(href="/NMHC-NAA-US-Apartment-Demand-in-2030.pdf",v-in-viewport) download
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
    .block.right
      .inner
        .copy A vision for 2030
        .copy Meeting the country's demand for apartments will take courageous steps at the federal, state and local levels. 
<<<<<<< HEAD
        //router-link(to='/about',v-if="$route.name !== 'about'").cta learn more
        a.cta(href="/Vision2030.pdf") Download
</template>
=======
        router-link(to='/about',v-if="$route.name !== 'about'",v-in-viewport).cta learn more
        a.cta(href="/Vision2030.pdf",v-if="$route.name === 'about'",v-in-viewport) Download
</template>

>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
<style lang="stylus">
json('../assets/colors.json')
json('../assets/fonts.json')
@import '../assets/stylus/mixins.styl'
#Downloads
  background-color purple
  position relative
  > .blackline
    position absolute
    width 3px
    height 60px
    background-color black
    top -30px
    left 50%

  > .inner
    width 900px
    margin auto
    padding 90px 0
    color white
    column-count 2
    column-span 2
    column-gap 0
    > .block
      padding 60px
      break-inside avoid-column
      page-break-inside avoid
      display table
      &:nth-child(2)
        background-color royalpurple
        border-radius 3px
        > .inner
          > .copy:nth-child(2)
            padding 60px 0
          > .cta
            z-index 100
            color white
            text-transform uppercase
      &:nth-child(1)
        > .inner > .cta
          z-index 100
          background-color blue
          color white
          padding 15px 40px
          border-radius 3px
          float left
          text-transform uppercase
          font c1b
          text-decoration none
<<<<<<< HEAD
          &:hover
            text-decoration underline
=======
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
      > .inner
        > .copy:nth-child(1)
          font h1
        > .copy:nth-child(2)
          padding 30px 0 60px 0
          width 300px
@media all and (min-width: 1px) and (max-width: 1000px)
  #Downloads
    > .inner
      width auto
      column-count 1
      column-span 0
      > .block
        margin auto


</style>

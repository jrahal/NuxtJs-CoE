
<template lang="pug">
doctype
<<<<<<< HEAD
p(v-in-viewport)  Between now and 2030, 

  span(v-if="type === 'national'") the country will need to build 
    span {{ needed }} 
    | new apartment homes each year to accomodate household growth and losses to the stock. 
  span(v-else) {{ value }} will need to build 
    span {{ needed }} 
    | new apartment homes each year to accomodate household growth and losses to the stock. 
  //span(v-if="type === 'state'") this state will add 
    span {{ needed }} 
    | new apartment homes each year to meet demand 
  //span(v-if="type === 'metro'") this metro will add 
    span {{ needed }} 
    | new apartment homes each year to meet demand 
  //span(v-if="type === 'district'") this district will add 
    span {{ needed }} 
    | new apartment homes each year to meet demand 
    //| However, new housing approaches are needed as only an average of {{ needed }} apartment homes were built each year between 2011 - 2016.
  | However, producing enough new apartments to meet demand may require new development approaches, more incentives and fewer restrictions
=======
p(v-in-viewport) New research shows that demand for apartments is on the rise.  Whether it's young professionals, couples, families or empty nesters, 
  span(v-if="type === 'national'") the country will see a demand for an additional 
    span {{ households }} 
    | new apartment homes 
    span by 2030
  span(v-if="type === 'state'") this state will need to add 
    span {{ households }} 
    | new apartment homes 
    span by 2030
  span(v-if="type === 'metro'") this metro will need to add 
    span {{ households }} 
    | new apartment homes 
    span by 2030
  span(v-if="type === 'district'") this district will need to add 
    span {{ households }} 
    | new apartment homes 
    span by 2030
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
</template>

<script>
import inViewportDirective from 'vue-in-viewport-directive'
import numeral from 'numeraljs'
export default {
  directives: { 'in-viewport': inViewportDirective },
  props: [ 'type', 'value' ],
  methods: {
    populate () {

      let json = {}
      let index = false
      // const numeral = window.numeral

      switch (true) {

        case (this.type === 'national'):
          json = require('../static/US Building.json').data
          this.needed = numeral(json['Total U.S.'][1]).format('0,0a')
          break
        case (this.type === 'state'):
          json = require('../static/State Building Units.json')
          this.needed = numeral(json.data[this.value][1]).format('0,0')
          break
        case (this.type === 'metro'):
          json = require('../static/Metro Supply.json')
          this.needed = numeral(json.data[this.value][1]).format('0,0')
          break
      }

    }
  },
  mounted () {
    this.populate()
  },
  watch: {
    '$route' () {
      this.populate()
    }
  },
  data () {
    this.populate()
    if (this.type === 'state') {
      return {
        title: this.value + ' - Learn about the demand for apartments in your area',
        description: 'The state of ' + this.value + ' will see a demand for an additional ' + this.households + ' new apartment homes by 2030',
<<<<<<< HEAD
        households: 0,
        needed: 0,
=======
        households: 0
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
      }
    }
    if (this.type === 'metro') {
      return {
        title: this.value + ' - Learn about the demand for apartments in your area',
        description: this.value + ' will see a demand for an additional ' + this.households + ' new apartment homes by 2030',
<<<<<<< HEAD
        households: 0,
        needed: 0,
=======
        households: 0
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
      }
    }
    return {
      title: 'Learn about the demand for apartments in your area',
      description: 'This country will see a demand for an additional ' + this.households + ' new apartment homes by 2030',
<<<<<<< HEAD
      households: 0,
      needed: 0,
=======
      households: 0
>>>>>>> 550970a855e4035d4412ce1b08f9dea667f388e1
    }
  },
  head () {
    return {
      title: this.title,
      meta: [
        { hid: 'description', name: 'description', content: this.description },
        { hid: 'og:url', property: 'og:url', content: this.$route.path },
        { hid: 'og:title', property: 'og:title', content: this.title },
        { hid: 'og:description', property: 'og:description', content: this.description },
        { hid: 'twitter:title', name: 'twitter:title', content: this.title },
        { hid: 'twitter:description', name: 'twitter:description', content: this.description },
      ]
    }
  },
}

</script>

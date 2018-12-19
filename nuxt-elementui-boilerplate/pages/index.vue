<template>
  <div>
    <navi/>
    <carou/>
    <el-button type="primary">Primary Button</el-button>
  </div>
</template>

<script>
  import navi from '@/components/navi'
  import carou from '@/components/carou'
  import { Button } from 'element-ui'

  export default {
    components: {
      navi,
      carou,
      'el-button': Button
    }
  }

</script>


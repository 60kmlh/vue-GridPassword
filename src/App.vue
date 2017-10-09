<template>
  <div id="app">
    <GridPassword :onConfirm='onConfirm' :passwordLength='5' :isPassword='true'></GridPassword>
  </div>
</template>

<script>
import GridPassword from '@/components/GridPassword'

export default {
  name: 'app',
  data() {
    return {
      onConfirm: (e) => {
        console.log(e);
      },
      isBtn: false
    }
  },
  components: {
    GridPassword
  }
}
</script>

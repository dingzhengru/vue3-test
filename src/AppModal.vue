<template>
  <div style="border: 1px solid #ccc; width: 300px; height: 100px;">
    <slot name="content">
      <span>default content</span>
    </slot>

    <p>not in slot</p>
    
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'AppModal',
  props: {
    
  },
  setup(props) {
    
  }
}
</script>

<style scoped>

::v-slotted(p) {
  color: red;
  font-weight: bold;
}

</style>

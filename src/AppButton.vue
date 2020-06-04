<template>
  <button @click="buttonClickHandler">{{ text }}</button>
  {{ count }}
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'AppButton',
  props: {
    text: {
      type: String,
      default: () => 'DefaultText'
    }
  },
  emits: {
    clickCount: payload => { // 此處可以認證資料，正確就回傳 true，讓事件傳遞出去
      console.log('trigger: clickCount');
      return true;
    }
  },
  setup(props, { emit, root }) {
    const count = ref(0);
    const buttonClickHandler = () => {
      count.value++;
      emit('clickCount', count.value);
    };

    return {
      count,
      buttonClickHandler
    };
  }
}
</script>

<style scoped>

</style>

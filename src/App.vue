<template>
  <h1>Hello Vue 3!</h1>

  <hr>
  <h2>AppButton</h2>
  <button @click="appButtonText=appButtonText + '0'">add appButtonText</button>
  <AppButton
    :text.sync="appButtonText"
    @clickCount="appButtonCount"
  />

  <hr>
  <h2>Teleport</h2>
  
  <button @click="teleportDestination == '#teleport-01' ? teleportDestination = '#teleport-02' : teleportDestination = '#teleport-01'">
    改變傳送地點
  </button>

  <div id="teleport-01"></div>
  <p>傳送至此上面或下面</p>
  <div id="teleport-02"></div>
  
  <teleport :to="teleportDestination">
    <div style="background: orange;">被傳送區塊</div>
  </teleport>

  <hr>
  <h3>Computed</h3>
  <input type="number" v-model="num1">
  <input type="number" v-model="num2">
  <span>sum: {{ sum }}</span>

  <hr>
  <h3>Watch</h3>
  <button @click="watchedObject.name = watchedObject.name + '!'">改變 watchedObject</button>
  <span>{{ watchedObject }}</span>

  <hr>
  <h3>Style slot content</h3>
  <AppModal>
    <template v-slot:content>
      <p>v-slot: content</p>
    </template>
  </AppModal>

</template>

<script>
import { ref, computed, watch, onMounted } from 'vue';
import AppButton from './AppButton.vue';
import AppModal from './AppModal.vue';

export default {
  setup() {
    /* 測試 Component，以 appButton 測試 */

    const appButtonText = ref('000000000')
    const appButtonCount = (count) => {
      console.log(count)
    }

    /* 測試 Teleport，可以把內容傳送至指定目標 */
    const teleportDestination = '#teleport-01'

    /* 測試 computed */
    const num1 = ref(1);
    const num2 = ref(2);
    const sum = computed(() => num1.value + num2.value)


    /* 測試 watch，deep, immediate 設定放於第三個參數*/
    const watchedObject = ref({ name: 'watch test' })
    watch(watchedObject, (newVal, oldVal) => {
      console.log(oldVal.name, newVal.name)
    }, { deep: true, immediate: false })

    /* 測試 hook */
    onMounted(() => {
      console.log("onMounted!!");
    });

    return {
      appButtonText,
      appButtonCount,
      teleportDestination,
      num1,
      num2,
      sum,
      watchedObject
    }
  },
  components: {
    AppButton,
    AppModal
  }
}
</script>

<style scoped>

</style>

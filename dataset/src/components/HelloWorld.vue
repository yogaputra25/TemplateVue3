<script setup >
import { ref, onMounted } from 'vue'
import axios from 'axios'

defineProps({
  msg: String,
})

const count = ref(0)

const data = ref([])
const eror = ref(null)

const fetchData = async () => {
  try {
    const response = await axios.get('https://api.polygon.io/v2/aggs/ticker/AAPL/range/1/day/2023-01-09/2023-01-09?apiKey=FtRWh0kkJ6wbp8gx8rlfZeyn4ApiLgZp')
    data.value = response.data.results
  } catch (err) {
    eror.value = err.message
  }
}

onMounted(() => {
  fetchData()
})

</script>

<template>
  <h1>{{ msg }}</h1>
 
  <h1  v-for="item in data" :key="item.id">{{ item.v }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <button type="button" @click="test()">test</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>

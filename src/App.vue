<template>
  <div>
    App.vue
    {{ abc }}
    {{ utilVarRef }}
    {{ utilVarReact.key }}
  </div>
  <test-1 />
</template>

<script>
import { ref, reactive } from 'vue'
import { utilVarRef, utilVarReact } from './Utils/util'
import Test1 from './components/Test1.vue'
export default {
  name: 'App',
  components: {
    Test1
  },
  setup () {
    let abc = ref('testing')
    let userDetails = reactive({
      name: 'Jhon',
      age: '25'
    })
    abc.value = 2
    utilVarRef.value = 'changed'
    utilVarReact.key = 'react-changed' // no need to mention .value to access key.
    return {
      abc,
      utilVarRef,
      userDetails,
      utilVarReact
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

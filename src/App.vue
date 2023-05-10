<template>
  <div>
    App.vue
    {{ abc }}
    {{ utilVarRef }}
    {{ utilVarReact.key }}
    {{ myValues.someVar }}
    {{ userDetails.todo }}
    <test-1 />
    <div :class="classObject">
      computed: {{ userInfo }}
    </div>
    <div>
      Group Computed: {{ computedPpty.ageVal }}
    </div>
    <div>
      Methods
      <button @click="alert"> Click me</button>
    </div>
  </div>

</template>

<script>
import { ref, reactive, computed } from 'vue'
import { utilVarRef, utilVarReact } from './Utils/util'
import Test1 from './components/Test1.vue'
export default {
  name: 'App',
  components: {
    Test1
  },
  setup () {
    const abc = ref('testing')
    const userDetails = reactive({
      name: 'Jhon',
      age: 25
    })
    abc.value = 2
    utilVarRef.value = 'changed'
    utilVarReact.key = 'react-changed' // no need to mention .value to access key.
    const classObject = ref({
      active: true,
      inactive: false
    })
    // combining multiple refs
    const myValues = ref({
      someVar: true,
      otherValue: false
    })

    // computed 
    const userInfo = computed(() => {
      return userDetails.name + ' ' + userDetails.age 
    })
    console.log(userInfo.value) // accessing computed

    // Grouping computed properties
    const computedPpty = {
      firstName: computed(() => {
        return userDetails.name
      }),
      ageVal: computed(() => {
        return userDetails.age
      })
    }
    console.log(computedPpty.firstName.value, 'group computed')

    // methods
    function alert() {
      window.alert('button clicked')
    }
   
    return {
      abc,
      utilVarRef,
      userDetails,
      utilVarReact,
      myValues,
      userInfo,
      computedPpty,
      classObject,
      alert
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
.active {
  font-size: 18px;
  color: red;
}
.inactive {
  font-size: 24px;
}
</style>

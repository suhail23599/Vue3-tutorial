<template>
  <div>
    <router-view />
    App.vue
    {{ abc }}
    {{ utilVarRef }}
    {{ utilVarReact.key }}
    {{ myValues.someVar }}
    {{ userDetails.todo }}
    <test-1 propVal="2" @receive-event="eventCall">
      <template #slotVal>
        <div>Slot</div>
      </template>
    </test-1>
    <div :class="classObject">
      computed: {{ userInfo }}
    </div>
    <div>
      Group Computed: {{ computedPpty.ageVal }}
    </div>
    <div>
      Methods
      <button @click="alert(); increment()"> Click me</button>
      <div>count: {{ count }}</div>
    </div>
  </div>

</template>

<script>
import { ref, reactive, computed, onRenderTracked, onRenderTriggered, watch, watchEffect } from 'vue'
import { utilVarRef, utilVarReact } from './Utils/util'
import Test1 from './components/Test1.vue'
export default {
  name: 'App',
  components: {
    Test1
  },
  setup () {
    console.log(this, 'THIS')
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

    const count = ref(0)

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

    function increment() {
      count.value++
    }

    // hooks
    onRenderTracked ( (event) => {
      console.log('Tracked-event', event)
    })

    onRenderTriggered((event) => {
      console.log('re-rendered', event)
    })

    // watch
    watch (count, (newVal, oldVal) => {
      console.log(newVal, oldVal, 'Watch')
    })

    watchEffect(() => {
      console.log(count.value, 'Watch effect')
    })

    function eventCall (args) {
      console.log('event1')
      console.log('event', args)
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
      alert,
      increment,
      count,
      eventCall
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

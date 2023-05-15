<template>
   <div>
      Test 1 {{utilVarRef}}
   </div>
   <div>
      Props: {{propValue}}
   </div>
   <button @click="emitEvent">
      emit an event
   </button>
   <button @click="redirect()">Go to about</button>
   <slot name="slotVal"></slot>
</template>

<script>
import { utilVarRef } from '../Utils/util.js'
import { useRouter } from 'vue-router'
export default {
   // const props = defineProps(['propVal'])
   // const emit = defineEmits(['receiveEvent'])
   props: ['propVal'],
   setup (props, context) {
      const router = useRouter()
      console.log(utilVarRef.value)
      console.log(context.slots)
      function emitEvent () {
        console.log('emit')
        context.emit('receiveEvent', 7)
      }
      function redirect () {
         console.log('redirect')
         router.push('/about')
      }
      return {
         utilVarRef,
         propValue: props.propVal,
         emitEvent,
         redirect
      }
   }
}
</script>
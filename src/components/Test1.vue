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
   <slot name="slotVal"></slot>
</template>

<script>
import { utilVarRef } from '../Utils/util.js'
export default {
   // const props = defineProps(['propVal'])
   // const emit = defineEmits(['receiveEvent'])
   props: ['propVal'],
   setup (props, context) {
      console.log(utilVarRef.value)
      console.log(context.slots)
      function emitEvent () {
        console.log('emit')
        context.emit('receiveEvent', 7)
      }
      return {
         utilVarRef,
         propValue: props.propVal,
         emitEvent
      }
   }
}
</script>
<template>
   <div>
      Test 1 {{utilVarRef}}
   </div>
</template>

<script>
import { utilVarRef } from '../Utils/util.js'
export default {
   setup() {
      console.log(utilVarRef.value)
      return {
         utilVarRef
      }
   }
}
</script>
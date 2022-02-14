<template>
  <div class="home">

   <!-- <HelloWorld/> -->
   <todo/>

  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Todo from '@/components/Todo.vue'

export default {
  name: 'Home',
  components: {
    Todo
    
  }
}
</script>

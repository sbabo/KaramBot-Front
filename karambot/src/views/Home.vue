<template>
  <div class="home">
    <vueChat msg="KaramBot"/>
  </div>
</template>

<script>
// @ is an alias to /src
import vueChat from '@/components/vueChat.vue'

export default {
  name: 'home',
  components: {
    vueChat
  }
}
</script>

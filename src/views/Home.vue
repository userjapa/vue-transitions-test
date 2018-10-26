<template>
  <div class="home">
    <img alt="Vue logo" src="@/assets/logo.png">
    <Transitions/>
  </div>
</template>

<script>
// @ is an alias to /src
import Transitions from '@/components/Transitions'

export default {
  name: 'home',
  components: {
    Transitions
  }
}
</script>

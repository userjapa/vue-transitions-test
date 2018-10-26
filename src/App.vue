<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <!-- Router Transition -->
    <transition name="route-fade">
      <router-view/>
    </transition>
  </div>
</template>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

.route-fade {
  &-enter-active {
    animation: fade .25s ease-out backwards;
    animation-delay: .25s;
  }
  &-leave-active {
    animation: fade .25s ease-in reverse backwards;
  }
}

@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>

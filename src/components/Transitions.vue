<template>
  <div class="transitions">
    <h1>Vue Transition Use</h1>
    <p>
      View the repository
      <a href="https://github.com/usuarioJapa/vue-transitions-test.git" target="_blank" rel="noopener">repository</a>.
    </p>
    <hr>
    <h3>Hide elements</h3>
    <div class="transitions__item transitions__item--show">
      <p>Transition when hide elements using <b>v-if</b> or <b>v-show</b>.</p>
      <button type="button" name="button" @click="showEx1 = !showEx1">{{ showEx1 ? 'Hide' : 'Show' }}</button>
      <transition name="ex-01">
        <p v-show="showEx1">Example 1</p>
      </transition>
    </div>
    <hr>
    <h3>Switch Elements</h3>
    <div class="transitions__item transitions__item--if">
      <p>Transition when switch elements using <b>v-if</b> and <b>v-else</b>.</p>
      <transition name="ex-02">
        <button @click="showEx2 = true" key="on" v-if="!showEx2">Turn ON</button>
        <button @click="showEx2 = false" key="off" v-else>Turn OFF</button>
      </transition>
    </div>
    <hr>
    <h3>Render Lists</h3>
    <div class="transitions__item transitions__item--group">
      <p>Transition when render lists with <b>v-for</b> using transition-group.</p>
      <div>
        <input type="number" step="1" min="0" max="99" v-model="nextNum">
      </div>
      <div>
        <button @click="add()">Insert</button>
        <button @click="remove()">Remove</button>
        <button @click="shuffle()">Shuffle</button>
      </div>
      <br>
      <transition-group name="list">
        <span class="list__item" v-for="item in list" :key="item">{{ item }}</span>
      </transition-group>
    </div>
    <hr>
    <h3>Search Lists</h3>
    <div class="transitions__item transitions__item--list">
      <p>Transition when render lists with <b>v-for</b> using transition-group.</p>
      <div>
        <input type="text" v-model="searchInList">
      </div>
      <transition-group name="list-names">
        <p class="list-names__item" v-for="(name, index) in namesFiltered" :key="name" :data-index="index">{{ name }}</p>
      </transition-group>
    </div>
  </div>
</template>

<script>
import { shuffle } from 'lodash'

export default {
  name: 'Transitions',
  data () {
    return {
      showEx1: true,
      showEx2: false,
      list: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      nextNum: 11,
      names: ['Alan', 'Fraga', 'Snow', 'Dan', 'Garry'],
      searchInList: ''
    }
  },
  computed: {
    namesFiltered () {
      return this.names.filter(n => n.toLowerCase().match(this.searchInList.toLowerCase()))
    }
  },
  methods: {
    randomIndex () {
      return Math.floor(Math.random() * this.list.length)
    },
    add () {
      if (!this.list.includes(this.nextNum)) this.list.splice(this.randomIndex(), 0, this.nextNum++)
      else alert('Number already on list!')
    },
    remove () {
      this.list.splice(this.randomIndex(), 1)
    },
    shuffle () {
      this.list = shuffle(this.list)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 15px 0 0;
}
a {
  color: #42b983;
}

button {
  transition: all .2s;
  cursor: pointer;
  margin: 0 5px;
  padding: 3px 10px;
  border: 2px solid #ddd;
  background-color: #ddd;
  color: #777;
  outline: none;
  border-radius: 25px;
  &:hover {
    background-color: #eee;
    border-color: #eee;
  }
  &:active {
    color: #bbb;
  }
  &:disabled {
    cursor: not-allowed;
    background-color: #eee;
    border-color: #eee;
    color: #ccc;
  }
}

input {
  margin: 5px;
  padding: 3px 10px;
  border: 2px solid #ddd;
  width: 187.25px;
  border-radius: 25px;
  text-align: center;
  outline: none;
}

.transitions {
  &__item {
    margin: 0 10px;
    &--show {
      height: 125px;
    }
    &--if {
      height: 90px;
    }
    &--group {
      height: auto;
      min-height: 220px;
    }
    &--list {
      height: 280px;
    }
  }
}

.ex-01 {
  &-enter-active {
    animation: toLeft .5s ease backwards;
    animation-delay: .5s;
  }
  &-leave-active {
    animation: toRight .5s ease reverse backwards;
  }
}

.ex-02 {
  &-enter-active {
    animation: toRight .5s ease backwards;
    animation-delay: .5s;
  }
  &-leave-active {
    animation: toLeft .5s ease reverse backwards;
  }
}

.list {
  transition: all 1s;
  &-enter, &-leave-to {
    opacity: 0;
  }
  &-enter {
    transform: translateY(-50px);
  }
  &-leave-to {
    transform: translateY(50px);
  }
  &-leave-active {
    position: absolute;
  }
  &__item {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    border: 2px solid #cfcfcf;
    width: 30px;
    height: 30px;
    transition: all 1s;
    margin: 2.5px 5px;
  }
}

.list-names {
  display: flex;
  justify-content: center;
  align-content: center;
  transition: all 1s;
  &-enter, &-leave-to {
    opacity: 0;
  }
  &-enter {
    height: 0px;
  }
  &-leave-to {
    height: 18px;
  }
  &-enter-active {
    height: 18px;
  }
  &-leave-active {
    align-self: center;
    width: calc(100% - #{36.5px});
    position: absolute;
    height: 0;
  }
  &__item {
    transition: all 1s;
  }
}

@keyframes toTop {
  from {
    opacity: 0;
    transform: translateY(-150px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes toBottom {
  from {
    opacity: 0;
    transform: translateY(150px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes toLeft {
  from {
    opacity: 0;
    transform: translateX(-150px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes toRight {
  from {
    opacity: 0;
    transform: translateX(150px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>

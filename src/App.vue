<template>
  <div id="app">
    <img class="vue-logo" alt="Vue logo" src="./assets/logo.png">

    <h3>Selector</h3>

    <div class="flex-wrapper">
      <div class="wrapper">
        <transition-group
          name="selector-transition"
          tag="div"
          class="transition-wrapper"
        >
          <Selector
            class="transition-element"
            key="selector"
            v-model="selectedValue"
            :options="options"
            :is-opened.sync="isOpened"
          ></Selector>

          <button
            class="transition-element button-save"
            key="button"
          >Save</button>
        </transition-group>
      </div>
    </div>
  </div>
</template>

<script>
import Selector from '@/components/Selector.vue'

const OPTIONS = [{ id: 1, value: 1 }, { id: 2, value: 2 }, { id: 3, value: 3 }]

export default {
  name: 'app',

  components: {
    Selector,
  },

  data: () => ({
    selectedValue: OPTIONS[0],
    isOpened: false,
  }),
  computed: {
    options() {
      return OPTIONS
    },
  },
}
</script>

<style lang="postcss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 16px;
}
.vue-logo {
  height: 50px;
}

.flex-wrapper {
  display: flex;
  justify-content: center;
}
.wrapper {
  flex-basis: 300px;
}

.select-option {
  cursor: pointer;
  border: 1px solid black;
  margin-bottom: 8px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  background-color: #fff;
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);

  &._selected {
    background: #42b983;
    z-index: 1;
  }

  &._collapsed {
    position: absolute;
    width: 100%;
    opacity: 0;
    top: 0;
    left: 0;
  }
}
.button-save {
  cursor: pointer;
  border: 1px solid #42b983;
  background-color: #fff;
  border-radius: 6px;
  padding: 8px 16px;
  margin-top: 16px;
}

.transition-wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
}
.selector-transition-enter,
.selector-transition-leave-to {
  opacity: 0;
}
.selector-transition-leave-active {
  position: absolute;
  width: 100%;
  top: 0;
  left: 0;
}

.transition-element {
  transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
}
</style>

<template>
  <div id="app">
    <img class="vue-logo" alt="Vue logo" src="./assets/logo.png">

    <h3>Selector</h3>

    <div id="nav">
      <div @click="ver = 1" :class="{_active: ver === 1}">ver1</div>
      <div @click="ver = 2" :class="{_active: ver === 2}">ver2</div>
    </div>

    <transition-group
      name="selector-transition"
      tag="div"
      class="transition-wrapper"
      @before-leave="beforeLeave"
    >
      <template v-if="ver === 1">
        <div
          class="select-option"
          v-for="option in options"
          :key="option.id"
          :class="{
            _selected: option.value === value,
            _collapsed: isClosed && option.value !== value
          }"
          @click="onOptionClick(option)"
        >
          {{ option.value }}
        </div>
      </template>

      <template v-if="ver === 2">
        <div
          class="select-option"
          v-for="option in options2"
          :key="option.id"
          :class="{
            _selected: option.value === value
          }"
          @click="onOptionClick(option)"
        >
          {{ option.value }}
        </div>
      </template>

      <button class="button-save" key="button">Save</button>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: 'app',

  data: () => ({
    ver: 1,
    value: 1,
    isOpened: false,
  }),
  computed: {
    options() {
      return [{ id: 1, value: 1 }, { id: 2, value: 2 }, { id: 3, value: 3 }]
    },
    options2() {
      const { value, options } = this
      if (this.isClosed) {
        return [options.find(v => v.value === value)]
      }
      return options
    },
    isClosed() {
      return !this.isOpened
    },
  },
  methods: {
    onOptionClick(option) {
      if (this.isOpened) {
        this.value = option.value
        this.isOpened = false
      } else {
        this.isOpened = true
      }
    },
    beforeLeave(el) {
      el.classList.remove('_selected')
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
#nav {
  padding-bottom: 20px;
  display: flex;
  justify-content: center;
  div {
    cursor: pointer;
    font-weight: bold;
    color: #2c3e50;
    &._active {
      color: #42b983;
    }
  }
  div + div {
    margin-left: 16px;
  }
}

.select-option {
  border: 1px solid black;
  margin-bottom: 8px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  background-color: #fff;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);

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
  border: 1px solid #42b983;
  background-color: #fff;
  border-radius: 6px;
  padding: 8px 16px;
  margin-top: 16px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
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
</style>

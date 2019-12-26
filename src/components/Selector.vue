<template>
  <transition-group
    name="selector-transition"
    tag="div"
    class="transition-wrapper"
  >
    <div
      class="select-option"
      v-for="option in options"
      :key="option.id"
      :class="{
        _selected: option === value,
        _collapsed: isClosed && option !== value
      }"
      @click="onOptionClick(option)"
    >
      {{ option.value }}
    </div>
  </transition-group>
</template>

<script>
export default {
  props: {
    value: {
      type: Object,
      required: true,
    },
    options: {
      type: Array,
      required: true,
    },
    isOpened: {
      type: Boolean,
      required: true,
    },
  },
  computed: {
    isClosed() {
      return !this.isOpened
    },
  },
  methods: {
    onOptionClick(option) {
      if (this.isOpened) {
        this.$emit('input', option)
        this.$emit('update:isOpened', false)
      } else {
        this.$emit('update:isOpened', true)
      }
    },
  },
}
</script>

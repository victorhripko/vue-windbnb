<template>
  <div class="counter">
    <button class="counter__btn"
      @click="decrement"
      :class="{['counter__btn--disabled'] : val <= minValue}"
      :disabled="val <= minValue"
      :tabindex="val <= minValue ? -1 : null"
    >
      <MinusIcon size="1.5x" />
    </button>
    <span class="counter__value">{{val}}</span>
    <button class="counter__btn" @click="increment">
      <PlusIcon size="1.5x" />
    </button>
  </div>
</template>

<script>
import './Counter.scss';
import { PlusIcon, MinusIcon } from 'vue-feather-icons';

export default {
  name: 'Counter',
  components: {
    PlusIcon,
    MinusIcon,
  },
  props: {
    value: {
      type: Number,
      default: 0,
    },
    minValue: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      val: this.value,
    };
  },
  created() {
    if (this.value < this.minValue) {
      console.error(`Counter value less than minValue:
        value = ${this.value};
        minValue = ${this.minValue};
      `);
    }
  },
  methods: {
    increment() {
      this.val += 1;
      this.$emit('change', this.val);
    },
    decrement() {
      if (this.val <= this.minValue) return;
      this.val -= 1;
      this.$emit('change', this.val);
    },
  },
};
</script>

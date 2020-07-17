<template>
  <aside class="aside" :class="{'aside--open': open}">
    <div class="aside__overlay" @click="close"></div>
    <div class="aside__content">
      <div class="aside__header">
        <button class="aside__close" type="button" @click="close" aria-label="close button">
          <XIcon />
        </button>
      </div>
      <div class="aside__body">
        <slot name="body"></slot>
        <div class="aside__footer">
          <slot name="footer"></slot>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
import { XIcon } from 'vue-feather-icons';
import './Aside.scss';

export default {
  name: 'Aside',
  props: {
    open: {
      type: Boolean,
      default: false,
    },
  },
  components: {
    XIcon,
  },
  methods: {
    close() {
      this.$emit('close');
    },
  },
};
</script>

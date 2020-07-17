<template>
  <header class="header">
    <img class="header__logo" :src="logo" alt="">
    <button class="header__hamburger" type="button" @click="emit" aria-label="menu button">
      <SlidersIcon />
    </button>
  </header>
</template>

<script>
import logo from '@/assets/logo.svg';
import './Header.scss';
import { SlidersIcon } from 'vue-feather-icons';

export default {
  name: 'Header',
  data() {
    return {
      logo,
    };
  },
  components: {
    SlidersIcon,
  },
  methods: {
    emit() {
      this.$emit('click');
    },
  },
};
</script>

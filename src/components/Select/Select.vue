<template>
  <div class="select" :class="{'select--open' : isOpen}">
    <div class="select__overlay" v-if="isOpen && data" @click="isOpen = false"></div>
    <div class="select__field" :class="{'select__field--static': !data}" @click="isOpen = !isOpen">
      <span class="select__placeholder" v-if="!selectedValue">{{placeholder}}</span>
      {{selectedValue | select}}
      <ChevronDownIcon class="select__icon" size="1x" />
      <div class="select__list" v-if="isOpen && data">
        <div class="select__item select__item--default" @click="change(null)">None</div>
        <div class="select__item"
          v-for="(item, id) in data" :key="id"
          @click="change(item)">
          {{item | select}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import './Select.scss';
import { ChevronDownIcon } from 'vue-feather-icons';

export default {
  name: 'Select',
  props: {
    data: {
      default: null,
    },
    placeholder: {
      type: String,
      default: 'Choose...',
    },
  },
  data() {
    return {
      selectedValue: null,
      isOpen: false,
    };
  },
  components: {
    ChevronDownIcon,
  },
  methods: {
    change(val) {
      this.selectedValue = val;
      this.$emit('change', val);
    },
  },
  filters: {
    select(val) {
      return val ? val.split(' ').join(', ') : val;
    },
  },
};
</script>

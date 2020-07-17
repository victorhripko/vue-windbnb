<template>
  <div class="appartaments">
    <div class="appartaments__head">
      <h1 class="appartaments__countries" v-if="countries">
        Stays in {{countries}}
      </h1>
      <span class="appartaments__count">
        {{data.length | placesCount}} stays
      </span>
    </div>
    <div class="appartaments__body">
      <AppartamentsItem
        v-for="(item, id) in data" :key="id"
        :src="item.photo"
        :type="item.type"
        :rating="item.rating"
        :description="item.title"
        :superHost="item.superHost"
        :beds="item.beds"
      />
    </div>
  </div>
</template>

<script>
import './Appartaments.scss';
import AppartamentsItem from '@/components/AppartamentsItem/AppartamentsItem.vue';

export default {
  name: 'Appartaments',
  props: {
    data: null,
  },
  components: {
    AppartamentsItem,
  },
  computed: {
    countries() {
      return [...new Set(this.data.map((el) => el.country))].join();
    },
  },
  filters: {
    placesCount(val) {
      return val < 12 ? val : '12+';
    },
  },
};
</script>

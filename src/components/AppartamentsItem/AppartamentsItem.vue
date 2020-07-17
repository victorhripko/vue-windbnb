<template>
  <div class="appartaments-item">
    <div class="appartaments-item__image">
      <img class="appartaments-item__picture"
        :src="src"
        :alt="type"
        :class="{
          ['appartaments-item__picture--loaded'] : imgload
        }"
        loading="lazy"
        @load="imageLoad"
      />
    </div>
    <div class="appartaments-item__wrap">
      <div class="appartaments-item__info">
        <h5 class="appartaments-item__title">
          <span class="appartaments-item__superhost" v-if="superHost">super host</span>
          {{type}} {{beds | bedsCount}}
        </h5>
        <span class="appartaments-item__rating">
          <StarIcon size="1x" class="appartaments-item__star" />{{rating}}
        </span>
      </div>
      <p class="appartaments-item__description">{{description}}</p>
    </div>
  </div>
</template>

<script>
import './AppartamentsItem.scss';
import { StarIcon } from 'vue-feather-icons';

export default {
  name: 'AppartamentsItem',
  data() {
    return {
      imgload: false,
    };
  },
  props: {
    src: String,
    type: String,
    rating: Number,
    description: String,
    beds: Number,
    superHost: Boolean,
  },
  components: {
    StarIcon,
  },
  filters: {
    bedsCount(val) {
      return val ? `.${val} beds` : null;
    },
  },
  methods: {
    imageLoad() {
      this.imgload = true;
    },
  },
};
</script>

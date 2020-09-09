<template>
  <div id="app" class="app">
    <Header @click="toggleAside" />
    <Appartaments class="app-body" :data="filterData" />
    <Aside @close="toggleAside" :open="aisdeOpen">
      <template v-slot:body>
        <h5 class="title">City</h5>
        <Select :data="citiesData" placeholder="Choose city" @change="filterCity" />
        <h5 class="title">Adults</h5>
        <p class="subtitle">Ages 13 or above</p>
        <Counter @change="adults" />
        <h5 class="title">Children</h5>
        <p class="subtitle">Ages 2-12</p>
        <Counter @change="childrens" />
        <h5 class="title">Guests: {{guests}}</h5>
      </template>
      <template v-slot:footer>
        <button class="button" type="button" @click="filterGuests">
          <SearchIcon class="button__start-icon" size="1x" />
          Apply
        </button>
      </template>
    </Aside>
    <Footer class="app-footer" />
  </div>
</template>

<script>
import Header from '@/components/Header/Header.vue';
import Footer from '@/components/Footer/Footer.vue';
import Aside from '@/components/Aside/Aside.vue';
import Appartaments from '@/components/Appartaments/Appartaments.vue';
import Select from '@/components/Select/Select.vue';
import Counter from '@/components/Counter/Counter.vue';
import { SearchIcon } from 'vue-feather-icons';
import appartamentsData from '@/assets/stays.json';

export default {
  name: 'App',
  data() {
    return {
      aisdeOpen: false,
      adult: 0,
      child: 0,
      appartamentsData,
      filterData: JSON.parse(JSON.stringify(appartamentsData)),
      citiesData: [],
      city: null,
    };
  },
  components: {
    Header,
    Select,
    Aside,
    Appartaments,
    Counter,
    SearchIcon,
    Footer,
  },
  methods: {
    toggleAside() {
      this.aisdeOpen = !this.aisdeOpen;
    },
    adults(value) {
      this.adult = value;
    },
    childrens(value) {
      this.child = value;
    },
    filterGuests() {
      let temp = this.appartamentsData;

      if (this.city) {
        temp = temp
          .filter((el) => el.city === this.city)
          .filter((el) => el.maxGuests >= this.adult + this.child);
      } else {
        temp = this.appartamentsData
          .filter((el) => el.maxGuests >= this.adult + this.child);
      }

      console.log(this.city);

      this.filterData = temp;
      this.aisdeOpen = false;
    },
    filterCity(value) {
      if (value) {
        const [city] = value.split(' ');
        this.city = city;
      } else {
        this.city = null;
      }
    },
  },
  computed: {
    guests() {
      return this.adult + this.child;
    },
  },
  created() {
    const cities = [...new Set(appartamentsData.map((el) => el.city))];

    cities.forEach((el) => {
      this.citiesData = [...this.citiesData, `${el} ${appartamentsData.find((fel) => fel.city === el).country}`];
    });
  },
};
</script>

<style lang="scss">
* { box-sizing: border-box; }

html,
body,
.app {
  scrollbar-width: none;

  &::-webkit-scrollbar {
    display: none;
  }
}

:root {
  --color: #333;
  --bg: white;
  --accent: #ef7979;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
                Helvetica, Arial, sans-serif, "Apple Color Emoji",
                "Segoe UI Emoji", "Segoe UI Symbol";
  background-color: var(--bg);
  color: var(--color);

  // @media (prefers-color-scheme: dark) {
  //   --bg: #333;
  //   --color: white;
  // }
}

.app {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.app-body {
  margin-bottom: 50px;
}

.app-footer {
  margin-top: auto;
}

.title {
  margin-bottom: 10px;
  font-size: 16px;
  font-weight: 600;
}

.subtitle {
  margin-top: 0;
  margin-bottom: 10px;
  font-weight: 400;
  font-size: 14px;
  color: #9d9d9d;
}

.button {
  display: inline-flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 15px 20px;
  border: 0;
  border-radius: 4px;
  color: white;
  text-align: center;
  font-size: 18px;
  line-height: 0;
  background-color: var(--accent);
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
  cursor: pointer;
  box-shadow: 0 5px 15px -5px darken(#ef7979, 5%);
  transition: 200ms ease-in-out;

  &:hover {
    background-color: darken(#ef7979, 5%);
    box-shadow: 0 10px 20px -5px darken(#ef7979, 5%);
  }

  &__start-icon {
    margin-right: 0.5em;
  }
}
</style>

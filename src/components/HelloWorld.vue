<template>
  <div class="hello">
    <checkbox :checkboxes="columns" 
              @selected="selectedTag" />
    <select-color :options="colors" @selectedColor="selectedColor" />
    <table>
      <tr>
        <td v-for="(title, i) in columns" 
            :key="i" 
            v-show="selected.includes(title)">
            {{title}}
        </td>
      </tr>
      <tr v-for="car in newCars" 
          :key="car.model" 
          v-show="color !== 'All' ? car.color === color : true">
          <td v-for="(column, i) in columns" :key="i" v-show="selected.includes(column)">
            {{car[column]}}
          </td>
      </tr>
    </table>
  </div>
</template>

<script>
import Checkbox from './lib/checkbox/Checkbox';
import SelectColor from './lib/select/Select';

export default {
  name: 'HelloWorld',
  data () {
    return {
      cars: [
        { model: "audi", year: 2016, color: "red", audiosystem: true },
        { model: "reno", year: 2017, color: "blue", audiosystem: true },
        { model: "ford", year: 2019, color: "red", audiosystem: false },
        { model: "bmw", year: 2018, color: "green", audiosystem: false },
        { model: "bmw5", year: 2018, color: "white", audiosystem: false, maxSpeed: 280 },
        { model: "kia", year: 2018, audiosystem: false }
      ],
      selected: [],
      color: 'All',
    }
  },
  methods: {
    selectedTag(columns) {
      this.selected = columns;
    },
    selectedColor(color) {
      this.color = color;
    }
  },
  computed: {
    newCars() {
      let newCars = [...this.cars];
      for(let car of newCars) {
        let res = this.columns.filter(el => Object.keys(car).indexOf(el) === -1);
        if(res.length) {
          for(let i = 0; i <= res.length - 1; i++) {
            car[res[i]] = null;
          }
        }
      }
      return newCars;
    },
    columns() {
      return Object.keys(this.cars.reduce((result, obj) => {
        return Object.assign(result, obj);
      }, {}));
    },
    colors() {
      let colors = this.cars.map(car => car.color).filter(el => el);
      colors.unshift('All');
      return [...new Set(colors)];
    }
  },
  components: {
    Checkbox,
    SelectColor
  }
}
</script>
<style scoped>
  table {
    border-spacing: 0px;
    border-collapse: collapse;
    margin: auto;
  }
  td {
    padding: 4px;
    border: 1px solid #111;
  }
</style>
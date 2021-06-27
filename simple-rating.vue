<template>
    <div>
        <label class="star"
        v-for="rate in ratingsRange" v-bind:key="rate" 
        :class="{'selected': ((rated >= rate)) && selected != null}"
        v-on:mouseup="setRating(rate)" 
        v-on:mouseover="hoverin(rate)" 
        v-on:mouseout="hoverout">
        <input class="checkbox" 
        type="radio" 
        v-model="rating"><div v-if="rated >=rate"><span v-html="star1"></span></div><div v-else><span v-html="star2"></span></div></label>
    </div>
</template>

<script>
export default {
   props: {
    afterrated: {
      type: Function,
    }
  },
  data: function () {
    return {
      ratingsRange: [1, 2, 3, 4, 5],
      rated: 0,
      temp: 0,
      selected: null,
      rating: 0,
      star1: "&#9733",
      star2: "&#9734"
    };
  },

  methods: {
    setRating(rate) {
      this.temp = rate;
      this.rated = this.temp;
      this.selected = true;
      this.afterrated(this.rated);
    },
    hoverin(rate) {
      this.temp = this.rated;
      this.rated = rate;
    },
    hoverout() {
      this.rated = this.temp;
      this.rating = this.temp;
    },
  },
};
</script>

<style>
.checkbox {
    position: absolute;
    overflow: hidden;
    margin: -1px;
    height: 1px;
    width: 1px;
    padding: 0;
    clip: rect(0 0 0 0);
  }

.star {
    display: inline-block;
    font-size: 1.5em;
    padding: 3px;
    line-height: 1;
    vertical-align: middle;
    color: #b8b8b8;
}

.star.selected {
    color: black;
}
</style>
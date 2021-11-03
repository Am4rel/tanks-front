<template>
  <div>
    <div class="header-wrapper" :class="layout">
      <h1 class="page-title">Most popular tanks</h1>
      <label class="switch">
        <span class="switch-label">{{layout}}</span>
        <input type="checkbox" class="switch_input" @change="changeLayout">
        <span class="slider" :class="layout"></span>
      </label>
    </div>
    <div class="thumbnails" :class="layout">
      <nuxt-link class="link-thumb" v-for="tank of tanks" :key="tank._id" :to="tank._id">
        <Tankthumb :tank-item="tank"/>
      </nuxt-link>
    </div>
  </div>
</template>

<script>
// import { Context } from '@nuxt/types'

export default {
  data () {
    return {
      layout: "grid"
    }
  },

  methods: {
    changeLayout() {
      if (this.layout === "grid"){
        this.layout = "flex"
      }else{
        this.layout = "grid"
      }
      // console.log(this.$attrs)
    }
  },

  async asyncData(context) {
    try {
      const tanks = await context.$axios.$get(`https://tanks-proj.herokuapp.com/tanks`);
      // console.log(tanks)
      return {tanks};
    } catch (e) {
      console.log(e)
    }
  }
}

</script>

<style>
root {
    margin: 0;
    padding: 0;
}

* {
    background-color: #212020;
    color: #b3a6a6;
}

.thumbnails {
  padding: 40px;
}

.thumbnails.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, calc(100% / 4)));
  justify-content: center;
  align-items: center;
}

.thumbnails.flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.header-wrapper {
  width: calc(100% - 40px);
  margin: 20px auto;

  justify-content: center;
  align-items: center;
}

.header-wrapper.flex {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header-wrapper.grid {
  display: grid;
  grid-template-columns: max-content max-content 1fr;
}

.header-wrapper.grid .switch {
  grid-column-start: -1;
}

.link-thumb {
  margin: 10px;
}

.flex .link-thumb {
  max-width: calc(100% / 4 - 20px);
  min-width: 200px;
}

.switch-label {
  position: absolute;
  top: 40px;
  right: 20px;

  text-align: center;
}

.switch {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
  }
  
.switch_input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;

  width: 60px;
  height: 34px;

  background-color: #3a5243;
  border-radius: 34px;
  transition: 400ms;
}

.slider.flex {
  display: flex;
  align-items: center;
}

.slider.grid {
    display: grid;
    align-items: center;
  }

.slider:before {
  content: "";
  display: inline-block;
  height: 26px;
  width: 26px;

  margin-left: 4px;

  background-color: #b3a6a6;
  border-radius: 50%;
  transition: 400ms;
}

input:checked + .slider:before {
  transform: translateX(26px);
}
</style>
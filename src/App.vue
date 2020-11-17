<template>
  <div id="app">
    <div id="svg-container">
      <svg id="svg-1" :width="treemapWidth" :height="treemapHeight">
        <g
          v-for="rectangle in treeMapResult"
          :key="`${rectangle.x}:${rectangle.y}`"
          class="treemap__rectangle"
          :fill="rectangle.data.color"
        >
          <rect
            :x="rectangle.x"
            :y="rectangle.y"
            :width="rectangle.width"
            :height="rectangle.height"
          ></rect>
          <text :x="getXText(rectangle)" :y="getYText(rectangle)" fill="black">
            {{ rectangle.data.label }}
          </text>
        </g>
        Sorry, your browser does not support inline SVG.
      </svg>
    </div>
  </div>
</template>

<script>
import { getTreemap } from "treemap-squarify";

export default {
  name: "App",
  methods: {
    getXText(rectangle) {
      return rectangle.x + 2;
    },
    getYText(rectangle) {
      console.log("The Y rectangle is -: " + JSON.stringify(rectangle.y));
      return rectangle.y + 15;
    },
  },
  data: function() {
    return {
      treeMapResult: "unknown",
      treemapWidth: 1000,
      treemapHeight: 1000,
    };
  },
  created() {
    this.treeMapResult = getTreemap({
      data: [
        { value: 23, color: "#1B277C", label: "23" },
        { value: 20, color: "#2C5A9C", label: "20" },
        { value: 19, color: "#3984B6", label: "19" },
        { value: 14, color: "#3F97C2", label: "14" },
        { value: 9, color: "#78C6D0", label: "9" },
        { value: 8, color: "#AADACC", label: "8" },
        { value: 7, color: "#DCECC9", label: "7" },
      ],
      width: 1000,
      height: 1000,
    });

    console.log("The tree is -: " + JSON.stringify(this.treeMapResult));
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: black;
  height: 100vh;
  width: 100vw;
}

#svg-container {
  display: flex;
  align-items: center;
  background-color: black;
  height: 100%;
}

#svg-1 {
  margin: 0 auto;
  display: block;
}

html,
body {
  width: 100vh;
  height: 100vh;
  margin: 0;
}
</style>

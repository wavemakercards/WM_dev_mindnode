<template>
  <mindmap style="height: 100vh" v-model="data" @update:modelValue="onChange" @click="doClick" :locale="locale"
    :branch="4" :x-gap="84" :y-gap="40" :zoom="true" :fit-btn="true" :center-btn="true" :download-btn="true" :drag="true"
    :edit="true" :add-node-btn="true" :sharp-corner="false" :ctm="false" :timetravel="false" :vertical="true" />
</template>

<script>
import learn from "./learn.json";
import mindmap from "vue3-mindmap";
import "vue3-mindmap/dist/style.css";

export default {
  name: "App",
  components: { mindmap },
  data() {
    return {
      data: [...learn],
      locale: "en",
    };
  },
  methods: {
    onChange() {
      console.log("Update", JSON.parse(JSON.stringify(this.data)))
    },
    doClick() {
      let node = document.getElementsByClassName("Mindmap_selected_fgvb6")[0]
      if (node) {
        let d = node.dataset.id.split("-")
        console.log(d)
        let result = this.data
        result = result[0]
        d.forEach((v, i) => {
          if (i != 0) {
            result = result.children[v]
            console.log(result.name)
          } else {
            console.log(result.name)
          }
        })

      }


    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;700&display=swap');

body {
  font-family: "Poppins", Arial, Helvetica, sans-serif;
}

.container {
  width: 100%;
  height: calc(100vh - 16px);
  border-radius: 4px;
  border: thin solid rgba(0, 0, 0, 0.12);
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.12);
  display: grid;
  grid-template-columns: 75% 1px 25%;
  grid-template-rows: 48px 1px auto;
}

/*
.Mindmap_fit_fgvb6,
.Mindmap_gps_fgvb6,
.Mindmap_download_fgvb6 {
  border: 1px solid red;
  background: black;
}

.Mindmap_text_fgvb6 tspan {
  stroke: none;
  fill: #fff;
}
*/
.node .Mindmap_content_fgvb6 .Mindmap_text_fgvb6 rect {
  stroke: darkblue;
  fill: #fff;
  border-radius: 20px;
  opacity: 1;
  margin: 10px;
  bottom: 40px;
}

.node .Mindmap_selected_fgvb6 .Mindmap_text_fgvb6 rect {
  stroke: darkblue;
  fill: lightgreen;
  border-radius: 20px;
  opacity: 1;
  margin: 10px;
  bottom: 40px;
}

foreignObject {
  overflow: visible;
  height: fit-content;
}

foreignObject div {
  stroke: darkblue;
  fill: #fff;
  opacity: 1;
  padding: 10px !important;
  border-radius: 5px;
  position: relative;
  top: -20px;
  left: -20px;
  margin: 10px;
  border: 2px solid darkblue;

  background-color: #fff;
  ;
}
</style>

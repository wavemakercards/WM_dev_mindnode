<template>
  <mindmap style="height: 100vh" v-model="data" @update:modelValue="onChange" @click="doClick" :locale="locale"
    :branch="4" :x-gap="84" :y-gap="18" :zoom="true" :fit-btn="true" :center-btn="true" :download-btn="true" :drag="true"
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
        let result = [...this.data]
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
body {
  font-family: Arial, Helvetica, sans-serif;
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

.Mindmap_fit_fgvb6,
.Mindmap_gps_fgvb6,
.Mindmap_download_fgvb6 {
  border: 1px solid red;
  background: black;
}
</style>

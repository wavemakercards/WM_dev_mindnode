<template>
  <MindNode />
</template>

<script>
import MindNode from "./components/MindNode.vue";
import "vue3-mindmap/dist/style.css";
import { uuid } from 'vue-uuid';
import learn from "./learn.json"
import lang from "./lang.json"
export default {
  name: "App",
  components: { MindNode },
  data() {
    return {
      mindNodeData: learn,
      uuid,
      lang
    };
  },
  methods: {

  }
};
</script>

<style></style>

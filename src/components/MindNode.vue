<template>
    <mindmap style="height: 100vh" v-model="$root.mindNodeData" @update:modelValue="onChange" @click="doClick"
        :locale="locale" :branch="lineThickness" :x-gap="xgap" :y-gap="ygap" :zoom="zoom" :fit-btn="fitbtn"
        :center-btn="centerbtn" :download-btn="downloadbtn" :drag="draggable" :edit="editable" :add-node-btn="addnodebtn"
        :sharp-corner="sharpcorner" :ctm="contextMenu" :timetravel="timetravel" :vertical="vertical"
        :contextTxt="$root.lang" />
</template>
  
<script>
import mindmap from "vue3-mindmap-ou";
import "vue3-mindmap-ou/dist/style.css";
export default {
    name: "App",
    components: { mindmap },
    data() {
        return {
            locale: "en",
            lineThickness: 4,
            xgap: 84,
            ygap: 40,
            zoom: true,
            fitbtn: true,
            centerbtn: true,
            downloadbtn: true,
            draggable: true,
            editable: true,
            addnodebtn: true,
            sharpcorner: false,
            contextMenu: true,
            timetravel: true,
            vertical: false
        };
    },
    methods: {
        onChange() {
            console.log("Update", JSON.parse(JSON.stringify(this.$root.mindNodeData)))
            /// might need to do some tewaking of the $root.mindNodeData to make sure each node has a uuid somehow
        },
        doClick() {
            let node = document.getElementsByClassName("Mindmap_selected_fgvb6")[0]
            if (node) {
                let d = node.dataset.id.split("-")
                // console.log(d)
                let result = this.$root.mindNodeData
                result = result[0]
                d.forEach((v, i) => {
                    if (i != 0) {
                        result = result.children[v]
                        // console.log(result.name)
                    } else {
                        // console.log(result.name)
                    }
                })

                if (!result.uuid) {
                    result.uuid = this.$root.uuid.v4()
                }
                if (!result.children) {
                    result.children = []
                }
                console.log(result)
            }


        }
    }
};
</script>
  
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;700&display=swap');

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
    margin: -10px;
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
  
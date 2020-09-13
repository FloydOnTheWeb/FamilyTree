<template>
  <div class="master">
    <h1>{{ msg }}</h1>
    <div id="graph"></div>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import d3 from "../assets/js/d3.v4.min.js";
// eslint-disable-next-line no-unused-vars
import dTree from "../assets/js/dTree.min.js";
// eslint-disable-next-line no-unused-vars
import lodash from "../assets/js/lodash.min.js";

export default {
  name: "Master",
  data: function () {
    return {
      treeData: [
        {
          name: "Niclas Superlongsurname",
          class: "man",
          textClass: "emphasis",
          marriages: [
            {
              spouse: {
                name: "Iliana",
                class: "woman",
                extra: {
                  nickname: "Illi",
                },
              },
              children: [
                {
                  name: "James",
                  class: "man",
                  marriages: [
                    {
                      spouse: {
                        name: "Alexandra",
                        class: "woman",
                      },
                      children: [
                        {
                          name: "Eric",
                          class: "man",
                          marriages: [
                            {
                              spouse: {
                                name: "Eva",
                                class: "woman",
                              },
                            },
                          ],
                        },
                        {
                          name: "Jane",
                          class: "woman",
                        },
                        {
                          name: "Jasper",
                          class: "man",
                        },
                        {
                          name: "Emma",
                          class: "woman",
                        },
                        {
                          name: "Julia",
                          class: "woman",
                        },
                        {
                          name: "Jessica",
                          class: "woman",
                        },
                      ],
                    },
                  ],
                },
              ],
            },
          ],
        },
      ],
    };
  },
  props: {
    msg: String,
  },
  mounted: function () {
    this.loaded();
  },
  methods: {
    loaded: function () {
      dTree.init(this.treeData, {
        target: "#graph",
        debug: true,
        height: 800,
        width: 1200,
        callbacks: {
          nodeClick: function (name, extra) {
            console.log(name);
            console.log(extra);
          },
          textRenderer: function (name, extra, textClass) {
            // THis callback is optinal but can be used to customize
            // how the text is rendered without having to rewrite the entire node
            // from screatch.
            if (extra && extra.nickname)
              name = name + " (" + extra.nickname + ")";
            return (
              "<p align='center' class='" + textClass + "'>" + name + "</p>"
            );
          },
          nodeRenderer: function (
            name,
            x,
            y,
            height,
            width,
            extra,
            id,
            nodeClass,
            textClass,
            textRenderer
          ) {
            // This callback is optional but can be used to customize the
            // node element using HTML.
            let node = "";
            node += "<div ";
            node += 'style="height:100%;width:100%;" ';
            node += 'class="' + nodeClass + '" ';
            node += 'id="node' + id + '">\n';
            node += textRenderer(name, extra, textClass);
            node += "</div>";
            return node;
          },
        },
      });
    },
  },
};
</script>

<style scoped>
body {
  font: 10px sans-serif;
}
.linage {
  fill: none;
  stroke: #000;
}
.marriage {
  fill: none;
  stroke: black;
}
.man {
  background-color: lightblue;
  border-style: solid;
  border-width: 1px;
  box-sizing: border-box;
}
.woman {
  background-color: pink;
  border-style: solid;
  border-width: 1px;
  box-sizing: border-box;
}
.emphasis {
  font-style: italic;
}
p {
  padding: 0;
  margin: 0;
}
svg {
  border-style: solid;
  border-width: 1px;
}
</style>

<template>
  <div class="card" :class="{ 'print': cardType === 'print', 'app': cardType === 'app' }">
    <div class="left" :class="{ 'left_letter': cardData.type === 'letter' }">
      <div class="name">{{ name }}</div>
      <div v-if="(cardData.type === 'letter')" class="number"
      :class="{ 'single' : cardData.name.length === 1 }"
      >
        {{ cardData.name[0] }}
        <span>{{ cardData.name[1] || '' }}</span>
      </div>
      <div v-if="(cardData.type != 'letter')" class="cardname">
        <div class="title">{{ cardData.name }}</div>
        <div>{{ cardData.subname }}</div>
      </div>
    </div>
    <div class="right" v-html="MDtoHTML(cardData.text || '')"/>
  </div>
</template>

<script>
import MDtoHTML from "marked";

MDtoHTML.setOptions({
  sanitize: true,
  breaks: true,
  gfm: true
});

export default {
  props: {
    cardData: {
      type: Object,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    cardType: {
      type: String,
      default: 'edit'
    }
  },
  methods: {
    MDtoHTML
  }
};
</script>

<style scoped>
.card {
  height: 452px;
  width: 604px;
  position: relative;
  font-family: "Crimson Text", serif;
  color: black;
  letter-spacing: -0.2px;
  background: linear-gradient(90deg, #a26f3e 50%, #ebd188 50%);
}

.left {
  background-image: url("./asserts/mini/left_ohne.png");
  background-size: cover;
  height: 100%;
  width: 50%;
  float: left;
  position: relative;
}

.card.print {
  padding: 25px;
  margin: 0 auto;
  margin-bottom: 20px;
}

.card.print >>> .left {
  background-image: url("./asserts/full/left_ohne.png");
  border: 1px dashed black;
  border-right: none;
  left: -1px;
}

.left_letter {
  background-image: url("./asserts/mini/left_mit.png");
}

.card.print >>> .left_letter {
  background-image: url("./asserts/full/left_mit.png");
}

.right {
  background-image: url("./asserts/mini/right.png");
  background-size: cover;
  height: calc(100% - 10px);
  overflow: hidden;
  padding: 5px 10px;
  font-size: 13px;
  line-height: 1em;
}

.card.print >>> .right {
  background-image: url("./asserts/full/right.png");
  border: 1px dashed black;
  border-left: none;
}

.card .name {
  font-weight: bold;
  text-align: center;
  position: relative;
  top: 150px;
  font-size: 17px;
  line-height: 1em;
  padding: 0 40px;
}

.card .cardname {
  text-align: center;
  position: relative;
  top: 280px;
  margin: 0 40px;
  line-height: 1em;
}
.card .cardname .title {
  font-weight: bold;
  font-size: 17px;
}

.card .number {
  -webkit-text-stroke: 2px black;
  color: white;

  font-size: 100px;
  position: absolute;
  top: 200px;
  left: 100px;
}

.card .number.single {
    left: 120px;
}

.card .number span {
  font-size: 80px;
  display: inline-block;
  margin-left: -20px;
}

.card >>> hr {
  overflow: visible;
  padding: 0;
  border: none;
  border-top: 1px solid #333;
  border-bottom: 1px solid #333;
  padding-top: 1px;
}

.card >>> p {
  margin: 10px 0;
}

.card >>> ul {
  padding-left: 2rem;
  margin: 0;
}

/* Ansicht für die App */
.card.app {
  background: #ebd188;
  width: auto;
}

.card.app >>> .left{
  display: none;
}

.card.app >>> .right {
  height: 100%;
  overflow: auto;
  font-size: 17px;
}
</style>
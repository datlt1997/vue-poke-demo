<template>
  <h1>Template Component Here...</h1>
  <CardItem v-for="(card, index) in cardsContext" :key="index" />
</template>
<script>
import CardItem from "./CardItem.vue";
export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  name: "InteractScreen",
  components: {
    CardItem,
  },
};
</script>

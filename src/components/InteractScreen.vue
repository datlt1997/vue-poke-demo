<template>
  <div class="screen">
    <div
      class="screen__inner"
      :style="{
        width: `${
          ((((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4 +
            16) *
          Math.sqrt(cardsContext.length)
        }px`,
      }"
    >
      <CardItem
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imageBackGroundUrl="`images/${card}.png`"
        :card="{ index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      />
    </div>
    <!--    <h1>Template Component Here...</h1>-->
  </div>
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
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("Right.....");
        // add class disable reset rules
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableCard();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableCard();
        this.rules = [];

        const disableElements = document.querySelectorAll(
          ".screen .card.card_disable"
        );

        // console.log(disableElements.length, this.cardsContext.length);
        if (
          disableElements &&
          disableElements.length === this.cardsContext.length - 2
        ) {
          console.log(disableElements.length);
          setTimeout(() => {
            this.$emit("onFinish");
          }, 1000);
        }
        console.log(disableElements);
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("wrong.....");

        setTimeout(() => {
          //close two card
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();

          //reset rules
          this.rules = [];
        }, 1000);
      } else {
        return false;
      }
    },
  },
};
</script>
<style scoped>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  /*width: 690px;*/
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>

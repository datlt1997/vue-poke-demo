<template>
  <div
    class="card"
    :class="{ card_disable: isDisable }"
    :style="{
      height: `${(920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16}px`,
      width: `${
        (((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 4
      }px`,
      perspective: `${
        (((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 3) / 2
      }px`,
    }"
  >
    <div
      class="card__inner"
      :class="{ 'is-fipped': isFipped }"
      @click="onToggleFipCard"
    >
      <div class="card__face card__face--font">
        <div
          class="card__content card__content--front"
          :style="{
            backgroundSize: `${
              ((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 0.25
            }px ${
              ((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 0.25
            }px`,
          }"
        ></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content card__content--back"
          :style="{
            backgroundImage: `url(${require('@/assets/' +
              imageBackGroundUrl)})`,
            backgroundSize: `${
              ((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 0.25
            }px ${
              ((920 - 16 * 4) / Math.sqrt(cardsContext.length) - 16) * 0.25
            }px`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageBackGroundUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  name: "CardItem",
  data() {
    return {
      isFipped: false,
      isDisable: false,
    };
  },

  methods: {
    onToggleFipCard() {
      if (this.isDisable) return false;
      this.isFipped = !this.isFipped;
      if (this.isFipped) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFipped = false;
    },
    onEnableDisableCard() {
      this.isDisable = true;
    },
  },
};
</script>

<style scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}

.card__inner.is-fipped {
  transform: rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}

.card__content--front {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  height: 100%;
  width: 100%;
}

.card__content--back {
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(180deg);
}

.card.card_disable .card__inner {
  cursor: default;
}
</style>

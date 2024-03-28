<template>
  <div
    class="card"
    :class="{ disabled: isDisabled }"
    :style="{
      height: `${(660 - 16 * 4) / Math.sqrt(cardcontext.length) - 16}px`,
      width: `${
        (((660 - 16 * 4) / Math.sqrt(cardcontext.length) - 16) * 3) / 4
      }px`,
    }"
  >
    <div class="card_inner" :class="{ fleped: isFleped }" @click="onFleped()">
      <div class="card_face card_face--front">
        <div class="card-content"></div>
      </div>
      <div class="card_face card_face--back">
        <div
          class="card-content"
          :style="{ backgroundImage: `url(${require('@/assets/' + nameImg)})` }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    nameImg: {
      type: String,
      required: true,
    },
    card: {
      type: [Number, Array, Object, String],
    },
    cardcontext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      isFleped: false,
      isDisabled: false,
    };
  },
  methods: {
    onFleped() {
      if (this.isDisabled) return false;
      this.isFleped = !this.isFleped;
      if (this.isFleped) {
        this.$emit("onFlip", this.card);
      }
    },
    onFlipBackCard() {
      this.isFleped = false;
    },
    onDisabledCard() {
      this.isDisabled = true;
    },
  },
};
</script>
<style lang="css" scoped>
.card {
  display: inline-block;
  margin-bottom: 1rem;
  margin-right: 1rem;
  /* width: 90px;
  height: 120px; */
}
.card_inner {
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card.disabled .card_inner {
  cursor: default;
}
.card_inner.fleped {
  transform: rotateY(-180deg);
  /* box-shadow: 1px 6px 53px 28px rgb(255, 255, 30); */
}
.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  box-shadow: 0 3px 10px 3px #3d3b3b;
}
.card_face--front .card-content {
  background: url("../assets/imgs/icon.png") no-repeat center;
  background-size: 100%;
  width: 100%;
  height: 100%;
}
.card_face--back .card-content {
  height: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center center;
}
.card_face--back {
  transform: rotateY(-180deg);
}
</style>

<template>
  <div class="screen">
    <div
      class="screen_inner"
      :style="{
        width: `${
          ((((660 - 16 * 4) / Math.sqrt(cardcontext.length) - 16) * 3) / 4) *
            Math.sqrt(cardcontext.length) +
          16 * Math.sqrt(cardcontext.length)
        }px`,
      }"
    >
      <card-item
        v-for="(card, i) in cardcontext"
        :key="i"
        :ref="`card-${i}`"
        :nameImg="`imgs/i${card}.png`"
        :card="{ i, value: card }"
        @onFlip="checkRule($event)"
        :cardcontext="cardcontext"
      />
    </div>
    <!-- <p>Chơi đc thì chơi ko chơi dc out</p> -->
  </div>
</template>

<script>
import CardItem from "./CardItem.vue";
export default {
  components: {
    CardItem,
  },
  props: {
    cardcontext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  methods: {
    checkRule(value) {
      if (this.rules.length === 2) return false;
      this.rules.push(value); // Thêm 1 pt value vào mảng rules
      // console.log(this.rules);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        // add class 'disabled' to card
        this.$refs[`card-${this.rules[0].i}`][0].onDisabledCard();
        this.$refs[`card-${this.rules[1].i}`][0].onDisabledCard();
        // reset array rules
        this.rules = [];
        // finsh game
        const FinshCard = document.querySelectorAll(".screen .card.disabled");
        if (FinshCard && FinshCard.length === this.cardcontext.length - 2) {
          setTimeout(() => {
            this.$emit("onfinishGame");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          // console.log("wrong");
          // close two card
          this.$refs[`card-${this.rules[0].i}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].i}`][0].onFlipBackCard();

          // reset array rules
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
<style lang="css" scoped>
.screen {
  /* background-color: aqua; */
  background-color: #19283c;
  width: 100%;
  height: 605px;
}
.screen_inner {
  display: flex;
  flex-wrap: wrap;
  margin: 1rem auto;
  padding: 15px 0 0 15px;
}
</style>

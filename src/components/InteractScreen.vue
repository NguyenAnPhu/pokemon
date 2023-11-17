<template>
  <div class="screen">
    <!-- <h1 style="text-align: center">InteractScreen in here</h1> -->

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
      <card-flip
        v-for="(card, index) in cardsContext"
        :key="index"
        :ref="`card-${index}`"
        :imgBackFaceUrl="`images/${card}.png`"
        :card="{ index: index, value: card }"
        :cardsContext="cardsContext"
        @onFlip="checkRule($event)"
      ></card-flip>
    </div>
  </div>
</template>

<script>
import CardFlip from "./Card.vue";
export default {
  components: {
    CardFlip,
  },
  props: {
    cardsContext: {
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
    checkRule(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);

      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("Right");
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisabledMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisabledMode();
        //reset rules []
        this.rules = [];
        //check result
        const disabledElements = document.querySelectorAll(
          ".screen .card.isDisabled"
        );
        console.log(disabledElements);
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onFinish");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value != this.rules[1].value
      ) {
        console.log("Wrong");
        setTimeout(() => {
          // close card
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // reset rules to []
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style lang="css" scoped>
.screen {
  width: 100%;
  min-height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
}
.screen__inner {
  width: calc(424px);
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>

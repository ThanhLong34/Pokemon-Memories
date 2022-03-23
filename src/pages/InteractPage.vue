<template>
  <div class="interact-page page">
    <ul class="card-list" :class="`mode-${modeNumber}`">
      <li class="card-item" v-for="(card, index) in cards" :key="card">
        <CardView
          :ref="`card-${index}`"
          :cardIndex="index"
          :bgImage="card"
          @onFlip="handleCheckTwoCards"
          :isFlipping="isFlipping"
        />
      </li>
    </ul>
  </div>
</template>

<script>
import { shuffle } from "../helpers/functions.js";
import CardView from "../views/CardView.vue";

export default {
  components: {
    CardView,
  },
  props: {
    modeNumber: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      numberOfImage: 64,
      pairCards: [],
      point: 0,
      timeOutFlip: 800,
      isFlipping: false,
    };
  },
  emits: ["onRedirectResult"],
  methods: {
    handleCheckTwoCards(cardValue) {
      this.pairCards.push(cardValue);
      const cards = this.pairCards;
      if (cards.length === 2) {
        this.isFlipping = true;
        if (
          cards[0].value === cards[1].value &&
          cards[0].index !== cards[1].index
        ) {
          // true
          this.point++;
          this.$refs[`card-${cards[0].index}`][0].isDisabled = true;
          this.$refs[`card-${cards[1].index}`][0].isDisabled = true;
        } else {
          // false
          setTimeout(() => {
            this.$refs[`card-${cards[0].index}`][0].isFlip = false;
            this.$refs[`card-${cards[1].index}`][0].isFlip = false;
          }, this.timeOutFlip);
        }
        // reset pair cards
        setTimeout(() => {
          this.pairCards.length = 0;
          this.isFlipping = false;
          console.log(Math.pow(this.modeNumber, 2) / 2);
          if (this.point === Math.pow(this.modeNumber, 2) / 2) {
            this.$emit("onRedirectResult");
          }
        }, this.timeOutFlip + 100);
      }
    },
  },
  computed: {
    cards() {
      const tempArr = [];
      const shuffleCards = shuffle(this.orderCards);
      for (let i = 0; i < Math.pow(this.modeNumber, 2) / 2; i++) {
        tempArr.push(shuffleCards[i]);
      }
      tempArr.push(...tempArr);
      const result = shuffle(tempArr);
      return result;
    },
    orderCards() {
      const result = [];
      for (let i = 1; i <= this.numberOfImage; i++) {
        result.push(i);
      }
      return result;
    },
  },
};
</script>

<style lang="css" scoped>
.interact-page {
  width: 100vw;
  height: 100vh;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.card-list {
  display: grid;
}
.mode-4 {
  grid-template-columns: repeat(4, 140px);
  grid-template-rows: repeat(4, 140px);
  gap: 20px;
}
.mode-6 {
  grid-template-columns: repeat(6, 90px);
  grid-template-rows: repeat(6, 90px);
  gap: 16px;
}
.mode-8 {
  grid-template-columns: repeat(8, 65px);
  grid-template-rows: repeat(8, 65px);
  gap: 14px;
}
.mode-10 {
  grid-template-columns: repeat(10, 56px);
  grid-template-rows: repeat(10, 56px);
  gap: 10px;
}
.card-item {
  width: 100%;
  height: 100%;
}
</style>

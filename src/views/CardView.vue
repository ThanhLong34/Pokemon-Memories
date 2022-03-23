<template>
  <div
    class="card-view"
    :class="{ flip: isFlip, disabled: isDisabled }"
    @click="handleToggleFlip"
  >
    <div class="card-view-inner">
      <div class="card-view-front card-view-face"></div>
      <div
        class="card-view-back card-view-face"
        :style="{
          backgroundImage: `url('${require(`../assets/images/${bgImage}.png`)}')`,
        }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    bgImage: {
      type: [Number, String],
      required: true,
    },
    cardIndex: {
      type: Number,
      required: true,
    },
    isFlipping: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      isFlip: false,
      isDisabled: false,
      card: {
        index: this.cardIndex,
        value: this.bgImage,
      },
    };
  },
  emits: ["onFlip"],
  methods: {
    handleToggleFlip() {
      if (!this.isFlipping) {
        this.isFlip = !this.isFlip;
        this.$emit("onFlip", this.card);
      }
    },
  },
};
</script>

<style lang="css" scoped>
.card-view {
  width: 100%;
  height: 100%;
  background-color: transparent;
  perspective: 600px;
  cursor: pointer;
}
.card-view.disabled {
  pointer-events: none !important;
}
@keyframes matchCardAnimate {
  0% {
    outline-color: transparent;
  }
  75% {
    outline-color: var(--secondary-color);
  }
  100% {
    outline-color: transparent;
  }
}
.card-view.disabled .card-view-back {
  animation: matchCardAnimate ease 1s forwards;
}
.card-view.flip .card-view-inner {
  transform: rotateY(180deg);
}
.card-view-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}
.card-view-face {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
  border-radius: 50%;
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.2);
  background-color: var(--bg-color-light);
  aspect-ratio: 1/1;
  transition: all ease 0.6s;
  outline: 3px solid transparent;
}
.card-view-front {
  background-image: url("../assets/images/icon_front.png");
  background-position: center;
  background-size: 50%;
  background-repeat: no-repeat;
  background-color: rgb(197, 197, 197) !important;
}
.card-view-back {
  transform: rotateY(180deg);
  background-position: center;
  background-size: 65%;
  background-repeat: no-repeat;
}
.card-view-face:hover {
  outline-color: var(--primary-color);
}
.card-view-front:hover {
  transform: scale(1.04);
}
.card-view-back:hover {
  transform: rotateY(180deg) scale(1.04);
}
</style>

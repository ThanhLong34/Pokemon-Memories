<template>
  <div class="main-page page">
    <h3 class="hello">
      Hello, <span class="primary-highlight">{{ username }}</span>
    </h3>
    <h3 class="title">Chọn chế độ trò chơi</h3>
    <div class="mode-list">
      <button
        class="mode-item"
        v-for="(mode, index) in modes"
        :key="index"
        @click="handleChooseMode(mode.number)"
      >
        <span class="mode-item-number">
          {{ mode.number + " x " + mode.number }}
        </span>
        <span class="mode-item-desc">{{ mode.description }}</span>
        <span class="mode-item-icon">{{ mode.icon }}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    username: {
      type: String,
      default: "you",
    },
  },
  data() {
    return {
      modes: [
        { number: 4, description: "Dễ", icon: "😂" },
        { number: 6, description: "Trung bình", icon: "😆" },
        { number: 8, description: "Khó", icon: "😲" },
        { number: 10, description: "Rất khó", icon: "😏" },
      ],
    };
  },
  emits: ["onChooseMode"],
  methods: {
    handleChooseMode(modeNumber) {
      this.$emit("onChooseMode", modeNumber);
    },
  },
};
</script>

<style lang="css" scoped>
.main-page {
  position: relative;
  top: 12px;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.3);
  padding: 25px 60px 40px;
  border-radius: 30px;
  background-color: var(--bg-color-dark);
}
.hello {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: var(--text-color-light);
  text-transform: uppercase;
  text-align: center;
}
.title {
  font-size: 1rem;
  margin-bottom: 1.6rem;
  color: var(--text-color-light);
  text-transform: uppercase;
  text-align: center;
}
.mode-list {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 12px;
}
.mode-item {
  padding: 10px 20px;
  display: block;
  aspect-ratio: 1/1;
  background-color: white;
  border-radius: 16px;
  text-align: center;
  transition: all ease 0.5s;
  border: 3px solid var(--primary-color);
}
.mode-item:hover {
  background-color: var(--primary-color);
  border-color: var(--bg-color-dark);
}
.mode-item span {
  display: block;
}
.mode-item-number {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 6px;
}
.mode-item-desc {
  font-size: 1rem;
  color: rgb(95, 95, 95);
  margin-bottom: 6px;
}
.mode-item-icon {
  font-size: 2rem;
}
</style>

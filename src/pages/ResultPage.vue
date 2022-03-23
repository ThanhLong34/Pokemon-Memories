<template>
  <div class="result-page page">
    <form @submit.prevent="handleRestart">
      <h4 class="title">🎉Chúc mừng👏</h4>
      <h4 class="title">🐱‍🏍Bạn đã hoàn thành trò chơi🌹</h4>
      <p class="para">
        Thời gian hoàn thành:
        <span class="primary-highlight">{{ timeCompleted }}</span
        >s
      </p>
      <button class="submit-btn primary-btn" type="submit">Chơi lại</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    timeCompleted: {
      type: Number,
      required: true,
    },
  },
  emits: ["onRestart"],
  methods: {
    handleRestart() {
      this.$emit("onRestart");
    },
  },
};
</script>

<style lang="css" scoped>
.result-page {
  display: flex;
  align-items: center;
  justify-content: center;
}
form {
  position: relative;
  top: -3rem;
  padding: 40px;
  border-radius: 30px;
  box-shadow: 0 3px 20px rgba(0, 0, 0, 0.3);
  background-color: var(--bg-color-dark);
  color: var(--text-color-light);
}
.title {
  font-size: 1.4rem;
  text-align: center;
  text-transform: uppercase;
  margin: 0.5rem 0;
}
.para {
  text-align: center;
  margin-top: 1.2rem;
  font-size: 1.4rem;
}
.submit-btn {
  display: block;
  margin: 1.6rem auto 0;
  font-size: 1.2rem;
  border-radius: 25px;
}
</style>

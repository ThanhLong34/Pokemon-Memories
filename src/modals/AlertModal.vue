<template>
  <div class="overlay">
    <form @submit.prevent="handleAccept">
      <h5 class="title">Cảnh báo</h5>
      <p class="content">{{ content }}</p>
      <button class="accept-btn" type="submit">OK</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    content: {
      type: String,
      required: true,
    },
  },
  emits: ["onAccept"],
  methods: {
    handleAccept() {
      this.$emit("onAccept");
    },
  },
};
</script>

<style lang="css" scoped>
.overlay {
  position: fixed;
  inset: 0;
  background-color: var(--overlay);
  display: flex;
  align-items: center;
  justify-content: center;
}
@keyframes showFormAnimate {
  0% {
    opacity: 0.6;
    top: -8rem;
  }
  100% {
    opacity: 1;
    top: -5rem;
  }
}
form {
  padding: 20px;
  border-radius: 25px;
  box-shadow: 2px 2px 30px rgba(0, 0, 0, 0.2);
  background-color: white;
  position: relative;
  animation: showFormAnimate ease 0.6s forwards;
}
.title {
  margin-bottom: 1.2rem;
  text-align: center;
  font-size: 1.2rem;
  color: var(--text-color-dark);
}
.content {
  font-size: 1rem;
  margin-bottom: 1rem;
}
.accept-btn {
  margin: 0 auto;
  display: block;
}
</style>

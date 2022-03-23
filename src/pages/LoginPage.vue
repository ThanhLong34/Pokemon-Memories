<template>
  <div class="login-page page">
    <form @submit.prevent="handleSubmit">
      <h2 class="title">Đăng nhập</h2>
      <input
        class="name-input"
        type="text"
        placeholder="Nhập tên của bạn..."
        v-model="username"
      />
      <button class="submit-btn primary-btn" type="submit">Enter</button>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      error: 0,
    };
  },
  emits: ["onSubmit"],
  methods: {
    handleSubmit() {
      const username = this.username;
      let error = this.error;
      if (!username) {
        // username is empty
        error = 1;
      } else if (username.length > 12) {
        // username is gretter than 12 characters
        error = 2;
      }
      this.$emit("onSubmit", username, error);
    },
  },
};
</script>
<style lang="css" scoped>
@keyframes formAnimate {
  0% {
    border-radius: 40px 40px 180px 180px;
  }
  25% {
    border-radius: 63px 100px 104px 140px;
  }
  50% {
    border-radius: 124px 79px 219px 165px;
  }
  75% {
    border-radius: 97px 129px 89px 207px;
  }
  100% {
    border-radius: 40px 40px 180px 180px;
  }
}
form {
  padding: 1.6rem 2.8rem 2.8rem;
  background-color: var(--bg-color-dark);
  border-radius: 40px 40px 180px 180px;
  box-shadow: 2px 2px 20px rgba(0, 0, 0, 0.1);
  position: relative;
  top: -2rem;
  animation: formAnimate linear 30s infinite;
}
.title {
  font-size: 1.6rem;
  text-transform: uppercase;
  text-align: center;
  margin-bottom: 1rem;
  color: var(--secondary-color);
}
.name-input {
  display: block;
  margin: 1.6rem auto 2rem;
  font-size: 1.2rem;
  border-radius: 25px;
}
.submit-btn {
  padding: 0.6rem 2rem;
  display: block;
  margin: 0 auto;
}
</style>

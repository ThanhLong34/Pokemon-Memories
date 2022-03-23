<template>
  <!-- components -->
  <HeaderComponent v-if="show.showHeader" />
  <!-- pages -->
  <LoginPage v-if="page === pages.login" @onSubmit="handleSubmit" />
  <MainPage
    v-if="page === pages.main"
    :username="username"
    @onChooseMode="handleChooseMode"
  />
  <InteractPage
    v-if="page === pages.interact"
    :modeNumber="modeNumber"
    @onRedirectResult="handleRedirectResultPage"
  />
  <ResultPage
    v-if="page === pages.result"
    :timeCompleted="timeCompleted"
    @onRestart="handleRestart"
  />
  <!-- components -->
  <FooterComponent v-if="show.showFooter" />
  <!-- modals -->
  <AlertModal
    v-if="isShowAlert"
    :content="contentAlert"
    @onAccept="handleCloseAlert"
  />
</template>

<script>
// components
import HeaderComponent from "./components/HeaderComponent.vue";
import FooterComponent from "./components/FooterComponent.vue";

// modals
import AlertModal from "./modals/AlertModal.vue";

// pages
import LoginPage from "./pages/LoginPage.vue";
import MainPage from "./pages/MainPage.vue";
import InteractPage from "./pages/InteractPage.vue";
import ResultPage from "./pages/ResultPage.vue";

export default {
  components: {
    // components
    HeaderComponent,
    FooterComponent,
    // modals
    AlertModal,
    // pages
    LoginPage,
    MainPage,
    InteractPage,
    ResultPage,
  },
  data() {
    return {
      pages: {
        login: "login",
        main: "main",
        interact: "interact",
        result: "result",
      },
      page: "login",
      username: "",
      isShowAlert: false,
      contentAlert: "",
      show: {
        showHeader: true,
        showFooter: true,
      },
      errors: {
        usernameIsEmpty: 1,
        usernameGretterThan_12_Characters: 2,
      },
      modeNumber: 0,
      timeCompleted: 0,
      timeCompletedInterval: null,
    };
  },
  methods: {
    handleSubmit(username, error) {
      switch (error) {
        case this.errors.usernameIsEmpty: {
          this.isShowAlert = true;
          this.contentAlert = "Bạn chưa nhập tên!";
          break;
        }
        case this.errors.usernameGretterThan_12_Characters: {
          this.isShowAlert = true;
          this.contentAlert = "Tên không được vượt quá 12 ký tự!";
          break;
        }
        default: {
          this.page = this.pages.main;
          this.username = username;
          break;
        }
      }
    },
    handleCloseAlert() {
      this.isShowAlert = false;
    },
    handleChooseMode(modeNumber) {
      this.modeNumber = modeNumber;
      this.page = this.pages.interact;
      this.show.showHeader = false;
      this.show.showFooter = false;
      // set time completed
      this.timeCompletedInterval = setInterval(() => {
        this.timeCompleted += 1;
      }, 1000);
    },
    handleRedirectResultPage() {
      this.page = this.pages.result;
      this.show.showHeader = true;
      this.show.showFooter = true;
      if (this.timeCompletedInterval) {
        clearInterval(this.timeCompletedInterval);
      }
    },
    handleRestart() {
      this.timeCompleted = 0;
      this.page = this.pages.main;
    },
  },
};
</script>

<template>
  <div class="auth-form row">
    <div class="auth-form__left col p-4 d-none d-md-block"></div>

    <div class="auth-form__right d-flex align-items-center col p-md-5 p-3">
      <transition name="fade" mode="out-in">
        <div key="1" v-if="!isTryToLogin" class="flex-fill">
          <img
            class="auth-form__logo"
            src="https://static.tildacdn.com/tild6464-6266-4561-b833-386137663636/05d8f8a8-e392-4928-b.svg"
          />

          <h5 class="mt-4">Войти в аккаунт</h5>

          <form>
            <input
              :disabled="loading"
              v-model="login"
              type="text"
              class="form-control mt-4"
              placeholder="Логин"
            />

            <input
              :disabled="loading"
              v-model="password"
              type="password"
              class="form-control mt-3"
              placeholder="Пароль"
            />

            <button
              :disabled="loading || !isValid"
              class="btn btn-primary mt-3 form-control"
              type="submit"
              @click="auth"
            >
              <span
                v-if="loading"
                class="spinner-border spinner-border-sm"
                role="status"
                aria-hidden="true"
              />

              Авторизоваться
            </button>
          </form>

          <div class="d-flex justify-content-between mt-4">
            <a class="small text-muted" href="#!">Забыли пароль?</a>
            <a class="small text-muted" href="#!">Регистрация</a>
          </div>
        </div>

        <div key="2" v-else class="flex-fill">
          <h3>{{ authText }}</h3>
          <button
            :disabled="loading"
            class="btn btn-primary mt-3 form-control"
            type="submit"
            @click="back"
          >
            Назад
          </button>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "AuthFrom",

  data: () => ({
    login: "",
    password: "",
    loading: false,
    isCorrect: false,
    isTryToLogin: false,
    isValid: false,
  }),

  computed: {
    authText() {
      return this.isTryToLogin && this.isCorrect
        ? "Вы успешно авторизовались"
        : this.isTryToLogin && !this.isCorrect
        ? "Неверный логин или пароль"
        : "";
    },
  },

  methods: {
    auth() {
      this.loading = true;

      if (this.checkAuth()) {
        this.isCorrect = true;
      }

      setTimeout(() => {
        this.isTryToLogin = true;
        this.loading = false;
      }, 2000);
    },

    checkAuth() {
      const users = [{ login: "admin", passowd: "password" }];

      return Boolean(
        users.find(
          (item) => item.login == this.login && item.passowd == this.password
        )
      );
    },

    back() {
      this.isTryToLogin = false;
      this.isCorrect = false;
      this.login = "";
      this.password = "";
    },
  },

  watch: {
    login() {
      this.isValid = this.login.length && this.password.length;
    },

    password() {
      this.isValid = this.login.length && this.password.length;
    },
  },
};
</script>

<style lang="scss">
.auth-form {
  width: 100%;
  max-width: 800px;
  min-height: 445px;
  background-color: #ffffff;
  border-radius: 20px;
  overflow: hidden;

  @media (min-width: 768px) {
    box-shadow: 20px 20px 60px #bebebe, -20px -20px 60px #ffffff;
    width: 80%;
  }

  &__left {
    background-image: url("https://static.tildacdn.com/tild3137-3264-4862-b735-326636306237/Lemon_Pie.svg");
    background-repeat: no-repeat;
    background-color: #ffce2a;
    background-size: contain;
    background-origin: content-box;
    background-position: center;
    padding-right: 0;
  }

  &__right {
    @media (min-width: 768px) {
      min-width: 400px;
    }
  }

  &__logo {
    width: 200px;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
}
</style>

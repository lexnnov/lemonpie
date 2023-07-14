<template>
  <div class="main-page d-flex align-items-center justify-content-center">
    <auth-from />
  </div>
</template>

<script>
import AuthFrom from "../components/AuthFrom.vue";

export default {
  name: "IndexPage",
  components: {
    AuthFrom,
  },
};
</script>

<style>
html,
body,
#__nuxt,
#__layout {
  height: 100% !important;
  width: 100% !important;
}

.main-page {
  height: 100%;
}

.btn-primary,
.btn-primary:hover,
.btn-primary:active,
.btn-primary:visited {
  background-color: #ffce2a !important;
  color: black;
  border-color: #ffce2a;
}

.btn-primary.btn:disabled {
  color: black;
  border-color: #ffce2a;
}
</style>

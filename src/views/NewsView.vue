<template>
  <div class="container">
    <div class="text-center mb-5">
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/logo.svg"
        width="125"
        height="125"
      />
      <h1>Top Stories</h1>
    </div>
  </div>


  <NewsList />
</template>

<script>
import NewsList from "../components/NewsList.vue";

export default {
  components: { NewsList }
};
</script>
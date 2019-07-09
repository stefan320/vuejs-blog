<template>
  <header class="pd-3">
    <h1 class="header--title">{{title}}</h1>
  </header>
</template>


<script>
export default {
  name: "Header",
  data() {
    return {
      title: "Dorado Blog"
    };
  }
};
</script>


<style>
header {
  background-color: #52616a;
  text-align: center;
}
.header--title {
  font-size: 3.5rem;
  font-weight: 500;
  margin: 0 auto;
  padding: 4rem 0;
  color: #f0f5f9;
}
</style>

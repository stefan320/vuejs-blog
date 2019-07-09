<template>
  <div id="app">
    <Header />
    <Blogs />
  </div>
</template>

<script>
import Header from "./Header";
import Blogs from "./Blogs";
export default {
  name: "app",
  components: {
    Header,
    Blogs
  },
  data() {
    return {};
  }
};
</script>

<style>
html {
  font-size: 10px;
  max-width: 100%;
}
* {
  font-family: "Open Sans", sans-serif;
  margin: 0;
  padding: 0;
}

.pd-3 {
  padding: 0 3rem;
}
</style>

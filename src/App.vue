<template>
  <div id="app">
    <appHeader />
    <router-view></router-view>
  </div>
</template>

<script>
import addBlog from "./components/addBlog.vue";
import showBlogs from "./components/showBlogs.vue";
import listBlogs from "./components/listBlogs.vue";
import header from "./components/header.vue";

export default {
  components: {
    addBlog: addBlog,
    showBlogs: showBlogs,
    listBlogs: listBlogs,
    appHeader: header
  },
  data() {
    return {};
  },
  methods: {}
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Nunito SemiBold";
}
</style>

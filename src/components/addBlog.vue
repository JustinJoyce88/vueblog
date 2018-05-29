<template>
  <div id="addBlog">
    <h2 v-if="!submitted">Add a new blog post</h2>
    <form v-if="!submitted">
      <label>Blog Title</label>
      <input type="text" v-model.lazy="blog.title" required />
      <label>Blog Content:</label>
      <textarea v-model.lazy="blog.content" name="" id="" cols="30" rows="10"></textarea>
      <div id="checkboxes">
        <label>Front End</label>
        <input type="checkbox" value="Front End" v-model="blog.categories" />
        <label>Back End</label>
        <input type="checkbox" value="Back End" v-model="blog.categories" />
        <label>Full Stack</label>
        <input type="checkbox" value="Full Stack" v-model="blog.categories" />
        <label>Other</label>
        <input type="checkbox" value="Other" v-model="blog.categories" />
      </div>
      <label>Author:</label>
      <select v-model="blog.author">
        <option v-for="author in authors" :key="author.id">{{author}}</option>
      </select>
      <button v-on:click.prevent="postBlog">Add Blog</button>
    </form>
    <div v-if="submitted">
      <h3>Your post has been submitted!</h3>
    </div>
    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog title: {{blog.title}}</p>
      <p>Blog Content:</p>
      <p>{{blog.content}}</p>
      <p>Blog Categories:</p>
      <ul>
        <li v-for="category in blog.categories" :key="category.id">{{category}}</li>
      </ul>
      <p>Author: {{blog.author}}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blog: {
        title: "",
        content: "",
        author: "",
        categories: []
      },
      authors: ["Justin Joyce", "Bobby McBobbins", "Ted"],
      submitted: false
    };
  },
  methods: {
    postBlog() {
      this.$http
        .post("https://vue-blog-c448e.firebaseio.com/posts.json", this.blog)
        .then(function() {
          this.submitted = true;
        });
    }
  }
};
</script>

<style scoped>
#addBlog {
  margin: 20px auto;
  max-width: 500px;
}
label {
  display: block;
  margin: 20px 0 10px;
}
input[type="text"],
textarea {
  display: block;
  width: 100%;
  padding: 8px;
}
#preview {
  padding: 10px 20px;
  border: 1px dotted #ccc;
  margin: 30px 0;
}
h3 {
  margin-top: 10px;
}
#checkboxes input {
  display: inline-block;
  margin-right: 10px;
}
#checkboxes label {
  display: inline-block;
}
</style>
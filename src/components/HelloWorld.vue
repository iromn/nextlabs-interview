<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      This project consists of all the tasks that was given to me. <br>
      I have divided each task into 3 separate pages.
    </p>
    <h3 style="margin-bottom: 10px">You can navigate to each page using the below links <br>
    or you can use the links in the navbar above
    </h3>
    <h5 @click="navigate('/pricing')">Pricing</h5>
    <h5 @click="navigate('/folderStructure')">Folder Structure</h5>
    <h5 @click="navigate('/lazyLoading')">Lazy Loading</h5>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    navigate(path){
      this.$router.push(path);
    }
  },
}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
h5 {
  color: #42b983;
}
h5:hover {
  cursor: pointer;
  text-decoration: underline;
}
</style>

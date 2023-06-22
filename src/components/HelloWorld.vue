<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      This project consists of all the tasks that was given to me. <br />
      I have divided each task into 3 separate pages.
    </p>
    <h3 style="margin-bottom: 10px">
      You can navigate to each page using the below links <br />
      or you can use the links in the navbar above
    </h3>
    <div style="display: flex; flex-direction: column; align-items: center;">
      <label class="link page-link" @click="navigate('/pricing')"
        >Pricing</label
      >
      <label class="link page-link" @click="navigate('/folderStructure')"
        >Folder Structure</label
      >
      <label class="link page-link" @click="navigate('/lazyLoading')"
        >Lazy Loading</label
      >
    </div>

    <p>
      <label style="font-weight: bold">Note:</label> You can go to the
      <label class="link" @click="navigate('APIfetch')"
        >Maakeetoo API Fetch</label
      >
      page to preview the data store in the API that was provided
    </p>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  methods: {
    navigate(path) {
      this.$router.push(path);
    },
  },
};
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
.link {
  color: #42b983;
}
.link:hover {
  cursor: pointer;
  text-decoration: underline;
}
.page-link {
  font-size: 30px;
}
</style>

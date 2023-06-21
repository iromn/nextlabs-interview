<template>
    <div class="d-flex flex-column flex-md-row align-items-center px-md-4 mb-3 bg-white border-bottom box-shadow">
      <h5 class="my-0 mr-md-auto font-weight-normal links" @click="navigate('/')">Next Labs</h5>
      <nav class="my-2 my-md-0 mr-md-3">
        <label class="p-2 text-dark links" @click="navigate('/pricing')">Pricing </label>
        <label class="p-2 text-dark links" @click="navigate('/folderStructure')">Folder Structure</label>
        <label class="p-2 text-dark links" @click="navigate('/lazyLoading')">Lazy Loading</label>
      </nav>
      <a class="btn btn-outline-primary" href="https://getbootstrap.com/docs/4.0/examples/pricing/#">Sign up</a>
    </div>
</template>
<script>
export default {
  data() {
    return {

    };
  },
  methods: {
    navigate(path){
      this.$router.push(path);
    }
  },
}
</script>
<style scoped>
.links{
  font-weight: bold;
}
.links:hover{
  cursor: pointer;
  text-decoration: underline;
}
</style>
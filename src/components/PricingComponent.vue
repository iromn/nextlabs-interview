<template>
  <div class="pricing-header px-3 py-3 pt-md-5 pb-md-4 mx-auto text-center">
    <div v-if="showPopUp">
      <PopUp @close="hidePopUp"></PopUp>
      <div class="overlay" @click="togglePopUp" ></div>
    </div>
    <h1 class="display-4">Pricing</h1>
    <p class="lead">
      Quickly build an effective pricing table for your potential customers with
      this Bootstrap example. It's built with default Bootstrap components and
      utilities with little customization.
    </p>
  </div>

  <div class="container">
    <div class="card-deck mb-3 text-center">
      <div class="card mb-4 box-shadow">
        <div class="card-header">
          <h4 class="my-0 font-weight-normal">Free</h4>
        </div>
        <div class="card-body">
          <h1 class="card-title pricing-card-title">
            $0 <small class="text-muted">/ mo</small>
          </h1>
          <ul class="list-unstyled mt-3 mb-4">
            <li>10 users included</li>
            <li>2 GB of storage</li>
            <li>Email support</li>
            <li>Help center access</li>
          </ul>
          <button
            type="button"
            class="btn btn-lg btn-block btn-outline-primary"
            @click="togglePopUp"
          >
            Sign up for free
          </button>
        </div>
      </div>
      <div class="card mb-4 box-shadow">
        <div class="card-header">
          <h4 class="my-0 font-weight-normal">Pro</h4>
        </div>
        <div class="card-body">
          <h1 class="card-title pricing-card-title">
            $15 <small class="text-muted">/ mo</small>
          </h1>
          <ul class="list-unstyled mt-3 mb-4">
            <li>20 users included</li>
            <li>10 GB of storage</li>
            <li>Priority email support</li>
            <li>Help center access</li>
          </ul>
          <button type="button" class="btn btn-lg btn-block btn-primary">
            Get started
          </button>
        </div>
      </div>
      <div class="card mb-4 box-shadow">
        <div class="card-header">
          <h4 class="my-0 font-weight-normal">Enterprise</h4>
        </div>
        <div class="card-body">
          <h1 class="card-title pricing-card-title">
            $29 <small class="text-muted">/ mo</small>
          </h1>
          <ul class="list-unstyled mt-3 mb-4">
            <li>30 users included</li>
            <li>15 GB of storage</li>
            <li>Phone and email support</li>
            <li>Help center access</li>
          </ul>
          <button type="button" class="btn btn-lg btn-block btn-primary">
            Contact us
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import PopUp from "./PopUpModal.vue";
export default {
  components: {
    PopUp,
  },
  data() {
    return {
      showPopUp: false,
    };
  },
  methods: {
    togglePopUp() {
      this.showPopUp = !this.showPopUp;
    },
    hidePopUp() {
      this.showPopUp = false;
    },
  },
};
</script>
<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 5;
}

.popup-form {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 6;
}
</style>
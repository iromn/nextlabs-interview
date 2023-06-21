<template>
  <div class="popup-form">
    <form v-on:submit.prevent="handleSubmit">
      <button class="close-btn" @click.prevent="$emit('close')">
        <span class="close-icon">&times;</span>
      </button>
      <div class="slidecontainer">
        <input
          type="range"
          min="1"
          max="40"
          value="1"
          class="slider"
          id="myRange"
        />
        <p>Users: <span id="sliderValue"></span></p>
      </div>
      <div class="input-holder">
        <label for="firstname" class="label">Name:</label>
        <input
          class="input-field"
          type="text"
          id="firstname"
          v-model="form.name"
          name="firstname"
          required
        />
      </div>
      <div class="input-holder">
        <label for="email" class="label">Email:</label>
        <input
          class="input-field"
          type="email"
          id="email"
          v-model="form.email"
          name="Email"
          required
        />
      </div>
      <div class="input-holder">
        <label for="message" class="label">Comment:</label>
        <textarea
          class="input-field"
          id="message"
          name="firstname"
          v-model="form.comments"
          rows="4"
          required
        ></textarea>
      </div>

      <button class="btn btn-success" type="submit">Submit</button>
      <div class="card-holder container">
        <div class="card-deck text-center">
          <div id="free" class="card highlight mb-4 box-shadow">
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
            </div>
          </div>
          <div id="pro" class="card mb-4 box-shadow">
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
            </div>
          </div>
          <div id="enterprise" class="card mb-4 box-shadow">
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
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      form: {
        name: "",
        email: "",
        comments: "",
      },
    };
  },
  mounted() {
    var slider = document.getElementById("myRange");
    var output = document.getElementById("sliderValue");
    output.innerHTML = slider.value;

    slider.oninput = function () {
      output.innerHTML = this.value;
      var free = document.getElementById("free");
      var pro = document.getElementById("pro");
      var enterprise = document.getElementById("enterprise");
      if(this.value<20){
        free.classList.add('highlight');
        pro.classList.remove('highlight');
        enterprise.classList.remove('highlight');
        free.classList.remove('box-shadow');
        pro.classList.add('box-shadow');
        enterprise.classList.add('box-shadow');
      }
      else if(this.value>=20 && this.value<30){
        free.classList.remove('highlight');
        pro.classList.add('highlight');
        enterprise.classList.remove('highlight');
        free.classList.add('box-shadow');
        pro.classList.remove('box-shadow');
        enterprise.classList.add('box-shadow');
      }
      else if(this.value>=30 && this.value<=40){
        free.classList.remove('highlight');
        pro.classList.remove('highlight');
        enterprise.classList.add('highlight');
        free.classList.add('box-shadow');
        pro.classList.add('box-shadow');
        enterprise.classList.remove('box-shadow');
      }
    };
  },
  methods: {
    handleSubmit() {
      const formData = new FormData();
      formData.append("firstname", this.form.name);
      formData.append("email", this.form.email);
      formData.append("message", this.form.comments);
      axios
        .post("https://forms.maakeetoo.com/formapi/159", formData, {
          headers: {
            "Content-Type": "multipart/form-data",
            // "Access-Control-Allow-Origin": "*",
          },
        })
        .then((response) => {
          console.log(`Status code: ${response.status}`);
          alert("created successfully");
          this.$emit("close");
          console.log(`Response data: ${response.data}`);
        })
        .catch((error) => {
          console.error(`Error making POST request: ${error}`);
        });
    },
  },
};
</script>
<style scoped>
.highlight{
  box-shadow: 0 0 10px #007bff;
}
.slidecontainer {
  width: 100%;
}

.card-holder{
  padding-top: 30px;
}

.slider {
  -webkit-appearance: none;
  width: 100%;
  height: 15px;
  border-radius: 5px;
  background: #d3d3d3;
  outline: none;
  opacity: 0.7;
  -webkit-transition: 0.2s;
  transition: opacity 0.2s;
}

.slider:hover {
  opacity: 1;
}

.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: #04aa6d;
  cursor: pointer;
}

.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: #04aa6d;
  cursor: pointer;
}
.popup-form form {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.input-holder {
  display: flex;
  flex-wrap: wrap;
}
.input-holder .label{
  flex: 0 0 20%;
}
.input-holder .input-field{
  flex: 0 0 80%;
  margin-bottom: 10px;
  box-sizing: border-box;
}

.popup-form .close-btn {
  background-color: #eb0e0e;
  color: white;
  border: none;
  padding: 0px 10px;
  border-radius: 50%;
  cursor: pointer;
  position: absolute;
  top: -15px;
  right: -15px;
}

.popup-form .close-btn:hover {
  background-color: #3e8e41;
}
.popup-form {
  position: relative; /* Add position property to set the context for absolute position */
}
.close-btn {
  position: absolute;
  top: 0;
  right: 0;
  padding: 0.5em;
  background-color: transparent;
  border: none;
  cursor: pointer;
}
.close-icon {
  font-size: 1.5em;
  color: rgb(255, 255, 255);
}
</style>
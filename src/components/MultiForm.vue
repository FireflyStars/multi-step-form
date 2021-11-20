<template>
  <div class="container-fluid">
    <div class="multi-step-container custom-bg-color">
      <div class="multi-step-header custom-border-bottom">
        <h1 class="text-white">Multi Step Form</h1>
      </div>
      <div class="multi-step-body d-flex flex-wrap">
        <div class="multi-step-nav-container col-md-4 p-0">
          <ul class="multi-step-nav pl-0 m-0 h-100">
            <li class="multi-step-nav-item">
                <div class="multi-step-nav-item-text col-md-10 d-flex align-items-center flex-wrap">
                  <p class="m-0 text-white w-100">Your Name</p>
                  <p class="m-0 text-gray w-100">Browse and Upload</p>
                </div>
                <div @click="goToStep(1)" class="multi-step-nav-item-icon col-md-2 d-flex align-items-center justify-content-center">
                  <b-icon icon="person" font-scale="3" class="rounded-circle progressbar-icon-bg p-2" :class="currentStep == 1 ? 'active' : currentStep > 1 ? 'passed' : ''" variant="white"></b-icon>
                </div>
            </li>
            <li class="multi-step-nav-item">
                <div class="multi-step-nav-item-text col-md-10 d-flex align-items-center flex-wrap">
                  <p class="m-0 text-white w-100">Describes</p>
                  <p class="m-0 text-gray w-100">Browse and Upload</p>
                </div>
                <div @click="goToStep(2)" class="multi-step-nav-item-icon col-md-2 d-flex align-items-center justify-content-center">
                  <b-icon icon="globe" font-scale="3" class="rounded-circle progressbar-icon-bg p-2" :class="currentStep == 2 ? 'active' :  currentStep > 2 ? 'passed' : ''" variant="white"></b-icon>
                </div>
            </li>
            <li class="multi-step-nav-item">
                <div class="multi-step-nav-item-text col-md-10 d-flex align-items-center flex-wrap">
                  <p class="m-0 text-white w-100">Services</p>
                  <p class="m-0 text-gray w-100">Browse and Upload</p>
                </div>
                <div @click="goToStep(3)" class="multi-step-nav-item-icon col-md-2 d-flex align-items-center justify-content-center">
                  <b-icon icon="gift-fill" font-scale="3" class="rounded-circle progressbar-icon-bg p-2" :class="currentStep == 3 ? 'active' :  currentStep > 3 ? 'passed' : ''" variant="white"></b-icon>
                </div>
            </li>
            <li class="multi-step-nav-item">
              <div class="multi-step-nav-item-text col-md-10 d-flex align-items-center flex-wrap">
                <p class="m-0 text-white w-100">Budget</p>
                <p class="m-0 text-gray w-100">Browse and Upload</p>
              </div>
              <div @click="goToStep(4)" class="multi-step-nav-item-icon col-md-2 d-flex align-items-center justify-content-center">
                <b-icon icon="peace" font-scale="3" class="rounded-circle progressbar-icon-bg p-2" :class="currentStep == 4 ? 'active' :  currentStep > 4 ? 'passed' : ''" variant="white"></b-icon>
              </div>
            </li>
            <li class="multi-step-nav-item">
              <div class="multi-step-nav-item-text col-md-10 d-flex align-items-center flex-wrap">
                <p class="m-0 text-white w-100">Complete</p>
                <p class="m-0 text-gray w-100">Browse and Upload</p>
              </div>
              <div @click="goToStep(5)" class="multi-step-nav-item-icon col-md-2 d-flex align-items-center justify-content-center">
                <b-icon icon="trophy-fill" font-scale="3" class="rounded-circle progressbar-icon-bg p-2" :class="currentStep == 5 ? 'active' : ''" variant="white"></b-icon>
              </div>
            </li>
          </ul>
        </div>
        <div class="multi-step-content col-md-8">
          <b-form @submit="onSubmit" class="multi-step-form">
            <div class="multi-step-item" v-show="currentStep == 1">
              <div class="multi-step-item-header custom-border-bottom">
                <label class="text-gray">Step {{ currentStep }} / {{ stepCount }}</label>
                <h2 class="text-white">Let's Start with your name</h2>
                <label class="text-gray">Please fill in</label>
              </div>
              <div class="multi-step-item-content">
                <b-form-group
                  id="input-group-name"
                  label="Enter your name:"
                  label-class="text-white"
                  label-for="name"
                >
                  <b-form-input
                    id="name"
                    v-model="form.email"
                    type="text"
                    placeholder="Enter Name"
                    required
                  ></b-form-input>
                </b-form-group>
                <div class="d-flex justify-content-end">
                  <b-button type="button" class="custom-btn next-btn" @click="goToStep(2)">Next Step</b-button>    
                </div>
              </div>
            </div>
            <div class="multi-step-item" v-show="currentStep == 2">
              <div class="multi-step-item-header custom-border-bottom">
                <label class="text-gray">Step {{ currentStep }} / {{ stepCount }}</label>
                <h2 class="text-white">What best describes you?</h2>
                <label class="text-gray">Please let us know what type of business describes you</label>
              </div>
              <div class="multi-step-item-content">
                <div class="custom-select-container">
                  <input type="hidden" name="description" v-model="form.description">
                  <div class="custom-select-item d-flex" :class="form.description == 1 ? 'active' : ''" @click="changeDescription(description[0])">
                    <div class="custom-select-item-icon">
                      <b-icon icon="life-preserver" font-scale="4" class="rounded-circle transparent-bg p-3" variant="white"></b-icon>
                    </div>
                    <div class="custom-select-item-text pl-3">
                      <p class="text-white m-0 w-100">New Business</p>
                      <p class="text-gray m-0 w-100">Started trading within last 12 month</p>
                    </div>
                  </div>
                  <div class="custom-select-item d-flex" :class="form.description == 2 ? 'active' : ''" @click="changeDescription(description[1])">
                    <div class="custom-select-item-icon">
                      <b-icon icon="slack" font-scale="4" class="rounded-circle transparent-bg p-3" variant="white"></b-icon>
                    </div>
                    <div class="custom-select-item-text pl-3">
                      <p class="text-white m-0 w-100">Exsiting Business</p>
                      <p class="text-gray m-0 w-100">Have been operating beyond 12 month</p>
                    </div>
                  </div>
                </div>
                <div class="d-flex justify-content-end">
                  <b-button type="button" class="custom-btn previous-btn" @click="goToStep(1)">Back</b-button>
                  <b-button type="button" class="custom-btn next-btn" @click="goToStep(3)">Next Step</b-button>    
                </div>
              </div>
            </div>
            <div class="multi-step-item" v-show="currentStep == 3">
              <div class="multi-step-item-header custom-border-bottom">
                <label class="text-gray">Step {{ currentStep }} / {{ stepCount }}</label>
                <h2 class="text-white">What services are you looking for?</h2>
                <label class="text-gray">Please let us know what type of business describes you</label>
              </div>
              <div class="multi-step-item-content">
                <div class="custom-select-container">
                  <input type="hidden" name="business" v-model="form.service">
                  <div class="custom-select-item d-flex"  :class="form.service == 1 ? 'active' : ''" @click="changeService(service[0])">
                    <div class="custom-select-item-icon">
                      <b-icon icon="shop" font-scale="4" class="rounded-circle transparent-bg p-3" variant="white"></b-icon>
                    </div>
                    <div class="custom-select-item-text pl-3">
                      <p class="text-white m-0 w-100">Website Development</p>
                      <p class="text-gray m-0 w-100">Development of Webflow Website</p>
                    </div>
                  </div>
                  <div class="custom-select-item d-flex" :class="form.service == 2 ? 'active' : ''" @click="changeService(service[1])">
                    <div class="custom-select-item-icon">
                      <b-icon icon="flower1" font-scale="4" class="rounded-circle transparent-bg p-3" variant="white"></b-icon>
                    </div>
                    <div class="custom-select-item-text pl-3">
                      <p class="text-white m-0 w-100">Exsiting Business</p>
                      <p class="text-gray m-0 w-100">Development of Website Design</p>
                    </div>
                  </div>
                </div>
                <div class="d-flex justify-content-end">
                  <b-button type="button" class="custom-btn previous-btn" @click="goToStep(2)">Back</b-button>
                  <b-button type="button" class="custom-btn next-btn" @click="goToStep(4)">Next Step</b-button>    
                </div>
              </div>
            </div>
            <div class="multi-step-item" v-show="currentStep == 4">
              <div class="multi-step-item-header custom-border-bottom">
                <label class="text-gray">Step {{ currentStep }} / {{ stepCount }}</label>
                <h2 class="text-white">Please Select your budget?</h2>
                <label class="text-gray">Please let us know the budget of your project</label>
              </div>
              <div class="multi-step-item-content">
                    <Slider
                      min="5000"
                      max="25000"
                      step = "1000"
                      v-model="form.budget"
                      :trackBgColor = "'#2b2d68'"
                      :trackColor = "'#25cd89'"
                      :labelSymbol = "'$'"
                      ref="customSlider"
                    ></Slider>
                <div class="d-flex justify-content-end">
                  <b-button type="button" class="custom-btn previous-btn" @click="goToStep(3)">Back</b-button>
                  <b-button type="button" class="custom-btn next-btn" @click="goToStep(5)">Next Step</b-button>    
                </div>
              </div>
            </div>
            <div class="multi-step-item" v-show="currentStep == 5">
              <div class="multi-step-item-header custom-border-bottom">
                <label class="text-gray">Step {{ currentStep }} / {{ stepCount }}</label>
                <h2 class="text-white">Complete Submission</h2>
                <label class="text-gray">Thanks for taking the time to complete this form.</label>
              </div>
              <div class="multi-step-item-content">
                <b-form-group
                  id="input-group-name"
                  label="Enter your name:"
                  label-class="text-white"
                  label-for="name"
                >
                  <b-form-input
                    id="name"
                    v-model="form.email"
                    type="text"
                    placeholder="Enter Name"
                    required
                  ></b-form-input>
                </b-form-group>
                <div class="d-flex justify-content-end">
                  <b-button type="button" class="custom-btn previous-btn" @click="goToStep(4)">Back</b-button>
                  <b-button type="submit" class="custom-btn">Submit</b-button>    
                </div>
              </div>
            </div>
          </b-form>
        </div>
    </div>
    </div>
  </div>
</template>

<script>
  import Slider from './CustomRangeSlider.vue'
  export default {
    components: {
      Slider
    },
    name: 'MultiForm',
    data() {
      return {
        form: {
          name: '',
          budget: "10000",
          email: '',
          description: '',
          service: '',
          food: null,
          checked: [],
        },
        sliderWidth: 0,
        description: [
          1, // New Business
          2  // Existing Business
        ],
        service: [
          1, // Website Development
          2  // Existing Business
        ],
        stepCount: 5,
        currentStep: 1,
        foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        show: true
      }
    },
    mounted(){
      this.sliderWidth = document.querySelector('.multi-step-item-content').offsetWidth;
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
      },
      goToStep(step){
        if(step == 4){
          this.$refs.customSlider.setSliderWidth(this.sliderWidth);
        }
        this.currentStep = step;
      },
      changeDescription(description){
        this.form.description = description;
      },
      changeService(service){
        this.form.service = service;
      }
    },
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

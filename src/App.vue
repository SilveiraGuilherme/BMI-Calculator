<template>
  <h1 class="label-title">BMI Calculator</h1>
  <div>
    <img src="./assets/health.jpg" alt="healthy heart" />
  </div>
  <h2 class="label-subtitle">
    Type your weight and height to calculate your BMI
  </h2>
  <div>
    <div class="div-bmi div-input">
      <span class="p-float-label">
        <InputText
          id="input-weight"
          type="text"
          v-model="weight"
          :disabled="bmi"
        />
        <label for="input-weight">Weight</label> kg
      </span>
    </div>

    <div class="div-bmi div-input">
      <span class="p-float-label">
        <InputText
          id="input-height"
          type="text"
          v-model="height"
          :disabled="bmi"
        />
        <label for="input-height">Height</label> m
      </span>
    </div>
  </div>
  <div class="div-bmi">
    <ButtonItem
      class="div-calculate-button"
      v-if="!bmi"
      label="Calculate"
      @click="calculate"
    />
    <ButtonItem
      class="div-clear-button"
      v-if="bmi"
      label="Clear"
      @click="clear"
    />
  </div>
  <div v-if="bmi">
    <p class="label-result">Your BMI is: {{ bmi }}</p>
    <p class="label-classification">
      Your classification is: {{ classification }}
    </p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weight: null,
      height: null,
      bmi: null,
      classification: "",
    };
  },

  methods: {
    calculate() {
      if (this.weight != null && this.height > 0 && this.height != null) {
        this.bmi = (this.weight / (this.height * this.height)).toFixed(2);
        if (this.bmi < 18.5) {
          this.classification = "Underweight";
        } else if (this.bmi >= 18.5 && this.bmi < 25) {
          this.classification = "Normal Weight";
        } else if (this.bmi >= 25 && this.bmi < 30) {
          this.classification = "Overweight";
        } else if (this.bmi >= 30 && this.bmi < 35) {
          this.classification = "Moderate Obesity";
        } else if (this.bmi >= 35 && this.bmi < 40) {
          this.classification = "Severe Obesity";
        } else {
          this.classification = "Very Severe Obesity";
        }
      }
    },
    clear() {
      this.weight = null;
      this.height = null;
      this.bmi = null;
      this.classification = "";
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  text-align: center;
  min-width: 280px;
}
.div-bmi {
  margin-top: 2rem;
}
.div-input {
  display: flex;
  justify-content: center;
}
.label-title {
  font-size: 2rem;
}
.label-subtitle {
  font-size: 1.1rem;
}
.label-result {
  font-size: 2rem;
}
.label-classification {
  font-size: 1.5rem;
}

.div-calculate-button {
  background-color: #ec1b20 !important;
  border: 1px solid #ec1b20 !important;
}
.div-clear-button {
  background-color: #02b3d5 !important;
  border: 1px solid #02b3d5 !important;
}
</style>

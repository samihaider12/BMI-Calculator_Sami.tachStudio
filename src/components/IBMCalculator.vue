<template>
  <div class="container ">
    <div class="row ">
      <div class="col d-flex justify-content-center">
        <div class="calculator ">
          <h2 class="text-center text-info mb-4"> IBM Calculator</h2>

          <div class="row">
            <div class="col">
              <label for="billAmount" class="form-label">Add Your Age</label>
              <input type="text" v-model="getAge" class="form-control" @keypress="allowOnlyNumbers" id="billAmount"
                placeholder="Your Age">
            </div>

            <div class="col">

              <label for="tipPercent" class="form-label">Your Height(Inches)</label>
              <input type="text" v-model="getHeight" class="form-control mb-3" id="tipPercent"
                @keypress="allowOnlyNumbers" placeholder="Your Height Inches">
            </div>
          </div>

          <div class="mb-3">
            <label for="tipPercent" class="form-label">Add Your Weight(Kg)</label>
            <input type="text" v-model="getWeight" class="form-control" id="tipPercent" @keypress="allowOnlyNumbers"
              placeholder="Enter Weight Kg">
          </div>

          <div class="result-box">
            <p><strong>IBM Value: </strong>  <span id="tipAmount">{{  finalIBMData}}</span></p>
            <p><strong>Category:</strong> <span id="totalAmount">{{Category }}</span></p>
            <p><strong>Message:</strong> <span id="totalAmount">{{message }}</span></p>
            <p></p>
          </div>

          <button class="btn btn-primary w-100 mt-3" @click="ibmCalculater()">Calculate</button>
          <button class="btn btn-clear w-100 mt-2" @click="clearFields()">Clear</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

let getAge = ref();
let getHeight = ref()
let getWeight = ref();

let finalIBMData = ref();
let  message = ref();
let Category=ref()


function ibmCalculater() {

  if (getAge.value && getHeight.value > 0 && getWeight.value > 0) {

    let gramtoKG = (getWeight.value);
    let cmtoInch = (getHeight.value);

    let height = (cmtoInch * 0.0254)
    let finalData = gramtoKG / (height * height)

    finalIBMData.value = finalData.toFixed(2)
    
 if (finalIBMData.value < 18.5) {
    Category.value = 'Underweight';
    message.value = 'Aapka wazan kam hai. Sehat ka khayal rakhain.';
  } 
  else  if (finalIBMData.value >= 18.5 && finalIBMData.value <= 24.9) {
    Category.value = 'Normal weight';
    message.value = 'Aapka wazan bilkul theek hai. Good job! 👍';
  }
   else  if (finalIBMData.value >= 25 && finalIBMData.value <= 29.9) {
    Category.value = 'Overweight';
    message.value = 'Aap thoda overweight hain. Exercise aur healthy diet ki zarurat hai.';
  }
   else  if (finalIBMData.value >=  30 && finalIBMData.value <= 34.9) {
    Category.value = 'Obese (Class 1)';
    message.value = 'Aap Obese hain. Kripya exercise aur diet par dhyan dein.';
  }
   else  if (finalIBMData.value >= 35 && finalIBMData.value <= 39.9) {
    Category.value = 'Obese (Class 2)';
    message.value = 'Aapka motapa zyada hai. Doctor se mashwara lena behtar hoga.';
  }
   else  if (finalIBMData.value >= 40) {
    Category.value = 'Obese (Class 3)';
    message.value = 'Bohat zyada motapa. Turant action lena zaroori hai!';
  }
   else {
    Category.value = 'Obese (Outstand)';
    message.value = 'Bohat zyada motapa. Turant action lena zaroori hai!';
  }

  }

}

// Bill Input field allow only Number 
function allowOnlyNumbers(num) {
  if (!/[0-9.]/.test(num.key)) {

    num.preventDefault();
  }
}


function clearFields() {
  // Clear Input fields
  getAge.value="";
  getHeight.value = "";
  getWeight.value = "";
  // Clear Result fields
  finalIBMData.value = "";
  message.value = "";
  Category.value="";
}
</script>

<style scoped>
.container {
  margin-top: 60px;
}

.calculator {
  background-color: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
  width: 100%;
  max-width: 400px;
}

.result-box {
  background-color: #f0f8ff;
  border-radius: 10px;
  padding: 15px;
  margin-top: 20px;
}

.btn-clear {
  background-color: #dc3545;
  color: white;
}

.btn-clear:hover {
  background-color: #bb2d3b;
}
</style>
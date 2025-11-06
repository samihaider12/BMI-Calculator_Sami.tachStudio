 <template>
  <div class="container-fluid d-flex flex-column min-vh-100" >
    <!-- Centered Content Using Grid -->
    <div class="row flex-grow-1 justify-content-center align-items-center">
      <div class="col-12 col-sm-8 col-md-6 col-lg-4" >
        <div class="calculator mx-auto">
          <h2 class="text-center text-info mb-3">IBM Calculator</h2>

          <div class="row">
            <div class="col">
              <label for="billAmount" class="form-label">Add Your Age</label>
              <input
                type="text"
                v-model="getAge"
                class="form-control"
                @keypress="allowOnlyNumbers"
                id="billAmount"
                placeholder="Your Age"
              />
            </div>

            <div class="col">
              <label for="tipPercent" class="form-label">Your Height (Inches)</label>
              <input
                type="text"
                v-model="getHeight"
                class="form-control"
                id="tipPercent"
                @keypress="allowOnlyNumbers"
                placeholder="Your Height Inches"
              />
            </div>
          </div>

          <div class="mb-3 mt-3">
            <label for="weight" class="form-label">Add Your Weight (Kg)</label>
            <input
              type="text"
              v-model="getWeight"
              class="form-control"
              id="weight"
              @keypress="allowOnlyNumbers"
              placeholder="Enter Weight Kg"
            />
          </div>

          <div class="result-box">
            <p><strong>IBM Value:</strong> <span>{{ finalIBMData }}</span></p>
            <p><strong>Category:</strong> <span>{{ Category }}</span></p>
            <p><strong>Message:</strong> <span>{{ message }}</span></p>

            <button class="btn btn-primary w-100 mt-1" @click="ibmCalculater()">Calculate</button>
            <button class="btn btn-clear w-100 mt-1" @click="clearFields()">Clear</button>
          </div>
        </div>
      </div>
    </div>

    <!-- ✅ Fixed Footer -->
    <footer class="footer bg-dark text-light  py-2 m-0">
      © Copyright — BMI Calculator App 2025
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue';

let getAge = ref('');
let getHeight = ref('');
let getWeight = ref('');
let finalIBMData = ref('');
let message = ref('');
let Category = ref('');

function ibmCalculater() {
  if (getAge.value && getHeight.value > 0 && getWeight.value > 0) {
    let gramtoKG = getWeight.value;
    let cmtoInch = getHeight.value;
    let height = cmtoInch * 0.0254;
    let finalData = gramtoKG / (height * height);
    finalIBMData.value = finalData.toFixed(2);

    if (finalIBMData.value < 18.5) {
      Category.value = 'Underweight';
      message.value = 'Aapka wazan kam hai. Sehat ka khayal rakhain.';
    } else if (finalIBMData.value >= 18.5 && finalIBMData.value <= 24.9) {
      Category.value = 'Normal weight';
      message.value = 'Aapka wazan bilkul theek hai. Good job! 👍';
    } else if (finalIBMData.value >= 25 && finalIBMData.value <= 29.9) {
      Category.value = 'Overweight';
      message.value = 'Aap thoda overweight hain. Exercise aur healthy diet ki zarurat hai.';
    } else if (finalIBMData.value >= 30 && finalIBMData.value <= 34.9) {
      Category.value = 'Obese (Class 1)';
      message.value = 'Aap Obese hain. Kripya exercise aur diet par dhyan dein.';
    } else if (finalIBMData.value >= 35 && finalIBMData.value <= 39.9) {
      Category.value = 'Obese (Class 2)';
      message.value = 'Aapka motapa zyada hai. Doctor se mashwara lena behtar hoga.';
    } else if (finalIBMData.value >= 40) {
      Category.value = 'Obese (Class 3)';
      message.value = 'Bohat zyada motapa. Turant action lena zaroori hai!';
    } else {
      Category.value = 'Obese (Outstanding)';
      message.value = 'Bohat zyada motapa. Turant action lena zaroori hai!';
    }
  }
}

function allowOnlyNumbers(e) {
  if (!/[0-9.]/.test(e.key)) e.preventDefault();
}

function clearFields() {
  getAge.value = '';
  getHeight.value = '';
  getWeight.value = '';
  finalIBMData.value = '';
  message.value = '';
  Category.value = '';
}
</script>

<style scoped>
 
.calculator {
  min-height: 70%;
  background-color: #918d8d;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
}

.result-box {
  background-color: #f0f8ff;
  border-radius: 10px;
  padding: 10px;
}

.btn-clear {
  background-color: #dc3545;
  color: white;
}

.btn-clear:hover {
  background-color: #bb2d3b;
}

/* ✅ Footer Fixed */
.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
}
</style>

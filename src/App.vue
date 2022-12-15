<script>
    import { ref } from 'vue'

    export default {
        data: () => ({
          mv: [],
          value: null,
        }),

        watch: {
            value: 'check'
        },

        methods: {
            computeValues(event) {
              event.preventDefault();
              this.mv = [...Array.from({length: 12}, (_, i) => this.value * (i+1))];
            },

            check () {
              if (this.mv) {
                this.mv = [];
              }
            }
        },
    }
</script>

<template>
  <div class="container flex justify-content-center align-items-center">
    <div class="card br-10">
      <h1>Multiplication times table</h1>
      
      <form @submit="computeValues">
        <div class="cform-control pattern-control">
          <label for="value" class="cform-label">Enter a number</label>

          <input
            type="number"
            id="value"
            v-model="value"
            placeholder="Enter a number"
            required
          />
          <div v-if="(typeof(value)) != 'number' && value != ''" class="err-msg">
            Please enter a number e.g 1,3,4
          </div>
        </div>
        <div>
          <button class="br-5">Generate time table</button>
        </div>
      </form>
      <div v-if="mv">
        <div class="flex justify-space-between">
          <ul>
            <li v-for="(n, i) in mv">
              {{value}} * {{i+1}} = {{n}}
            </li>
          </ul>

          <ul v-if="value && mv.length > 0">
            <li v-for="i in 12">
              {{value}} * {{i+1}} = {{value * i}}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 50%;
  padding: 20px !important;
  height: 400px
}

form {
  margin-bottom: 15px
}

h1 {
  text-decoration-line: underline;
  text-underline-offset: 5px;
  margin-bottom: 15px;
}

button {
  border: none;
  height: 30px;
  width: 200px;
  color: white;
  background-color: var(--primary-color);
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
  width: 100%;
}

.container {
  min-height: 100vh;
}
@media (max-width: 1024px) {
}
</style>

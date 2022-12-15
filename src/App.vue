<script>
    import { ref } from 'vue'

    export default {
        data: () => ({
          mv: [],
          value: null,
          visible: false
        }),

        watch: {
            value: 'check'
        },

        methods: {
            computeValues(event) {
              event.preventDefault();
              this.mv = [...Array.from({length: 12}, (_, i) => this.value * (i+1))];
              this.visible = true
            },

            check () {
              if (this.mv) {
                this.mv = [];
              }
              if(this.visible) {
                this.visible = false
              }
            }
        },
    }
</script>

<template>
  <div class="container flex place-center">
    <div class="content">
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
            <div v-if="(typeof(value)) != 'number' && value != null" class="err-msg">
              Please enter a number e.g 1,3,4
            </div>
          </div>
          <div class="mt-1">
            <button class="br-5">Generate time table</button>
          </div>
        </form>
        
        <div v-if="visible" class="flex justify-space-between">
          <div>
            <h3>Result via function computation</h3>
            <ul>
              <li v-for="(n, i) in mv">
                {{i+1}} <span class="text-primary">x</span> {{value}}  = {{n}}
              </li>
            </ul>
          </div>

          <div>
            <h3>Result via vue loop</h3>
            <ul>
              <li v-for="i in 12">
                {{i}} <span class="text-primary">x</span> {{value}} = {{value * i}}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.content {
  width: 50%;
  height: 470px
}

.mt-1 {
  margin-top: 10px;
}
.flex {
  gap: 30px;
}
.card {
  padding: 20px !important;
}

form {
  margin-bottom: 15px
}

h1 {
  text-decoration-line: underline;
  text-underline-offset: 5px;
}
h1, h3 {
  margin-bottom: 15px;
}

button {
  border: none;
  height: 35px;
  width: 200px;
  color: white;
  background-color: var(--primary-color);
  cursor: pointer;
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.container {
  min-height: 100vh;
}
@media (max-width: 1024px) {
}
</style>

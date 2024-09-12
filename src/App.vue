<template>
  <div class="page">
    <h2>Calculator Application</h2>
    <div class="content">
      <h1 v-show="isVisibleInput" class='input-numbers'></h1>
      <div class="containers">
        <table class="buttons">
          <tr>
            <th class="clear" @click="calculate">C</th>
            <th class="operation" @click="calculate">&#8730;</th>
            <th class="operation" @click="calculate">%</th>
            <th class="operation" @click="calculate">/</th>
          </tr>
          <tr>
            <th @click="calculate">7</th>
            <th @click="calculate">8</th>
            <th @click="calculate">9</th>
            <th class="operation" @click="calculate">*</th>
<h1>3</h1>
          </tr>
          <tr>
            <th @click="calculate">4</th>
            <th @click="calculate">5</th>
            <th @click="calculate">6</th>
            <th class="operation" @click="calculate">-</th>
          </tr>
          <tr>
            <th @click="calculate">1</th>
            <th @click="calculate">2</th>
            <th @click="calculate">3</th>
            <th class="operation" @click="calculate">+</th>
          </tr>
          <tr>
            <th @click="calculate">0</th>
            <th class="operation" @click="calculate">.</th>
            <th> </th>
            <th class="equal" @click="calculate">=</th>
          </tr>
        </table>
        <div class="history" v-show="isVisible">
        </div>
      </div>

    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      isVisible: false,
      input: '',
      result: '',
      isVisibleInput:false,
    }
  },
  methods: {
  calculate(event) {
    const inp = document.getElementsByClassName('input-numbers')[0]
    const operation = document.createElement('h2')

    const value = event.target.innerHTML;
    
    if (value !== '=' && value !== 'C') {
      if (value === '√') {
        this.result = Math.sqrt(eval(this.result)).toString(); 
        inp.innerText = this.result; 
      } else {
        this.result += value;
        this.isVisibleInput = true;
        inp.innerText = this.result;
      }
    } else if (value === '=') {
      operation.innerHTML = this.result + "=" + (eval(this.result).toString());
      document.getElementsByClassName('history')[0].appendChild(operation);
      inp.innerText += "=" + eval(this.result).toString();
      this.isVisible = true;
      this.result = '';
    } else if (value === 'C') {
      inp.innerHTML = "";
      this.result = '';
      this.isVisibleInput = false;
    }
  }
}

}
</script>

<style>
#app {
  font-family: 'Playpen Sans';
  text-align: center;
  min-height: 100vh;
  background-color: antiquewhite;
}

.page h1{
  background-color: aliceblue;
  padding: 1%;
  border: 2px solid black;
}
.page h2{
  padding-top: 10px;
  font-size: 3rem;
  font-weight: bold;
  -webkit-text-stroke-color: rgb(0, 0, 0);
  -webkit-text-stroke-width: 1px;
  color: rgb(251, 163, 210);
  text-decoration: underline;
}

.page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.content {
  background-image: url('../public/high-angle-school-supplies-arrangement.jpg');
  background-position: center;
  background-size: cover;
  min-width: 1200px;
  height: 600px;
  border: 2px solid rgb(0, 0, 0);
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.content input {
  width: 80%;
}

.buttons,
.history {
  margin-top: 20px;
  min-width: 400px;
  backdrop-filter: blur(50px);
  border-radius: 20px;
  border: 1.5px solid black;
}

.contai tr {
  color: rgb(0, 0, 0);
}

th {
  border: 2px solid black;
  font-size: 1.8rem;
  border-radius: 20px;
  width: 60px;
  cursor: pointer;
}

.equal,
.clear {
  background-color: rgb(255, 245, 202);
}

.operation {
  background-color: rgb(199, 179, 88);
}

.containers {
  display: flex;
  flex-direction: row;
  gap: 5%;
  width: fit-content;
}
</style>

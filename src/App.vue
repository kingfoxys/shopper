<template>
  <div id="app">
    <md-card>
      <md-card-header>
        <div class="md-title">Prueba de reclutamiento Shooper</div>
        <div class="md-subhead">Número menor o igual en secuencia de Fibonacci</div>
      </md-card-header>
      <md-card-content>
        <md-field>
          <label>Introduzca un número para buscar su más cercano en la secuencia de Fibonacci</label>
          <md-input v-model="numberuser"></md-input>
        </md-field>
        <div>
          <md-button class="md-raised md-primary" v-on:click="search">Buscar</md-button>
        </div>
      </md-card-content>
      <md-toolbar v-show="answered">
        <h3 class="md-title">El número más cercano a la secuencia de Fibonacci es: {{finalnumber}}</h3>
      </md-toolbar>
    </md-card>
  </div>
</template>

<script>
export default {
  name: "App",
  data: function() {
    return {
      fibonumbers: [0, 1],
      numberuser: 0,
      finalnumber: 0,
      answered: false
    };
  },
  methods: {
    createFibonacci: function() {
      let init = 0;
      for (let i = 2; i < 39 + 1; i++) {
        this.fibonumbers.push(
          this.fibonumbers[i - 2] + this.fibonumbers[i - 1]
        );
      }
    },
    search: function() {
      let check = Number(this.numberuser);
      if (!Number.isInteger(check)) {
        alert("Su número debe ser entero");
      } else if (check > 100000000) {
        alert("Su número debe ser inferior a 100,000,000");
      } else {
        this.createFibonacci();
        this.checkNumber(check);
        this.answered = true;
      }
    },
    checkNumber: function(check) {
      let resp = 0;
      this.fibonumbers.forEach(function(value, idx, arr) {
        if (arr[idx - 1] != undefined) {
          if (check > arr[idx - 1] && check <= arr[idx]) {
            resp = arr[idx-1];
            return arr[idx];
          }
        }
      });
      this.finalnumber = resp;
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>

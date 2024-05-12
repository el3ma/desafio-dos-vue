<template>
  <div id="app">
    <form>
      <div>
        <label>Título de la tarjeta: </label>
        <input v-model="registro.nomTarjeta">
      </div>

      <div>
        <label>Chip SRC: </label>
        <input />
      </div>

      <div>
        <label>Número: </label>
        <input v-model="registro.numeroTarjeta">
      </div>

      <div>
        <label>Fecha de expiración: </label>
        <input v-model="registro.fechaExp">
      </div>

      <div>
        <label>Propietario: </label>
        <input v-model="registro.propietario">
      </div>

      <div>
        <label for="tipoTarjeta">Tipo de tarjeta SRC: </label>
        <select name="tipoTarjeta" id="tipoTarjeta" v-model="registro.tituloTarjeta"
          @change="cambiarTarjeta(registro.tituloTarjeta)">
          <option value=" " selected>Seleccionar...</option>
          <option value="American Express">American Express</option>
          <option value="Mastercard">MasterCard</option>
          <option value="Visa">Visa</option>
        </select>
      </div>
      <button class="btn" @click="generarNumero()">
        Generar número de tarjeta
      </button>
    </form>

    <div class="carnet">
      <h3>{{ registro.tituloTarjeta }}</h3>
      <img width="40" src="/img/chip.png" alt="" />
      <div>
        <h2>{{ registro.numeroTarjeta }}</h2>
        <span>Fecha Exp: <b>{{ registro.fechaExp }}</b></span>
      </div>
      <footer>
        <span>{{ registro.propietario }}</span>
        <img :src="registro.currentTarget" width="60" height="35px" />
      </footer>
    </div>
  </div>
</template>

<script>
import moment from "moment";
export default {
  name: 'App',
  data() {
    return {
      registro: {
        tituloTarjeta: '',
        currentTarget: '',
        numeroTarjeta: '',
        fechaExp: '',
        propietario: 'William Henry Gates III',
        nomTarjeta: '',
        tipoTarjeta: ''
      },
      tiposTarjetas: [
        { id: 1, path: "/img/visa.png", nombre: 'Visa' },
        { id: 2, path: "/img/mastercard.png", nombre: 'Mastercard' },
        { id: 3, path: "/img/American-Express.png", nombre: 'American Express' }
      ],
    }
  },
  methods: {
    cambiarTarjeta: function (nomTarjeta) {
      if (nomTarjeta == "American Express") {
        this.registro.currentTarget = this.tiposTarjetas[2].path;
        console.log(this.registro.currentTarget);
        console.log(this.tipoTarjetas);
      } else if (nomTarjeta == "Mastercard") {
        this.registro.currentTarget = this.tiposTarjetas[1].path;
      } else if (nomTarjeta == "Visa") {
        this.registro.currentTarget = this.tiposTarjetas[0].path;
      } else {
        this.registro.currentTarget = false;
      }
    },
    generarNumero: function () {
      this.registro.numeroTarjeta = Math.floor(
        Math.random() * (599999999999 - 300000000000) + 300000000000
      );
      let fechaVenc = moment().add(5, "year");
      this.registro.fechaExp = fechaVenc.format("MM/YY");
    },
  },
  components: {

  }
}
</script>

<style>
* {
  margin: 0;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
  font-size: 10px;
  font-family: sans-serif;
  gap: 60px;
}

form {
  padding: 18px;
  border-radius: 20px;
  border: ridge 1px;
  box-shadow: 1px 1px 1px 1px gray;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  gap: 15px;
  justify-content: center;
}

form div {
  display: grid;
  grid-template-columns: 100px 200px;
  align-items: center;
  gap: 5px;
}

form div label {
  text-align: right;
}

.carnet {
  width: 400px;
  height: 230px;
  background: #1c1a1e;
  color: white;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px 2px black;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h3 {
  font-size: 20px;
}

h2 {
  font-size: 30px;
  letter-spacing: 10px;
  margin-bottom: 15px;
  text-shadow: 0px 0px 1px gold;
  font-family: Times;
}

b {
  font-size: 16px;
}

footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-weight: bold;
  font-size: 18px;
  text-transform: uppercase;
  font-style: italic;
}
</style>

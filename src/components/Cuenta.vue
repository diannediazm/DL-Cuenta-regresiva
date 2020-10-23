<template>
  <div>
    <h2>Cuenta regresiva</h2>
    <h2>{{temporizador(tiempo)}}</h2>
    <button class="botones" v-for="digitos in botones" :key="digitos" @click="cuentaRegresiva(digitos.tiempo)">{{digitos.cifra}}</button>
  </div>
</template>

<script>
export default {
  name: 'Cuenta',
  data(){
    return{
      tiempo: 0,
      botones: [
        {cifra: '03s', tiempo: 3},
        {cifra: '01m', tiempo: 60},
        {cifra: '05m', tiempo: 300},
        {cifra: '10m', tiempo: 600},
        {cifra: '30m', tiempo: 1800},
      ],
      intervalo: '',
      estado: {activo: false, boton: 'Iniciar'},
    }
  },
  methods: {
    temporizador: function (tiempo) {
      let minutos = ('0' + Math.floor(tiempo/60)).slice(-2);
      let segundos = ('0' + tiempo%60).slice(-2);
      return `${minutos}:${segundos} min/seg`
    },
    cuentaRegresiva: function (cuenta) {
      this.tiempo = cuenta;
      this.estado.activo = true;
      this.intervalo = setInterval(() => {
        if (this.tiempo > 0){
          this.tiempo --;
        } else {
          clearInterval(this.intervalo)
        }
      },1000);
    }    
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.botones {
  background-color: aqua;
  margin-left: 10px;
  border: 0px;
}
</style>

<template>
  <div id="app">
    <Gatos />
    <!--Titulo pagina -->
    <section>
      <h1>Random Gif Cat</h1>
    </section>
    <!--Filtros para agregar caracteristicas al gatito -->

    <section class="seccion-filtros">
      <div class="row ml-5">
        <h3>Título:</h3>
        <input type="text" placeholder="Escribe tu frase" v-model="titulo" />
      </div>
      <!--filtro -->
      <div class="row ml-5">
        <h3>Filtro:</h3>
        <select v-model="filtro">
          <option v-for="cambioFiltro in arrFiltro" :key="cambioFiltro">
            {{ cambioFiltro }}
          </option>
        </select>
      </div>

      <!--color  -->
      <div class="row ml-5 text-center">
        <h3>Color:</h3>
        <select
          v-model="color"
          class="form-select"
          aria-label="Default select example"
        >
          <option v-for="cambioColor in arrColor" :key="cambioColor">
            {{ cambioColor }}
          </option></select
        ><span
          class="selecColor"
          :style="{ backgroundColor: this.color }"
        ></span>
      </div>
      <!--Tamaño  -->
      <div class="row ml-5">
        <h3>Tamaño:</h3>
        <input type="number" v-model="tamano" />
      </div>
    </section>

    <!--Botón y gatito modificado-->
    <section>
      <button @click="getGato()" class="btn btn-danger" type="button">
        Obtener mi Gatito
      </button>
    </section>

    <!--gif final -->
    <div class="gif mt-5">
      <h5>Mi gatito modificado</h5>
      <img :src="imagen && imagen.config && imagen.config.url" alt="" />
    </div>
  </div>
</template>

<script>
import Gatos from "./components/Gatos.vue";
import axios from "axios"; /*no olvidar importar axios !!!!!*/

export default {
  name: "App",
  components: {
    Gatos,
  },
  data() {
    return {
      titulo: "",
      arrFiltro: ["blur", "mono", "sepia", "negative", "paint", "pixel"],
      arrColor: ["red", "green", "blue", "pink", "yellow", "white"],
      color: "",
      filtro: "",
      tamano: "",
      imagen: "",
    };
  },
  methods: {
    async getGato() {
      const url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}&type=or`;
      try {
        const peticionApi = await axios(url);
        if (!peticionApi) return;
        console.log(peticionApi.data);
        this.imagen = peticionApi;
      } catch (error) {
        console.log(error);
      }
    },
  },
  /*created(){
    this.getGato();
  }*/
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.seccion-filtros {
  position: relative;
  left: 32rem;
  margin: 1rem;
}

.selecColor {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  margin-left: 15px;
  display: inline-block;
}

* {
  margin: 0;
  padding: 0;
}
h1 {
  font-family: roboto;
  font-size: 50px;
  text-align: center;
  padding-top: 50px;
  padding-bottom: 50px;
  margin: 0;
}
select {
  width: 13rem;
}
h5{
   font-family: roboto;
  font-size: 50px;
}
</style>

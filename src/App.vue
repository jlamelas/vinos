<template>
  <div id="app">
    <div class="container">
      <div class="page-header">
        <h1>Vinos y espumosos</h1>
      </div>
      <div class="panel panel-primary">
        <div class="panel-heading">
          <h1>Nuevo vino</h1>
        </div>
        <div class="panel-body">
          <form id="form" class="form-inline" @submit.prevent="anadirVino">
            <div class="form-group">
              <label for="nombreVino">Nombre: </label>
              <input type="text" id="nombreVino" class="form-control" v-model="nuevoVino.nombre">
              <label for="doVino">Denominación de Origen: </label>
              <select class="form-control" id="doVino" v-model="nuevoVino.doVino">
                <option value="">Selecciona una D.O.</option>
                <option v-for="origen in denominacionesOrigen" value="">{{origen.nombre}}</option>
              </select>
              <label for="precioVino">Precio: </label>
              <input type="text" id="precioVino" class="form-control" v-model="nuevoVino.precio"><br>
              <h3>Notas de cata: </h3>
              <div class="form-group">
                <label for="vista">Vista: </label>
                <input type="textarea" id="vista" class="form-control" v-model="nuevoVino.cata.vista">
                <label for="nariz">Nariz: </label>
                <input type="textarea" id="nariz" class="form-control" v-model="nuevoVino.cata.nariz">
                <label for="boca">Boca: </label>
                <input type="textarea" id="boca" class="form-control" v-model="nuevoVino.cata.boca">
              </div><br>
              <h3>Proveedor: </h3>
              <div class="form-group">
                <label for="nombreProveedor">Nombre: </label>
                <input type="text" id="nombreProveedor" class="form-control" v-model="nuevoVino.proveedor.nombre">
                <label for="contactoProveedor">Contacto: </label>
                <input type="text" id="contactoProveedor" class="form-control" v-model="nuevoVino.proveedor.contacto">
                <label for="telefonoProveedor">Teléfono: </label>
                <input type="text" id="telefonoProveedor" class="form-control" v-model="nuevoVino.proveedor.telefono">
              </div>
              <br><br>
              <input type="submit" class="btn btn-primary" value="Añadir nuevo vino">
            </div>
          </form>
        </div>
      </div>
      <div class="row">
        <div class="col-xs-6 col-md-4 col-lg-3" v-for="origen in denominacionesOrigen">
          <div class="panel panel-primary">
            <div class="panel-heading">
              {{origen.nombre}}
            </div>
            <div class="panel-body">
              <img :src="origen.imagen" :alt="origen.nombre" class="img-responsive center-block">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Firebase from 'firebase';
let config = {
     apiKey: "AIzaSyBJNWGmIkfWrCk1rOzjyDzFLRaf073be08",
     authDomain: "vinos-y-esoumosos.firebas:eapp.com",
     databaseURL: "https://vinos-y-esoumosos.firebaseio.com",
     projectId: "vinos-y-esoumosos",
     storageBucket: "vinos-y-esoumosos.appspot.com",
     messagingSenderId: "324641178050"
};
Firebase.initializeApp(config);
let db = Firebase.database();
let ReferenciaVinos = db.ref('vinos');

export default {
  name: 'app',
  firebase: {
    vinos: ReferenciaVinos
  },
  data() {
    return {
      nuevoVino: {
        nombre: '',
        doVino: '',
        proveedor: {
          nombre: '',
          contacto: '',
          telefono: ''
        },
        cata: {
          vista: '',
          nariz: '',
          boca: ''
        },
        precio: '',
        imagen: ''
      },
      denominacionesOrigen: [
        {
          nombre: "D.O. Rías Baixas",
          imagen: "../static/do-rias-baixas.jpg"
        },
        {
          nombre: "D.O. Ribeira Sacra",
          imagen: ""
        },
        {
          nombre: "D.O. Monterrei",
          imagen: ""
        },
        {
          nombre: "D.O. Valdeorras",
          imagen: ""
        },
        {
          nombre: "D.O. Ribeiro",
          imagen: ""
        },
        {
          nombre: "D.O. Bierzo",
          imagen: ""
        },
        {
          nombre: "D.O. Ribera del Duero",
          imagen: "../static/ribera-del-duero.gif"
        },
        {
          nombre: "V.T. Castilla y León",
          imagen: ""
        },
        {
          nombre: "D.O. Toro",
          imagen: ""
        },
        {
          nombre: "D.O.C. La Rioja",
          imagen: "../static/rioja-vinos-do.jpg"
        },
        {
          nombre: "D.O. Somontano",
          imagen: ""
        },
        {
          nombre: "D.O.C. Priorat",
          imagen: ""
        },
        {
          nombre: "V.T. Castilla",
          imagen: ""
        },
        {
          nombre: "D.O. Málaga",
          imagen: ""
        }
      ]
    }
  },
  methods: {
    anadirVino(){
      ReferenciaVinos.push(this.nuevoVino);
      this.nuevoVino.nombre = '';
      this.nuevoVino.doVino = '';
      this.nuevoVino.proveedor.nombre = '';
      this.nuevoVino.proveedor.contacto = '';
      this.nuevoVino.proveedor.telefono = '';
      this.nuevoVino.cata.vista = '';
      this.nuevoVino.cata.nariz = '';
      this.nuevoVino.cata.boca = '';
      this.nuevoVino.precio = '';
    }
  }
}
</script>

<style>

</style>

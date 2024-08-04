<template>
    <div>
      <h1>{{ titulo }}</h1>
      <div class="filtro">
        Filtro: <input type="search" v-model="textoBusar">
      </div>
      <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Email</th>
                <th>Address</th>
                <th>Phone</th>
                <th>Country</th>
                <th>City</th>
                <th></th>
            </tr>
            <tr>
                <th><button @click="guardarNuevo()">Agregar</button></th>
                <th><input type="text" v-model="personaNuevaObj.name"></th>
                <th><input type="text" v-model="personaNuevaObj.email"></th>
                <th><input type="text" v-model="personaNuevaObj.address"></th>
                <th><input type="text" v-model="personaNuevaObj.phone"></th>
                <th><input type="text" v-model="personaNuevaObj.country"></th>
                <th><input type="text" v-model="personaNuevaObj.city"></th>
                <th></th>
            </tr>
            <tr>
                <th><button @click="guardarEdicion()">Guardar</button></th>
                <th><input type="text" v-model="personaEditarObj.name"></th>
                <th><input type="text" v-model="personaEditarObj.email"></th>
                <th><input type="text" v-model="personaEditarObj.address"></th>
                <th><input type="text" v-model="personaEditarObj.phone"></th>
                <th><input type="text" v-model="personaEditarObj.country"></th>
                <th><input type="text" v-model="personaEditarObj.city"></th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(persona, index) in listaPersonasComputada" :key="persona.id">
                <td>{{ persona.id }}</td>
                <td>{{ persona.name }}</td>
                <td>{{ persona.email }}</td>
                <td>{{ persona.address }}</td>
                <td>{{ persona.phone }}</td>
                <td>{{ persona.country }}</td>
                <td>{{ persona.city }}</td>
                <td><button @click="eliminarPersona(index)">Eliminar</button><button @click="editarPersona(persona, index)">Editar</button></td>
             </tr>
        </tbody>
      </table>
    </div>
  </template>
  
<script >
  export default {
    name: 'MiComponente',
    data() {
      return {
        titulo: 'Agenda de contactos',
        textoBusar: '',
        personaNuevaObj: {
            id: "6",
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        personaEditarObj: {
            id: "",
            name: "",
            email: "",
            address: "",
            phone: "",
            country: "",
            city: ""
        },
        indexParaEditar: null, 
        personas: 
        [
            {
            id: 1,
            name: "Alice Johnson",
            email: "alice.johnson@example.com",
            address: "123 Maple Street",
            phone: "123-456-7890",
            country: "USA",
            city: "New York"
            },
            {
            id: 2,
            name: "Bob Smith",
            email: "bob.smith@example.com",
            address: "456 Oak Avenue",
            phone: "987-654-3210",
            country: "Canada",
            city: "Toronto"
            },
            {
            id: 3,
            name: "Carol White",
            email: "carol.white@example.com",
            address: "789 Pine Road",
            phone: "555-123-4567",
            country: "UK",
            city: "London"
            },
            {
            id: 4,
            name: "David Brown",
            email: "david.brown@example.com",
            address: "321 Elm Street",
            phone: "444-555-6666",
            country: "Australia",
            city: "Sydney"
            },
            {
            id: 5,
            name: "Emily Davis",
            email: "emily.davis@example.com",
            address: "654 Spruce Lane",
            phone: "333-444-5555",
            country: "USA",
            city: "Los Angeles"
            }
        ]
      }
    },
    components: {
      // Registro de componentes que se utilizaran.
    },
    methods: {
      // métodos que se pueden llamar desde la plantilla o desde otras partes del componente.
      guardarNuevo(){
        this.personas.push(Object.assign({}, this.personaNuevaObj));
      },
      eliminarPersona(index){
        this.personas.splice(index, 1);
       },
       guardarEdicion(){
        this.personas[this.indexParaEditar] = Object.assign({}, this.personaEditarObj);
       },
       editarPersona(persona, index){
        this.indexParaEditar = index;
        this.personaEditarObj = Object.assign({},persona);
       },
    },
    computed: {
      // propiedades computadas que dependen de otras propiedades reactivas
      listaPersonasComputada(){
            return this.personas.filter(item => item.name.toLowerCase().includes(this.textoBusar.toLowerCase())||item.email.toLowerCase().includes(this.textoBusar.toLowerCase()));
        } 
    },
    props: {
      // propiedades que el componente puede recibir.
    },
    emits: [] // los eventos personalizados que el componente puede emitir.
  }
  </script>
  
  <style scope>
h1 {
    color: #42b983;
}
table {
    width: 100%;
    border-collapse: collapse;
}
th, td {
    border: 1px solid #ddd;
    padding: 8px;
}
th {
    background-color: #f2f2f2;
    text-align: left;
}
div {
  text-align: lef;
  }
  </style>
<template>
    <div class="container-fluid mt-3">
        <input type="text" class="form-control mb-3" v-model.trim="criterioDeBusquedaDNI" @input="criterioDeBusquedaDNIDIRTY = true" placeholder="Busqueda por DNI"> 
        <div v-if="errorDni.mostrar" class="alert alert-danger my-1">
                {{ errorDni.mensaje }}
        </div>
        <input type="text" class="form-control" v-model.trim="criterioDeBusquedaNombre" @input="criterioDeBusquedaNombreDIRTY = true" placeholder="Busqueda por Nombre">
        <div v-if="errorNombre.mostrar" class="alert alert-danger my-1">
            {{ errorNombre.mensaje }}
        </div>
        <br>
        
        <div class="card-deck m-0">
            <div class="row">
                <div class="col" v-for="persona in personasFiltradas">
                    
                    <div class="card mb-3">
                        <div class="card-body">
                            <h5 class="card-title">{{getNombreCompleto(persona)}}</h5>
                            <p class="card-text">dni {{persona.dni}}</p>
                            <a href="#" class="card-link">{{persona.correo}}</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
// Componentes de simple archivo (Template, Script y Style)

export default {
    name: 'Atributos', 
    
    data(){
        return {
            criterioDeBusquedaDNI: '',
            criterioDeBusquedaDNIDIRTY: null,
            criterioDeBusquedaNombre: '',
            criterioDeBusquedaNombreDIRTY: null,
            // formData: {
            //     nombre: null
            // },
            // formDirty: {
            //     nombre: null
            // },
             
            //Aquí, en este array es donde tienen que agregar su información
            personas: [
                {
                    nombre: "Daniel",
                    apellido: "Sanchez",
                    correo: "danielsanchez68@hotmail.com",
                    dni: "20442873"
                },
                {
                    nombre: "Juan",
                    apellido: "Perez",
                    correo: "j@p.gmail.com",
                    dni: "12345678"
                },
                {
                    nombre: "Ana",
                    apellido: "Suarez",
                    correo: "a@s.gmail.com",
                    dni: "87654321"
                },
                {
                    nombre: "Shelomo Uziel",
                    apellido: "Setton (no es mi dni)",
                    correo: "shelosetton@gmail.com",
                    dni: "20442873"
                },
                {
                    nombre: "Shlomo",
                    apellido: "dana",
                    correo: "shlomodana@gmail.com",
                    dni: "30600000"
                },
            ]
        }
    },
    methods: {
        getNombreCompleto(persona) {
            return `${persona.nombre} ${persona.apellido}`
        }
    },
    computed: {
        personasFiltradas() {
            if (this.errorDni.ok === false && this.errorNombre.ok === false) {
                return this.personas;
            }

            return this.personas.filter((persona) => {
                let coincideDni = true;
                let coincideNombre = true;

                if (this.errorDni.ok) {
                    coincideDni = persona.dni.toLowerCase()
                        .includes(this.criterioDeBusquedaDNI.toLowerCase());
                }

                if (this.errorNombre.ok) {
                    coincideNombre = persona.nombre.toLowerCase()
                        .includes(this.criterioDeBusquedaNombre.toLowerCase());
                }

                return coincideDni && coincideNombre;
            });
        },


        errorDni(){
            let mensaje = '';
            if (this.criterioDeBusquedaDNI.length < 3) mensaje = 'Este campo debe poseer al menos 3 caracteres';
            else if (this.criterioDeBusquedaDNI.includes(' ')) mensaje = 'Este campo no permite espacios intermedios';
            
            return {
                mensaje,
                mostrar: mensaje != '' && this.criterioDeBusquedaDNIDIRTY,
                ok: mensaje === '',
            }
        },
        errorNombre(){
            let mensaje = '';
            if (this.criterioDeBusquedaNombre.length < 3) mensaje = 'Este campo debe poseer al menos 3 caracteres';
            else if (this.criterioDeBusquedaNombre.includes(' ')) mensaje = 'Este campo no permite espacios intermedios';
            
            return {
                mensaje,
                mostrar: mensaje != '' && this.criterioDeBusquedaNombreDIRTY,
                ok: mensaje === '',
            }
        },
    }
}
</script>

<style scoped>
    .card-header{
        background-color: blueviolet;
        color: white;
    }



</style>
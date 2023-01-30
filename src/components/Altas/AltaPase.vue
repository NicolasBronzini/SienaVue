<template>
   <!-- Este va a ser el apartado de pase -->

   <div class="Alta_Expedientes_Pase_Conteiner" id="Container_total_Pase">
      <!-- encabezado y fecha -->
      <div class="Encabezado_Alta_Expediente_Pase">
         <span id="" style="font-size:1.4rem;">ALTA PASE MASIVO DE EXPEDIENTES ELECTRÓNICOS</span>
         <p>fecha: {{ currentDate }}</p>
      </div>
      <!-- referencias de proceso -->
      <div class="Referencia_Proceso_Pase_Expedientes">
         <p>Nro. Lote</p>
         <p>Estado <span> <strong>Pendiente</strong> </span> </p>
         <p>Usuario <span> <strong> Apellido/s y Nombre/s</strong></span></p>
         <p>Tipo Proceso <span> <strong> Firma</strong></span> </p>
      </div>
      <!-- inputs de seleccion de referencia para generar expediente -->
      <div class="container_Inputs_Entrada_Data_Pase">
         <!-- Input Referencia -->
         <div class="div_Inputs_Entrada_Data_Pase Inputs_btnAsocia_Unico_Item animate__animated form-control">
            <p>Referencia</p>
            <input type="text" class="grupo_Entrada_Data_Pase" required style="width: 100%; height: 40px;"
               v-model="referenciaPase" />
         </div>
         <!-- Firmante -->
         <div class="div_Inputs_Entrada_Data_Pase Inputs_btnAsocia_Unico_Item animate__animated form-control">
            <p> Firmante</p>
            <div class=" grupo_Entrada_Data_Pase" role="group">
               <input type="text" style="width: 100%; height: 40px;" id="firmante_alta_proceso_masivo_Pase"
                  v-model="firmantePase" />

            </div>
         </div>

      </div>
      <!-- SWITCH DE TESTEO Y ASOCIACION-->


      <div class="container_Permite_Asociacion_Pase container_Permite_Asociacion_Pase2">
         <div class="div_Permite_Asociacion_Pase2">
            <p>¿El destino de los EE es único?</p>
            <button class="Swich_Asociacion" id="switchDestinoUnicoPase" @click="toggleClassDestinoUnicoPase"
               v-bind:class="addedClassDestinoUnicoPase"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Pase2">
            <p>¿Asocia Expediente?</p>
            <button class="Swich_Asociacion" id="switchAsociaExpedientePase"
               @click="toggleClassAsociacionExpedientePase"
               v-bind:class="addedClassAsociacionExpedientePase"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Pase2">
            <p>¿Requiere Asociación SIENA?</p>
            <button class="Swich_Asociacion" id="switchAsociacionSIENA" @click="toggleClassAsociacionSienaPase"
               v-bind:class="addedClassAsociacionSienaPase"><span>No</span><span>Si</span></button>
         </div>

      </div>

      <!-- Otros tipos de switch y select de GDE -->

      <div class="container_Permite_Asociacion_Pase container_Permite_Asociacion_Pase2">
         <div class="div_Inputs_Entrada_Data_Pase Inputs_btnAsocia_Unico_Item animate__animated form-control">
            <p>Usuario, Reparticion o mesa de una reparticion en GDE</p>
            <div class=" grupo_Entrada_Data_Pase">
               <select class="select_Data_Alta" id="" style="width: 100%; height: 40px;">
                  <option>Seleccionar</option>
               </select>
            </div>
         </div>
         <div class="div_Permite_Asociacion_Pase2">
            <p><strong> ¿Asocia a un unico EE?</strong></p>
            <button class="Swich_Asociacion" id="switchAsociaUnicoEEPase" @click="toggleClassAsociacionUnicaEEPase"
               v-bind:class="addedClassAsociacionUnicaEEPase"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Pase2">
            <p>¿Asocia a un unico Item?</p>
            <button class="Swich_Asociacion" id="switchAsociaUnicoEEPase2" @click="toggleClassAsociacionUnicoItemPase"
               v-bind:class="addedClassAsociacionUnicoItemPase"><span>No</span><span>Si</span></button>
         </div>

      </div>

      <!-- Input y select de EE Pase -->
      <div class="container_Inputs_Entrada_Data_Pase">
         <!-- Input Referencia -->
         <div class="div_Inputs_Entrada_Data_Pase Inputs_btnAsocia_Unico_Item animate__animated form-control">
            <p>Expediente Electronico</p>
            <input type="text" class="grupo_Entrada_Data_Pase" required placeholder="Ex-Año-XXXXXXXX-APN-Reparticion" />
         </div>
         <!-- Firmante -->
         <div class="div_Inputs_Entrada_Data_Pase Inputs_btnAsocia_Unico_Item animate__animated form-control">
            <p> Firmante</p>
            <div class="grupo_Entrada_Data_Pase" role="group">
               <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;">
                  <!-- Chequear su existencia en GDE. Selección única -->
                  <option class="Seleccionar_Option" selected>Seleccionar</option>
                  <option>nombre de firmante</option>
               </select>
            </div>
         </div>

      </div>

      <!-- Apartado cruadricula Pase -->
      <div class="DatosPaseEEContainer">
         <div class="container_HeaderCuadricula">
            <div class="_dataFiltroPase"><span>+</span><span>Importar EE generado masivamente</span></div>
            <div class="btn_dataFiltroPase"><button>Primero</button><button>Anterior</button>
               <p>Registros {numero}</p>
               <p>Pàgina{numero} de {numero}</p><button>Siguiente</button><button>Último</button>
            </div>
         </div>

         <div class="ContainerCuadriculaMotivoInternoPase">
            <div class="HeaderCuadriculaMotivoInternoPase">
               <h4>Expediente Electrónico</h4>
            </div>
            <div class="OutputCuadriculaMotivoInternoPase">

            </div>
         </div>
      </div>
      <!-- Apartado cruadricula Caratulacion -->
      <div class="container" id="divTablaAltaProcesoMasivoDeFirma" style="margin-top:50px ;">
         <table>
            <tr v-for="(value, key) in localStorageData" :key="key">
               <td id="headerTabla">{{ key }}</td>
               <td id="tablavalue">{{ value }}</td>
            </tr>

         </table>
      </div>
      <!-- Botones de accion con ese nuevo proceso -->
      <div class="container_btn_Proceso_Pase" id="">
         <button class="Cancelar_Proceso_Pase btn btn-danger" id="">X Cancelar </button>
         <button class="Procesar_Proceso_Pase btn btn-primary" id=""> Procesar </button>
         <button class="Guardar_Proceso_Pase btn btn-success" id=""> Guardar </button>
      </div>
   </div>
</template>

<script>
import moment from 'moment';
export default {
   name: 'AltaPase',
   data() {
      return {
         addedClassAsociacionUnicoItemPase: '',
         addedClassAsociacionUnicaPase: '',
         addedClassAsociacionSienaPase: '',
         addedClassAsociacionExpedientePase: '',
         addedClassDestinoUnicoPase: '',
         addedClassAsociacionUnicaEEPase: '',

         //DataTime
         currentDate: moment().format('YYYY-MM-DD')
      }
   },
   methods: {
      toggleClassAsociacionUnicoItemPase() {
         this.addedClassAsociacionUnicoItemPase = this.addedClassAsociacionUnicoItemPase === 'active' ? '' : 'active'
      },
      toggleClassAsociacionUnicaPase() {
         this.addedClassAsociacionUnicaPase = this.addedClassAsociacionUnicaPASE === 'active' ? '' : 'active'
      },
      toggleClassAsociacionSienaPase() {
         this.addedClassAsociacionSienaPase = this.addedClassAsociacionSienaPase === 'active' ? '' : 'active'
      },
      toggleClassAsociacionExpedientePase() {
         this.addedClassAsociacionExpedientePase = this.addedClassAsociacionExpedientePase === 'active' ? '' : 'active'
      },
      toggleClassDestinoUnicoPase() {
         this.addedClassDestinoUnicoPase = this.addedClassDestinoUnicoPase === 'active' ? '' : 'active'
      },
      toggleClassAsociacionUnicaEEPase() {
         this.addedClassAsociacionUnicaEEPase = this.addedClassAsociacionUnicaEEPase === 'active' ? '' : 'active'
      }

   },
   computed: {
      fechaFormatada() {
         return this.fecha.toLocaleString();
      }
   }
}
</script>




<style lang="css" scoped>
/* Proceso de alta de expedientes */
.Alta_Expedientes_Pase_Conteiner {
   display: block;
   width: 98%;
   margin: auto;
   background-color: white;
   border: 1px solid gray;
   margin-top: 10px;
   border-radius: 5px;
}

.ContainerPaseActive {
   display: block;
}

.Encabezado_Alta_Expediente_Pase {
   display: flex;
   justify-content: space-between;
   margin: 0 400px 0 20px;
   color: grey;
}

/* proceso de referencias de datos Nro.Lote Estado Usuario Tipo proceso */
.Referencia_Proceso_Pase_Expedientes {
   display: flex;
   justify-content: space-around;
   color: gray;
}

.Referencia_Proceso_Pase_Expedientes p span {
   color: black;

}

/* inputs y buttons referencias y datos de nuevo expediente */
.container_Inputs_Entrada_Data_Pase {
   display: flex;
   justify-content: space-around;
   margin: auto;
   margin-bottom: 50px;
}

.div_Inputs_Entrada_Data_Pase {
   width: 32.6%;
   margin: 0 20px 0 50px;
}

.div_Inputs_Entrada_Data_Pase p {
   font-size: 1.2rem;
   color: gray;

}

.div_Inputs_Entrada_Data_Pase button {
   width: 500px;
   text-align: start;
}

.div_Inputs_Entrada_Data_Pase input {
   width: 500px;
}

.grupo_Entrada_Data_Pase {
   margin-top: -10px;
   text-align: start;
   height: 40px;

}

.selectDataAlta {
   width: 500px;
}

.btn_ProcesoPase {
   color: gray;
}

/* No requiere asociacion */
.container_PaseNoAsociacion {
   display: block !important;
}

.div_NoPermiteAsociacionPase {
   display: flex;
}

.div_NoPermiteAsociacionPase div {
   margin-bottom: 70px;
}

#div_UnicoItembtn {
   margin-left: 150px;
}

/* Permite Asociacion */
/* Input Entidad al Asociar Unico Item */

#div_InputTipoDocumentoSIENA {
   margin: auto;
   display: none;
}

.reactive#div_InputTipoDocumentoSIENA.active {
   display: block;
   margin-top: 50px;
}

#InputActiveEntidad {
   display: none;
}

.reactive#InputActiveEntidad.active {
   display: block;
}

#TipoDocumentoSiena {
   width: 300px;

}

.container_Permite_Asociacion_Pase {
   display: flex;
   justify-content: space-between;
   margin: auto;
   margin: 70px 80px;
}

.reactive#UbicacionPath2 {
   display: block;
}

.reactive#UbicacionPath2.active {
   display: none;
}

#UbicacionPath {
   margin-left: 100px;
   margin-top: 40px;
   display: none;
}

.reactive#UbicacionPath.active {
   display: block;
}

.div_Permite_Asociacion_Pase {
   font-size: 1.1rem;
}

.div_Permite_Asociacion_Pase button {
   background-color: #65b2e2;
   border: none;
   padding: 10px 50px 10px 0px;
   color: white;
}

.div_Permite_Asociacion_Pase2 {
   margin-top: -20px;
}

.div_Permite_Asociacion_Pase2 button {
   margin: -5px 0px;
   border: none;
}

/*---------------------------------- Switch------------------------------- */
.Swich_Asociacion {
   background: rgba(17, 123, 245, 1.0);
   background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   ;
   border: none;
   border-radius: 5px;
   position: relative;
   cursor: pointer;
   display: flex;
   outline: none;

}

.Swich_Asociacion::after {
   padding-top: 20px;
   content: "Si";
   display: block;
   width: 100px;
   height: 60px;
   position: absolute;
   background: #f1f1f1;

   border-radius: 3px;
   border: 1px solid rgba(150, 150, 150, 0.442);
}

.Swich_Asociacion span {
   width: 100px;
   height: 40px;
   margin-top: 20px;
   display: block;
   background: none;
   color: black;
}

.Swich_Asociacion.active {
   background: rgba(17, 123, 245, 1.0);
   background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   ;
   color: black;
}

.Swich_Asociacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}








/* Movimiento active no */
/* Destino Unico  */
#switchDestinoUnicoPase::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchDestinoUnicoPase.active::after {
   right: unset;
   left: 0;
   content: "No";
}










/* -------------------------------------------------------------- */
/* Asocia Expediente Pase */
#switchAsociaExpedientePase::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociaExpedientePase.active::after {
   right: unset;
   left: 0;
   content: "No";
}









/* -------------------------------------------------------------- */
/* Asocia SIENA  pase */
#switchAsociacionSIENA::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociacionSIENA.active::after {
   right: unset;
   left: 0;
   content: "No";
}



/* -------------------------------------------------------------- */
/* Asocia Unico Item  pase */
#switchAsociaUnicoEEPase::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociaUnicoEEPase.active::after {
   right: unset;
   left: 0;
   content: "No";
}

/* -------------------------------------------------------------- */
/* Asocia Unico Item  pase */
#switchAsociaUnicoEEPase2::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociaUnicoEEPase2.active::after {
   right: unset;
   left: 0;
   content: "No";
}






/* Fin SWITCH */

/* ----------------------------------------------------------------------------- */


/* cuadricula De Documento electronico */
.container_cuadricula_Datos_Pase {
   display: flex;
   justify-content: space-between;
   background-color: #39b3ff;
   width: 98%;
   margin: auto;

   margin-top: 40px;
}

.container_cuadricula_Datos_Pase p {
   margin-left: 20px;
   margin-right: 20px;
   padding-top: 10px;

}







/* ----------------------------------------------------------------------------------------------- */
/* Cuadricula ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS*/
.DatosPaseEEContainer {
   width: 98%;
   margin: auto;
   background-color: rgb(242, 240, 240);
   margin-top: 15px;
   padding: 0px 10px;
   padding-bottom: 10px;
   border: #7b7b7b solid 1px;
   border-radius: 10px;
}

.container_HeaderPase {
   display: flex;
   justify-content: space-between;

}

._dataFiltroPase {
   background-color: #7ab7c7;
   color: white;
   margin-top: 10px;
   padding-top: 5px;
   display: flex;
   justify-content: space-around;
   width: 350px;
}

.btn_dataFiltroPase {
   display: flex;
   margin: 10px;

}

.btn_dataFiltroPase button {
   border: none;
   color: #37bbed;
   font-size: 1.3rem;
   margin: 20 20px;
}

.btn_dataFiltroPase p {
   margin: 0 5px;
   color: gray;
}



.ContainerCuadriculaMotivoInternoPase {
   display: block;
   width: 100%;
   margin-top: 20px;
   border: #6a6969 1px solid;
   text-align: center;
}

.HeaderCuadriculaMotivoInternoPase {
   background-color: #39b3ff;

   height: 40px;
   font-size: large;
   text-decoration: double;
   color: white;
}

.OutputCuadriculaMotivoInternoPase {
   height: 250px;
}





/* -------------------------------------------------------------------- */


/* Botones de accion con ese nuevo proceso */
.container_btn_Proceso_Pase {
   display: flex;
   justify-content: space-between;
   width: 98%;
   margin: auto;
   margin-top: 50px;
   margin-bottom: 30px;
}

.Cancelar_Proceso_Pase {
   border-radius: 5px;
   width: 300px;
   height: 40px;
   border: solid 1px rgb(79, 107, 79);
   color: rgb(79, 107, 79);
}

.Procesar_Proceso_Pase {
   background-color: #9291a2;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}

.Guardar_Proceso_Pase {
   background-color: #39b3ff;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}

/* media querys */
@media screen and (max-width: 1400px) {
   .container_Inputs_Entrada_Data_Pase {
      display: flex;
      justify-content: space-around;
      margin: auto;
      margin-right: 50px;
   }

   .div_Inputs_Entrada_Data_Pase {
      width: 200px;
      margin: 0 20px 0 50px;
   }

   .div_Inputs_Entrada_Data_Pase input {
      width: 300px;
   }

   .grupo_Entrada_Data_Pase {
      width: 100% !important;
   }

}
</style>


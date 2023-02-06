<template>
   <!-- Este va a ser el apartado de caratulacion -->
   <div class="Alta_Expedientes_Caratulacion_Conteiner" id="Container_total_Caratulacion">
      <!-- encabezado y fecha -->
      <div class="Encabezado_Alta_Expediente_Caratulacion">
         <span id="" style="font-size:1.4rem;">ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS</span>
         <p>fecha: {{ currentDate }}</p>
      </div>
      <!-- referencias de proceso -->
      <div class="Referencia_Proceso_Caratulacion_Expedientes">
         <p>Nro. Lote</p>
         <p>Estado <span> <strong>Pendiente</strong> </span> </p>
         <p>Usuario <span> <strong> Apellido/s y Nombre/s</strong></span></p>
         <p>Tipo Proceso <span> <strong> Firma</strong></span> </p>
      </div>
      <!-- inputs de seleccion de referencia para generar expediente -->
      <div class="container_Inputs_Entrada_Data_Caratulacion">
         <!-- Input Referencia -->
         <div class="div_Inputs_Entrada_Data_Caratulacion form-control">
            <p>Referencia</p>
            <input type="text" class="grupo_Entrada_Data_Caratulacion" required style="width: 100%; height: 40px;"
               id="referencia_alta_proceso_masivo_firma" v-model="referenciaCaratulacion" />
         </div>
         <!-- Firmante -->
         <div class="div_Inputs_Entrada_Data_Caratulacion form-control">
            <p> Firmante</p>
            <div class=" grupo_Entrada_Data_Caratulacion " role="group">
               <!-- Chequear su existencia en GDE. Selección única -->
               <input type="text" style="width: 100%; height: 40px;" id="firmante_alta_proceso_masivo_firma"
                  v-model="firmanteCaratulacion" />
            </div>
         </div>
         <!--Button Tipo de Documento  -->
         <div class="div_Inputs_Entrada_Data_Caratulacion form-control" role="group">
            <p>Tipo de Documento</p>
            <div class=" grupo_Entrada_Data_Caratulacion" role="group">
               <select class="selectDataAlta" name="Seleccionar" id="" style="width:100%; height: 40px;"
                  v-model="tipoDocumentoCaratulacion">
                  <option value="IDCIN">IDCIN</option>
                  <option value="IFGRA">IFGRA</option>
                  <option value="CROQU">CROQU </option>
                  <option value="FPCCA">FPCCA</option>
                  <option value="" selected hidden>Seleccionar...</option>
               </select>
            </div>
         </div>
      </div>


      <!-- SWITCHCaratulacion -->
      <div class="container_Permite_Asociacion_Caratulacion container_Permite_Asociacion_Caratulacion2">
         <div class="div_Permite_Asociacion_Caratulacion2 ">
            <p>¿Trata Única?</p>
            <button class="Swich_Asociacion" id="switchTrataUnicaCaratulacion" @click="toggleClassTrataUnica"
               v-bind:class="addedClassTrataUnica"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Caratulacion2">
            <p>¿Asocia Expediente?</p>
            <button class="Swich_Asociacion" id="switchAsociaExpedienteCaratulacion"
               @click="toggleClassAsociaExpediente"
               v-bind:class="addedClassAsociaExpediente"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Caratulacion2">
            <p>¿Requiere Asociación SIENA?</p>
            <button class="Swich_Asociacion" id="switchAsociacionSIENACaratulacion" @click="toggleClassAsociaSiena"
               v-bind:class="addedClassAsociaSiena"><span>No</span><span>Si</span></button>
         </div>

      </div>

      <!--div trata y motivo  -->

      <div class="container_Permite_Asociacion_Caratulacion container_Permite_Asociacion_Caratulacion2">

         <div class="div_Inputs_Entrada_Data_Caratulacion Inputs_btnAsocia_Unico_Item animate__animated form-control"
            id="TrataCaratulacion">
            <p>Trata</p>
            <div class=" grupo_Entrada_Data_Caratulacion">
               <select class="select_Data_Alta" id="" style="width: 100%; height: 40px;" v-model="trataCaratulacion">
                  <option>Seleccionar</option>
               </select>
            </div>
         </div>
         <div class="div_Permite_Asociacion_Caratulacion2" id="divContainerAsociacionUnicaEECaratulacion"
            v-bind:class="addedClassAsociacionUnicoEEContainerCaratulacion">
            <p> <strong> ¿Asocia a un unico EE</strong></p>
            <button class="Swich_Asociacion" id="switchMotivoInternoEECaratulacion"
               @click="toggleClassAsociaUnicoEECaratulacion"
               v-bind:class="addedClassAsociaUnicoEECaratulacion"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Caratulacion2">
            <p>¿Motivo Interno y Descripción <br>
               Adicional del tramite coinciden ?</p>
            <button class="Swich_Asociacion" id="switchMotivoInternoCaratulacion" @click="toggleClassMotivoInterno"
               v-bind:class="addedClassMotivoInterno"><span>No</span><span>Si</span></button>
         </div>

      </div>
      <div class="container_Permite_Asociacion_Caratulacion container_Permite_Asociacion_Caratulacion2">


         <div class="div_Inputs_Entrada_Data_Caratulacion form-control"
            v-bind:class="addedClassContainerExpedienteElectronicoCaratulacion"
            id="ContainerExpedienteElectronicoCaratulacion">
            <div>
               <label for=""> <strong> Expediente Electrónico</strong></label>
            </div>
            <div>
               <input type="text" placeholder="EX-2017-22671255- -APN-DMEYD#AABE" v-model="numExpedienteCaratulacion" />
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
      <div class="container_btn_Proceso_Caratulacion" id="Alta_firma_container_btn">
         <button class="Cancelar_Proceso_Caratulacion btn btn-danger" id="">X Cancelar </button>
         <button class="Procesar_Proceso_Caratulacion btn btn-primary" id="" @click="guardarBaseCaratulacion"> Procesar
         </button>
         <button class="Guardar_Proceso_Caratulacion btn btn-success" @click="guardarCaratulacion"> Guardar </button>
      </div>
   </div>
</template>


<script>
import moment from 'moment';
import axios from 'axios';
export default {
   name: 'AltaCaratulacion',
   data() {
      return {

         //tipo ALTa
         TipoAlta: 'Caratulacion Masiva',

         estadoLote: 'Pendiente',
         usuario: 'DevTest',
         // class de btn reactivo
         addedClassTrataUnica: '',
         addedClassAsociaExpediente: '',
         addedClassAsociaSiena: '',
         addedClassMotivoInterno: '',


         // Reactive btn container
         addedClassAsociacionUnicoEEContainerCaratulacion: '',
         addedClassContainerExpedienteElectronicoCaratulacion: '',
         addedClassAsociaUnicoEECaratulacion: '',

         // localStorage

         referenciaCaratulacion: "",
         firmanteCaratulacion: "",
         tipoDocumentoCaratulacion: "",
         trataCaratulacion: '',
         numExpedienteCaratulacion: '',
         // personas: []

         // btn localstorage
         buttonTrataUnicaCaratulacion: false,
         buttonAsociaExpedienteCaratulacion: false,
         buttonAsociaSienaCaratulacion: false,
         buttonAsociaUnicoEECaratulacion: false,
         buttonAMotivoInternoCaratulacion: false,


         // localsotagetable
         localStorageData: null,



         //DataTime
         currentDate: moment().format('YYYY-MM-DD')
      }
   },
   methods: {

      // Localstorage





      // botones reactivos
      toggleClassTrataUnica() {
         this.addedClassTrataUnica = this.addedClassTrataUnica === 'active' ? '' : 'active'
         // btn localstorage
         this.buttonTrataUnicaCaratulacion = !this.buttonTrataUnicaCaratulacion
      },
      toggleClassAsociaExpediente() {
         this.addedClassAsociaExpediente = this.addedClassAsociaExpediente === 'active' ? '' : 'active'
         // Estos activan los container de asociacion unico ee que solo se tiene que mostrar cuando el btn este activo
         this.addedClassAsociacionUnicoEEContainerCaratulacion = this.addedClassAsociacionUnicoEEContainerCaratulacion === 'active' ? '' : 'active'
         this.addedClassContainerExpedienteElectronicoCaratulacion = this.addedClassContainerExpedienteElectronicoCaratulacion === 'active' ? '' : 'active'
         // btn localstorage
         this.buttonAsociaExpedienteCaratulacion = !this.buttonAsociaExpedienteCaratulacion
      },
      toggleClassAsociaSiena() {
         this.addedClassAsociaSiena = this.addedClassAsociaSiena === 'active' ? '' : 'active'
         // btn localstorage
         this.buttonAsociaSienaCaratulacion = !this.buttonAsociaSienaCaratulacion
      },
      toggleClassMotivoInterno() {
         this.addedClassMotivoInterno = this.addedClassMotivoInterno === 'active' ? '' : 'active'
         // btn localstorage
         this.buttonAMotivoInternoCaratulacion = !this.buttonAMotivoInternoCaratulacion
      },

      toggleClassAsociaUnicoEECaratulacion() {
         this.addedClassAsociaUnicoEECaratulacion = this.addedClassAsociaUnicoEECaratulacion === 'active' ? '' : 'active'
         // btn localstorage
         this.buttonAsociaUnicoEECaratulacion = !this.buttonAsociaUnicoEECaratulacion
      },


      // localstorage
      guardarCaratulacion() {
         // tipo documento select
         localStorage.setItem("tipo_documento", this.tipoDocumentoCaratulacion);

         // const persona = { referencia: this.referencia, firmante: this.firmante };
         // this.personas.push(persona);
         // valores de inputs iniciales
         localStorage.setItem("referencia", this.referenciaCaratulacion);
         localStorage.setItem("firmante", this.firmanteCaratulacion);
         //   trata unica
         localStorage.setItem("Trata", this.trataCaratulacion);


         // brn guardados 
         if (this.buttonTrataUnicaCaratulacion) {
            localStorage.setItem('Trata_Unica', this.buttonTrataUnicaCaratulacion)

         } else {
            localStorage.removeItem('Trata_Unica')

         }
         //  btnValor
         if (this.buttonAsociaExpedienteCaratulacion) {
            localStorage.setItem('Asocia_Expediente', this.buttonAsociaExpedienteCaratulacion)

         } else {
            localStorage.removeItem('Asocia_Expediente')

         }
         if (this.buttonAsociaSienaCaratulacion) {
            localStorage.setItem('Asocia_Siena', this.buttonAsociaSienaCaratulacion)

         } else {
            localStorage.removeItem('Asocia_Siena')

         }
         if (this.buttonAsociaUnicoEECaratulacion) {
            localStorage.setItem('Asocia_Unico_Expediente_EE', this.buttonAsociaUnicoEECaratulacion)

         } else {
            localStorage.removeItem('Asocia_Unico_Expediente_EE')

         }
         if (this.buttonAsociaExpedienteCaratulacion) {
            localStorage.setItem('buttonAsociaUnicoItem', JSON.stringify(this.buttonAsociaUnicoItem))
            // entidad
            localStorage.setItem("entidad", this.entidad);
            // tipoDocumentoSiena
            localStorage.setItem("tipoDocumentoSiena", this.tipoDocumentoSiena);
         } else {
            localStorage.removeItem('buttonAsociaUnicoItem')
            localStorage.removeItem('tipoDocumentoSiena')
            localStorage.removeItem('entidad')
         }

         // Tira valores dentro de la tabla localStorage  
         this.localStorageData = {};
         for (let i = 0; i < localStorage.length; i++) {
            let key = localStorage.key(i);
            this.localStorageData[key] = localStorage.getItem(key);
         }

      },
      guardarBaseCaratulacion() {
         const altasCaratulacion = {
            firmante: this.firmanteCaratulacion,
            referencia: this.referenciaCaratulacion,
            tipoDocumento: this.tipoDocumentoCaratulacion,
            requiereAsociacionSiena: this.buttonAsociaSienaCaratulacion,
            asociaExpediente: this.buttonAsociaExpedienteCaratulacion,
            trataUnica: this.buttonTrataUnicaCaratulacion,
            motivoInternoDescripcionAdicionalCoinciden: this.buttonAMotivoInternoCaratulacion,
            trata: this.trataCaratulacion,

         };
         const altaFirmasPadre = {
            referencia: this.referenciaCaratulacion,
            firmante: this.firmanteCaratulacion,
            TipoProceso: this.TipoAlta,
            Usuario: this.usuario,
            EstadoLote: this.estadoLote,
         };
         axios.post("https://localhost:5001/api/AltaPadre", altaFirmasPadre).then(response => {
            console.log(response);
         }).catch(error => {
            console.error(error);
         });
         axios.post("https://localhost:5001/api/GDE_Caratulacion", altasCaratulacion).then(response => {
            console.log(response);
         }).catch(error => {
            console.error(error);
         });

      },

      computed: {
         fechaFormatada() {
            return this.fecha.toLocaleString();
         }
      }
   }
}


</script>

<style lang="css" scoped>
/* Proceso de alta de expedientes */
.Alta_Expedientes_Caratulacion_Conteiner {
   display: block;
   width: 98%;
   margin: auto;
   background-color: white;
   border: 1px solid gray;
   margin-top: 30px;
   border-radius: 5px;
}


.Encabezado_Alta_Expediente_Caratulacion {
   display: flex;
   justify-content: space-between;
   margin: 0 400px 0 20px;
   color: grey;
}

/* proceso de referencias de datos Nro.Lote Estado Usuario Tipo proceso */
.Referencia_Proceso_Caratulacion_Expedientes {
   display: flex;
   justify-content: space-around;
   color: gray;
}

.Referencia_Proceso_Caratulacion_Expedientes p span {
   color: black;

}

/* inputs y buttons referencias y datos de nuevo expediente */
.container_Inputs_Entrada_Data_Caratulacion {
   display: flex !important;

   margin: auto;
}

.div_Inputs_Entrada_Data_Caratulacion {


   margin: 0 20px 0 30px;
}

.div_Inputs_Entrada_Data_Caratulacion p {
   font-size: 1.2rem;
   color: gray;

}

.div_Inputs_Entrada_Data_Caratulacion button {
   width: 500px;
   text-align: start;
}

.div_Inputs_Entrada_Data_Caratulacion input {
   width: 600px;
}

.grupo_Entrada_Data_Caratulacion {
   margin-top: -10px;
   text-align: start;
   height: 40px;

}

.selectDataAlta {
   width: 500px;
}

.btn_ProcesoCaratulacion {
   color: gray;
}

/* No requiere asociacion */
.container_CaratulacionNoAsociacion {
   display: block !important;
}

.div_NoPermiteAsociacionCaratulacion {
   display: flex;
}

.div_NoPermiteAsociacionCaratulacion div {
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

.container_Permite_Asociacion_Caratulacion {
   display: flex;
   justify-content: space-between;
   margin: auto;
   margin: 50px 100px 0px 200px;
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

.div_Permite_Asociacion_Caratulacion {
   font-size: 1.1rem;
}

.div_Permite_Asociacion_Caratulacion button {
   background-color: #65b2e2;
   border: none;
   padding: 10px 50px 10px 0px;
   color: white;
}

.div_Permite_Asociacion_Caratulacion2 {
   margin-top: -20px;
}

.div_Permite_Asociacion_Caratulacion2 button {
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







/* -------------------------------------------------------------- */
/* TrataUnicaCaratulacion */
#switchTrataUnicaCaratulacion::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchTrataUnicaCaratulacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}




/* Asocia Expediente Caratulacion */
#switchAsociaExpedienteCaratulacion::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociaExpedienteCaratulacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}




/* -------------------------------------------------------------- */
/* Asocia SIENA  Caratulacion */
#switchAsociacionSIENACaratulacion::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchAsociacionSIENACaratulacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}



/* -------------------------------------------------------------- */
/* Asocia Unico Item  Caratulacion */
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
/* Asocia Unico Item  Caratulacion */
#divContainerAsociacionUnicaEECaratulacion {
   display: none;
}

#divContainerAsociacionUnicaEECaratulacion.active {
   display: block;
}

#ContainerExpedienteElectronicoCaratulacion {
   display: none;
}

#ContainerExpedienteElectronicoCaratulacion.active {
   display: block;
   width: fit-content;
   display: block;
   margin: auto;
}

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



/* Asocia Motivo Interno  Caratulacion */
#switchMotivoInternoCaratulacion::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchMotivoInternoCaratulacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}

/* Asocia Motivo Interno  Caratulacion */
#switchMotivoInternoEECaratulacion::after {
   top: 0;
   right: 0;
   left: unset;
}

#switchMotivoInternoEECaratulacion.active::after {
   right: unset;
   left: 0;
   content: "No";
}




/* Fin SWITCH */

/* ----------------------------------------------------------------------------- */


/* cuadricula De Documento electronico */
.container_cuadricula_Datos_Caratulacion {
   display: flex;
   justify-content: space-between;
   background-color: #39b3ff;
   width: 98%;
   margin: auto;

   margin-top: 40px;
}

.container_cuadricula_Datos_Caratulacion p {
   margin-left: 20px;
   margin-right: 20px;
   padding-top: 10px;

}

/* Botones de accion con ese nuevo proceso */
.container_btn_Proceso_Caratulacion {
   display: flex;
   justify-content: space-between;
   width: 98%;
   margin: auto;
   margin-top: 50px;
   margin-bottom: 30px;
}

.Cancelar_Proceso_Caratulacion {
   border-radius: 5px;
   width: 300px;
   height: 40px;
   border: solid 1px rgb(79, 107, 79);
   color: rgb(79, 107, 79);
}

.Procesar_Proceso_Caratulacion {
   background-color: #9291a2;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}

.Guardar_Proceso_Caratulacion {
   background-color: #39b3ff;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}

#divTablaAltaProcesoMasivoDeFirma {
   display: flex;
   margin: auto;
}

/* tabla reactiva */
#divTablaAltaProcesoMasivoDeFirma table {
   width: fit-content;
   display: flex;
   margin-bottom: 100px;
   border: solid 1px rgb(113, 112, 112);
   border-top-left-radius: 1px;
   border-top-right-radius: 1px;
}


#divTablaAltaProcesoMasivoDeFirma table tr td {
   display: block;


}

tr #headerTabla {
   background-color: #1597e8;
   border: 1px solid gray;
   width: 100%;
   height: 100%;
   padding: 10px;

}

tr #tablavalue {
   background-color: #ffffff;
   border: 1px solid rgba(128, 128, 128, 0.448);
   width: 100%;
   height: 50px;
   padding: 10px;

}


/* media querys */
@media screen and (max-width: 1400px) {
   .container_Inputs_Entrada_Data_Caratulacion {
      display: flex;
      justify-content: space-around;
      margin: auto;
      margin-right: 50px;
   }

   .div_Inputs_Entrada_Data_Caratulacion {
      width: 200px;
      margin: 0 20px 0 50px;
   }

   .div_Inputs_Entrada_Data_Caratulacion input {
      width: 300px;
   }


}




#TrataCaratulacion {
   max-width: 500px !important;
}







/* Cuadricula ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS*/
.Datos_CaratulacionEE_Container {
   width: 98%;
   margin: auto;
   background-color: rgb(242, 240, 240);
   margin-top: 15px;
   padding: 0px 10px;
   padding-bottom: 10px;
   border: #7b7b7b solid 1px;
   border-radius: 10px;
}

.container_Header_Cuadricula {
   display: flex;
   justify-content: space-between;

}

._data_Filtro_Caratulacion {
   color: gray;
   margin-top: 10px;
}

.btn_data_Filtro_Caratulacion {
   display: flex;
   margin: 10px;
}

.btn_data_Filtro_Caratulacion button {
   border: none;
   color: #37bbed;
   font-size: 1.3rem;
   margin: 20 20px;
}

.btn_data_Filtro_Caratulacion p {
   margin: 0 5px;
   color: gray;
}

/* cuadricula interna motivo Interno */
.Container_Cuadricula_Motivo_Interno_Caratulacion {
   display: block;
   width: 100%;
   margin-top: 20px;
   border: #6a6969 1px solid;
   text-align: center;
}

.Header_Cuadricula_Motivo_Interno_Caratulacion {
   background-color: #39b3ff;

   height: 40px;
   font-size: large;
   text-decoration: double;
   color: white;
}

.Output_Cuadricula_Motivo_Interno_Caratulacion {
   height: 250px;
}
</style>


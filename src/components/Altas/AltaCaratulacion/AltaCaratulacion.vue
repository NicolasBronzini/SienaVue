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
      <div class="container" id="divTablaAltaProcesoMasivoDeFirma" style="margin-top:50px;">
         <table>
            <tr v-for="(value, key) in localStorageData" :key="key">
               <td id="headerTabla">{{ key }}</td>
               <td id="tablavalue">{{ value }}</td>
            </tr>
         </table>
      </div>
      <!-- Botones de accion con ese nuevo proceso -->
      <div class="container_btn_Proceso_Caratulacion" id="Alta_firma_container_btn">
         <button class="Cancelar_Proceso_Caratulacion btn btn-danger" style="color: white;">X Cancelar </button>
         <button class="Procesar_Proceso_Caratulacion btn btn-primary" id="" @click="guardarBaseCaratulacion"> Procesar
         </button>
         <button class="Guardar_Proceso_Caratulacion btn btn-success" @click="guardarCaratulacion"> Guardar </button>
      </div>
   </div>
</template>

<script>
import moment from 'moment';
import axios from 'axios';
import './styles.css';

export default {
   name: 'AltaCaratulacion',
   data() {
      return {
         showAltaProcesosMasivos: false,

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
         const altaCaratulacion = {
            botonTrataUnica: this.buttonTrataUnicaCaratulacion,
            botonAsociaExpediente: this.buttonAsociaExpedienteCaratulacion,
            botonAsociaSiena: this.buttonAsociaSienaCaratulacion,
            botonAsociaUnico: this.buttonAsociaUnicoEECaratulacion,
            botonMotivoInterno: this.buttonAMotivoInternoCaratulacion,
            referencia:  this.referenciaCaratulacion,
            firmante: this.firmanteCaratulacion,
            tipoDocumento: this.tipoDocumentoCaratulacion,
            trata: this.trataCaratulacion,
         }

         localStorage.setItem('AltaCaratulacion', JSON.stringify(altaCaratulacion))

         // TODO: mostrar tabla
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


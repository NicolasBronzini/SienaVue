<template>
   <!-- Este apartado es el de Vincular -->
   <div class="Alta_Expedientes_Vincular_Conteiner" id="Container_total_Vinculacion">
      <!-- encabezado y fecha -->
      <div class="Encabezado_Alta_Expediente_Vincular">
         <span id="" style="font-size:1.4rem;">VINCULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS</span>
         <p>fecha: {{ currentDate }}</p>
      </div>
      <!-- referencias de proceso -->
      <div class="Referencia_Proceso_Vincular_Expedientes">
         <p>Nro. Lote</p>
         <p>Estado <span> <strong>Pendiente</strong> </span> </p>
         <p>Usuario <span> <strong> Apellido/s y Nombre/s</strong></span></p>
         <p>Tipo Proceso <span> <strong> Firma</strong></span> </p>
      </div>
      <!-- inputs de seleccion de referencia para generar expediente -->
      <div class="container_Inputs_Entrada_Data_Vincular">
         <!-- Input Referencia -->
         <div class="div_Inputs_Entrada_Data_Vincular Inputs_btnAsocia_Unico_Item  form-control">
            <p>Referencia</p>
            <input type="text" class="grupo_Entrada_Data_Vincular" required style="width: 100%; height: 40px;"
               v-model="referenciaVinculacion" />
         </div>
         <!-- Firmante -->
         <div class="div_Inputs_Entrada_Data_Vincular Inputs_btnAsocia_Unico_Item  form-control">
            <p> Firmante</p>
            <div class=" grupo_Entrada_Data_Vincular" role="group">
               <input type="text" class="grupo_Entrada_Data_Vincular" required style="width: 100%; height: 40px;"
                  v-model="firmanteVinculacion" />
            </div>
         </div>
         <!--Button Tipo de Documento  -->
         <div class="div_Inputs_Entrada_Data_Vincular Inputs_btnAsocia_Unico_Item  form-control">
            <p>Tipo de Documento</p>
            <div class=" grupo_Entrada_Data_Vincular" role="group">
               <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;"
                  v-model="tipoDocuVinculacion">
                  <option>IDCIN</option>
                  <option>IFGRA</option>
                  <option>CROQU </option>
                  <option>FPCCA</option>
                  <option class="Seleccionar_Option" selected>Seleccionar</option>
               </select>
            </div>
         </div>
      </div>
      <!-- ubicacion Phath:     permite asociacion -->

      <!-- SWITCH DE TESTEO Y ASOCIACION-->
      <div class="container_Permite_Asociacion_Vincular container_Permite_Asociacion_Vincular2">
         <div class="div_Permite_Asociacion_Vincular2">
            <p>¿Asocia a un único EE principal?</p>
            <button class="Swich_Asociacion" id="SwitchAsociaUnicoEEPrincipalVincular"
               @click="toggleClassAsociacionUnicoEEVinculacion"
               v-bind:class="addedClassAsociacionUnicoEEVinculacion"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Vincular2">
            <p>¿Requiere Asociación SIENA?</p>
            <button class="Swich_Asociacion" id="SwitchAsociaSienaVincular"
               @click="toggleClassAsociacionSienaVinculacion"
               v-bind:class="addedClassAsociacionSienaVinculacion"><span>No</span><span>Si</span></button>
         </div>
         <div class="div_Permite_Asociacion_Vincular2">
            <p>¿Asocia a un único Item?</p>
            <button class="Swich_Asociacion" id="SwitchAsociaUnicoItemVincular"
               @click="toggleClassAsociacionUnicoItemVinculacion"
               v-bind:class="addedClassAsociacionUnicoItemVinculacion"><span>No</span><span>Si</span></button>
         </div>
      </div>
      <!-- Expediente electronico Firmante  -->

      <div class="container_Inputs_Entrada_Data_Vincular" id="ContainerVincularInputsEE">
         <!-- Input Referencia -->
         <div class="div_Inputs_Entrada_Data_Vincular   form-control" id="ExpedienteElectronicoVincular">
            <p>Expediente Electronico</p>
            <input type="text" class="grupo_Entrada_Data_Vincular" required
               placeholder="Ex-Año-XXXXXXXX-APN-Reparticion" style="width: 100%; height: 40px;"
               v-model="expedienteVinculacion" />
         </div>
         <!-- Firmante -->
         <div class="div_Inputs_Entrada_Data_Vincular form-control" id="EntidadVincularEE">
            <p> Entidad</p>
            <div class=" grupo_Entrada_Data_Vincular" role="group">
               <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;"
                  v-model="entidadVinculacion">
                  <!-- Chequear su existencia en GDE. Selección única -->
                  <option class="Seleccionar_Option" selected disabled>Seleccionar</option>
                  <option>nombre de firmante</option>
               </select>
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
      <div class="container_btn_Proceso_Vincular" id="">
         <button class="Cancelar_Proceso_Vincular btn btn-danger" id="">X Cancelar </button>
         <button class="Procesar_Proceso_Vincular btn btn-primary" id="" @click="guardarBasePase"> Procesar </button>
         <button class="Guardar_Proceso_Vincular btn btn-success" id="" @click="guardarTipo"> Guardar </button>
      </div>
   </div>
</template>

<script>
import moment from 'moment';
import axios from 'axios';
import './styles.css'

export default {
   name: 'AltaVinculacion',
   data() {
      return {
         addedClassAsociacionUnicoItemVinculacion: '',
         addedClassAsociacionSienaVinculacion: '',
         addedClassAsociacionUnicoEEVinculacion: '',

         // localStorage

         referenciaVinculacion: "",
         firmanteVinculacion: "",
         tipoDocuVinculacion: "",
         expedienteVinculacion: '',
         entidadVinculacion: '',
         // personas: []

         // btn localstorage
         buttonAsociaUnicoEEVinculacion: false,
         buttonRequiereAsociacionVinculacion: false,
         buttonAsociaUnicoVinculacion: false,



         // localsotagetable
         localStorageData: null,


         //DataTime
         currentDate: moment().format('YYYY-MM-DD')
      }
   },
   methods: {
      // toggleClassAsociacionUnicoEEVinculacion() {
      //    this.addedClassAsociacionUnicoEEVinculacion = this.addedClassAsociacionUnicoEEVinculacion === 'active' ? '' : 'active'
      //    this.buttonAsociaUnicoEEVinculacion = !this.buttonAsociaUnicoEEVinculacion
      // },
      // toggleClassAsociacionSienaVinculacion() {
      //    this.addedClassAsociacionSienaVinculacion = this.addedClassAsociacionSienaVinculacion === 'active' ? '' : 'active'
      //    this.buttonRequiereAsociacionVinculacion = !this.buttonRequiereAsociacionVinculacion
      // },


      // toggleClassAsociacionUnicoItemVinculacion() {
      //    this.addedClassAsociacionUnicoItemVinculacion = this.addedClassAsociacionUnicoItemVinculacion === 'active' ? '' : 'active'
      //    this.buttonAsociaUnicoVinculacion = !this.buttonAsociaUnicoVinculacion
      // },


      // localstorage
      guardarTipo() {
         // tipo documento select
         localStorage.setItem("Tipo_documento", this.tipoDocuVinculacion);

         // const persona = { referencia: this.referencia, firmante: this.firmante };
         // this.personas.push(persona);
         // valores de inputs iniciales
         localStorage.setItem("Referencia", this.referenciaVinculacion);
         localStorage.setItem("Firmante", this.firmanteVinculacion);

         // brn guardados 
         if (this.buttonAsociaUnicoEEVinculacion) {
            localStorage.setItem('Asocia_a_un_unico_EE_principal', this.buttonAsociaUnicoEEVinculacion)

         } else {
            localStorage.removeItem('Asocia_a_un_unico_EE_principal')

         }
         if (this.buttonRequiereAsociacionVinculacion) {
            localStorage.setItem('Requiere_Asociacion_SIENA', this.buttonRequiereAsociacionVinculacion)

         } else {
            localStorage.removeItem('Requiere_Asociacion_SIENA')

         }
         if (this.buttonAsociaUnicoVinculacion) {
            localStorage.setItem('Asocia_a_un_unico_item', this.buttonAsociaUnicoVinculacion)

         } else {
            localStorage.removeItem('Asocia_a_un_unico_item')

         }

         // Tira valores dentro de la tabla localStorage  
         this.localStorageData = {};
         for (let i = 0; i < localStorage.length; i++) {
            let key = localStorage.key(i);
            this.localStorageData[key] = localStorage.getItem(key);
         }

      },
      guardarBaseFirma() {
         const altasVinculacion = {
            Referencia: this.referenciaVinculacion,
            Firmante: this.firmanteVinculacion,
            TipoDocumento: this.tipoDocuVinculacion,
            expedienteElectronico: this.asociaUnicoItem,
            asociaUnicoEEPrincipal: this.buttonAsociaUnicoEEVinculacion,
            requiereAsociacionSiena: this.buttonRequiereAsociacionVinculacion,
            asociaUnicoItem: this.buttonAsociaUnicoVinculacion,
            Entidad: this.entidadVinculacion,
            TipoDocumentoSiena: this.tipoDocumentoSiena,


         }
         // const altaFirmasPadre = {
         //    Referencia: this.referencia,
         //    Firmante: this.firmante,
         //    TipoProceso: this.TipoAlta,
         //    Usuario: this.usuario,
         //    EstadoLote: this.estadoLote,
         // }
         axios.post("https://localhost:5001/api/GDE_Vinculacion", altasVinculacion).then(response => {
            console.log(response);
         }).catch(error => {
            console.error(error);
         });

      }
   }
}

</script>



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
         <button class="Procesar_Proceso_Pase btn btn-primary" id="" @click="guardarBasePase"> Procesar </button>
         <button class="Guardar_Proceso_Pase btn btn-success" id=""> Guardar </button>
      </div>
   </div>
</template>

<script>
import moment from 'moment';
import axios from 'axios';
import './styles.css';

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
      },
      guardarBasePase() {
         const altasFirma = {
            Referencia: this.referencia,
            Firmante: this.firmante,
            TipoDocumento: this.tipoDocumento,
            PermiteAsociacion: this.buttonPerimteAsociacion,
            AsociaUnicoItem: this.buttonAsociaUnicoItem,
            Entidad: this.entidad,
            TipoDocumentoSiena: this.tipoDocumentoSiena,
         }
         // const altaFirmasPadre = {
         //    Referencia: this.referencia,
         //    Firmante: this.firmante,
         //    TipoProceso: this.TipoAlta,
         //    Usuario: this.usuario,
         //    EstadoLote: this.estadoLote,
         // }
         axios.post("https://localhost:5001/api/GDE_Pase", altasFirma).then(response => {
            console.log(response);
         }).catch(error => {
            console.error(error);
         });

      }
   },

   computed: {
      fechaFormatada() {
         return this.fecha.toLocaleString();
      }
   }
}
</script>
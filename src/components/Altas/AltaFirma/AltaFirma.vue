<template>
    <!-- Este va a ser el apartado de pase -->

    <!-- Apartado alta de Firma de EE -->
    <div class="Alta_Expedientes_Firma_Conteiner" id="Container_total_Firma">
        <!-- encabezado y fecha -->
        <div class="Encabezado_Alta_Expediente_Firma">
            <span id="tituloModificarOption" style="font-size:1.4rem;">ALTA PROCESO MASIVO DE FIRMA</span>
            <p>fecha: {{ currentDate }}</p>
        </div>
        <!-- referencias de proceso -->
        <div class="Referencia_Proceso_Firma_Expedientes">
            <p>Nro. Lote</p>
            <p>Estado <span> <strong>Pendiente</strong> </span> </p>
            <p>Usuario <span> <strong> Apellido/s y Nombre/s</strong></span></p>
            <p>Tipo Proceso <span> <strong> Firma</strong></span> </p>
        </div>
        <!-- inputs de seleccion de referencia para generar expediente -->
        <div class="container_Inputs_Entrada_Data_Firmante">
            <!-- Input Referencia -->
            <div class="div_Inputs_Entrada_Data_Firmante form-control">
                <p>Referencia</p>
                <input type="text" class="grupo_Entrada_Data_Firma" style="max-width: 500px; height: 40px;"
                    id="referencia_alta_proceso_masivo_firma" v-model="referencia" />
            </div>
            <!-- Firmante -->
            <div class="div_Inputs_Entrada_Data_Firmante form-control">
                <p> Firmante</p>
                <div class=" grupo_Entrada_Data_Firma " role="group">
                    <!-- Chequear su existencia en GDE. Selección única -->
                    <input type="text" style="max-width: 500px; height: 40px;" id="firmante_alta_proceso_masivo_firma"
                        v-model="firmante" />
                </div>
            </div>
            <!--Button Tipo de Documento  -->
            <div class="div_Inputs_Entrada_Data_Firmante form-control">
                <p>Tipo de Documento</p>
                <div class="btn-group grupo_Entrada_Data_Firma" role="group">
                    <select class="selectDataAlta" name="Seleccionar" id="tipoDeDocumento_alta_proceso_masivo_firma"
                        v-model="tipoDocumento">
                        <option value="IDCIN">IDCIN</option>
                        <option value="IFGRA">IFGRA</option>
                        <option value="CROQU">CROQU </option>
                        <option value="FPCCA">FPCCA</option>
                        <option value="" selected hidden>Seleccionar...</option>
                    </select>
                </div>
            </div>
        </div>
        <!-- ubicacion Phath:     permite asociacion -->
        <div
            class="container_Permite_Asociacion_Firma container_Permite_Asociacion_Firma2  animate__animated animate__fadeIn">
            <div class="div_Permite_Asociacion_Firma" id="UbicacionPath2">
                <button id="path_alta_proceso_masivo_firma">+ Ubicacion</button> Path:
            </div>

            <!-- SWITCH -->

            <div class="div_Permite_Asociacion_Firma Inputs_btnAsocia_Unico_Item animate__animated animate__fadeIn form-control "
                id="InputActiveEntidad" v-bind:class="addedClassSelectContainerEntidad">
                <p>Entidad</p>
                <div class="btn-group grupo_Entrada_Data_Firma Select_Asociacion_Alta_Firma" role="group">
                    <select class="select_Data_Alta" id="SelectInmueble" name="Seleccionar"
                        style="width:100%; height: 40px;" v-model="entidad">
                        <option value="" selected hidden>Seleccionar...</option>
                        <option value="Inmueble">Inmueble</option>
                        <option value="Contrato">Contrato</option>
                        <option value="Dominio">Dominio</option>
                        <option value="Catastro">Catastro</option>
                        <option value="Titulo">Titulo</option>
                        <option value="Operaciones">Operaciones</option>
                    </select>
                </div>
            </div>
            <div class="div_Permite_Asociacion_Firma2 btn_Unico_Item "
                v-bind:class="addedClassAsociacionUnicoItemContainerFirma">
                <p>¿Asocia a único item?</p>
                <button class="Swich_Item_Unico" id="SwichItemUnico" @click="toggleClassAsociaUnicoItem"
                    v-bind:class="addedClassAsociaUnicoItem"><span>No</span><span>Si</span></button>
            </div>
            <div class="div_Permite_Asociacion_Firma2">
                <p>¿Permite Asociación?</p>
                <button class="Swich_Asociacion" id="SwichAsociacion" @click="toggleClassAsociacionFirma"
                    v-bind:class="addedClassAsociacionFirma"><span>No</span><span>Si</span></button>
            </div>
        </div>
        <!-- Tipo de docuemento SIENA -->
        <div class="div_Inputs_Entrada_Data_Firmante Inputs_btnAsocia_Unico_Item animate__animated animate__fadeIn form-control"
            id="div_InputTipoDocumentoSIENA" v-bind:class="addedClassTipoDocumentoSiena">
            <p>Tipo de documento SIENA</p>
            <div class="btn-group grupo_Entrada_Data_Firma">
                <select class="select_Data_Alta" id="TipoDocumentoSiena" v-model="tipoDocumentoSiena">
                    <option value="" selected hidden>Seleccionar...</option>
                    <option value="IDCIN">IDCIN</option>
                    <option value="IFGRA">IFGRA</option>
                    <option value="CROQU">CROQU </option>
                    <option value="FPCCA">FPCCA</option>
                </select>
            </div>
        </div>
        <div class="div_Permite_Asociacion_Firma" id="UbicacionPath">
            <button>&nbsp;+&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Ubicacion</button> Path:
        </div>
        <!-- cuadricula De Documento electronico -->
        <div class="container_cuadricula_Datos_Firma  animate__animated animate__fadeIn" style="display: none;">
            <p>Nombre del Documento</p>
            <p>Descripciòn del Documento</p>
            <p> Asocia SIENA</p>
            <p>Entidad</p>
            <p>Id.Entidad</p>
        </div>

        <!-- tabla localstorage -->
        <div class="container" id="divTablaAltaProcesoMasivoDeFirma" style="margin-top:50px ;">
            <table>
                <tr v-for="(value, key) in localStorageData" :key="key">
                    <td id="headerTabla">{{ key }}</td>
                    <td id="tablavalue">{{ value }}</td>
                </tr>

            </table>
        </div>
        <!-- Botones de accion con ese nuevo proceso -->
        <div class="container_btn_Proceso_Firma" id="Alta_firma_container_btn">
            <button class="Cancelar_Proceso_Firma btn btn-danger" id="btnCancelarFirma">X Cancelar </button>
            <button class="Procesar_Proceso_Firma btn btn-primary" id="btnProcesarFirma" @click="guardarBaseFirma">
                Procesar </button>
            <button class="Guardar_Proceso_Firma btn btn-success" id="btnGuardarFirma" @click="guardarTipo"> Guardar
            </button>
        </div>
    </div>






</template>




<script>
import moment from 'moment';
import axios from 'axios';
import './styles.css';

export default {
    name: 'AltaFirma',
    data() {
        return {
            // proceso ALta
            TipoAlta: "Firma Masiva",
            estadoLote: "Pendiente",
            usuario: "DevTest",

            // class de btn reactivo
            addedClassAsociacionFirma: '',
            addedClassAsociacionUnicoItemContainerFirma: '',
            addedClassSelectContainerEntidad: '',
            addedClassTipoDocumentoSiena: '',
            addedClassAsociaUnicoItem: '',

            // localStorage
            referencia: "",
            firmante: "",
            tipoDocumento: "",
            entidad: "",
            tipoDocumentoSiena: "",
            // personas: []
            // btn localstorage
            buttonPerimteAsociacion: false,
            buttonAsociaUnicoItem: false,

            // localsotagetable
            localStorageData: null,

            //DataTime
            currentDate: moment().format('YYYY-MM-DD')
        }
    },
    methods: {
        // btn reactive
        toggleClassAsociacionFirma() {
            this.addedClassAsociacionFirma = this.addedClassAsociacionFirma === 'active' ? '' : 'active'
            this.addedClassAsociacionUnicoItemContainerFirma = this.addedClassAsociacionUnicoItemContainerFirma === 'active' ? '' : 'active'
            // btn localstorage
            this.buttonPerimteAsociacion = !this.buttonPerimteAsociacion
        },
        toggleClassAsociaUnicoItem() {
            this.addedClassSelectContainerEntidad = this.addedClassSelectContainerEntidad === 'active' ? '' : 'active'
            this.addedClassTipoDocumentoSiena = this.addedClassTipoDocumentoSiena === 'active' ? '' : 'active'
            this.addedClassAsociaUnicoItem = this.addedClassAsociaUnicoItem === 'active' ? '' : 'active'

            // btn localstorage
            this.buttonAsociaUnicoItem = !this.buttonAsociaUnicoItem
        },

        // localstorage
        guardarTipo() {
            if (!this.referencia || !this.firmante || !this.tipoDocumento) {
                alert("Los campos de referencia, firmante y tipo de documento son obligatorios");
                return;
            }
            localStorage.setItem("referencia", this.referencia);
            localStorage.setItem("firmante", this.firmante);
            localStorage.setItem("tipo_documento", this.tipoDocumento);
            if (this.buttonPerimteAsociacion) {
                localStorage.setItem('buttonPerimteAsociacion', this.buttonPerimteAsociacion);
            } else {
                localStorage.removeItem('buttonPerimteAsociacion');
            }
            if (this.buttonAsociaUnicoItem) {
                localStorage.setItem('buttonAsociaUnicoItem', JSON.stringify(this.buttonAsociaUnicoItem));
                localStorage.setItem("entidad", this.entidad);
                localStorage.setItem("tipoDocumentoSiena", this.tipoDocumentoSiena);
            } else {
                localStorage.removeItem('buttonAsociaUnicoItem');
                localStorage.removeItem('tipoDocumentoSiena');
                localStorage.removeItem('entidad');
            }

            // Tira valores dentro de la tabla localStorage  
            this.localStorageData = {};
            for (let i = 0; i < localStorage.length; i++) {
                let key = localStorage.key(i);
                this.localStorageData[key] = localStorage.getItem(key);
            }
        },
        guardarBaseFirma() {
            const altasFirma = {
                Referencia: this.referencia,
                Firmante: this.firmante,
                TipoDocumento: this.tipoDocumento,
                PermiteAsociacion: this.buttonPerimteAsociacion,
                AsociaUnicoItem: this.buttonAsociaUnicoItem,
                Entidad: this.entidad,
                TipoDocumentoSiena: this.tipoDocumentoSiena,
                DataTime: this.currentDate,

            }
            const altaFirmasPadre = {
                referencia: this.referencia,
                firmante: this.firmante,
                tipoProceso: this.TipoAlta,
                Usuario: this.usuario,
                estadoLote: this.estadoLote,
                DataTime: this.currentDate,
            }
            axios.post("https://localhost:5001/api/AltaPadre", altaFirmasPadre).then(response => {
                console.log(response);
            }).catch(error => {
                console.error(error);
            });
            axios.post("https://localhost:5001/api/GDE_Firma", altasFirma).then(response => {
                console.log(response);
            }).catch(error => {
                console.error(error);
            });
        }
    },


}
</script>

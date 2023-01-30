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
                <input type="text" class="grupo_Entrada_Data_Firma" required style="max-width: 500px; height: 40px;"
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
            <button class="Procesar_Proceso_Firma btn btn-primary" id="btnProcesarFirma" @click="guardarBaseFIrma">
                Procesar </button>
            <button class="Guardar_Proceso_Firma btn btn-success" id="btnGuardarFirma" @click="guardarTipo"> Guardar
            </button>
        </div>
    </div>






</template>




<script>
import moment from 'moment';
import axios from 'axios';
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
            Firmante: "",
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

            // const persona = { referencia: this.referencia, firmante: this.firmante };
            // this.personas.push(persona);
            // valores de inputs iniciales
            localStorage.setItem("referencia", this.referencia);
            localStorage.setItem("firmante", this.firmante);
            // tipo documento select
            localStorage.setItem("tipo_documento", this.tipoDocumento);

            // brn guardados 
            if (this.buttonPerimteAsociacion) {
                localStorage.setItem('buttonPerimteAsociacion', this.buttonPerimteAsociacion)

            } else {
                localStorage.removeItem('buttonPerimteAsociacion')

            }
            if (this.buttonAsociaUnicoItem) {
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
        guardarBaseFIrma() {
            const altasFirma = {
                Referencia: this.referencia,
                Firmante: this.firmante,
                TipoDocumento: this.tipoDocumento,
                PermiteAsociacion: this.buttonPerimteAsociacion,
                AsociaUnicoItem: this.buttonAsociaUnicoItem,
                Entidad: this.entidad,
                TipoDocumentoSiena: this.tipoDocumentoSiena,


            }
            const altaFirmasPadre = {
                Referencia: this.referencia,
                Firmante: this.firmante,
                TipoProceso: this.TipoAlta,
                Usuario: this.usuario,
                EstadoLote: this.estadoLote,
            }
            axios.post("https://localhost:5001/api/GDE_Firma", altasFirma).then(response => {
                console.log(response);
            }).catch(error => {
                console.error(error);
            });
            axios.post("https://localhost:5001/api/ExpedientesGDEPadre", altaFirmasPadre).then(response => {
                console.log(response);
            }).catch(error => {
                console.error(error);
            })
        }
    },


}
</script>

<style lang="css" scoped>
/* Proceso de alta de expedientes */
.Alta_Expedientes_Firma_Conteiner {
    display: block;
    width: 98%;
    margin: auto;
    background-color: white;
    border: 1px solid gray;
    margin-top: 10px;
    border-radius: 5px;
    height: auto;
    margin-bottom: 400px;
}


.Encabezado_Alta_Expediente_Firma {
    display: flex;
    justify-content: space-between;
    margin: 0 400px 0 20px;
    color: grey;
}

/* proceso de referencias de datos Nro.Lote Estado Usuario Tipo proceso */
.Referencia_Proceso_Firma_Expedientes {
    display: flex;
    justify-content: space-around;
    color: gray;
}

.Referencia_Proceso_Firma_Expedientes p span {
    color: black;

}

/* inputs y buttons referencias y datos de nuevo expediente */
.container_Inputs_Entrada_Data_Firmante {
    display: flex;
    justify-content: space-around;
    margin: auto;
}

.div_Inputs_Entrada_Data_Firmante {
    max-width: 30%;
    margin: 0 20px 0 50px;
}

.div_Inputs_Entrada_Data_Firmante p {
    font-size: 1.2rem;
    color: gray;

}

.div_Inputs_Entrada_Data_Firmante select {
    width: 100% !important;
    text-align: start;
}

.div_Inputs_Entrada_Data_Firmante input {
    width: 100% !important;
}

.grupo_Entrada_Data_Firma {
    margin-top: -10px;

    text-align: start;
    height: 40px;
    width: 100% !important;

}

.Inputs_btnAsocia_Unico_Item {
    width: 30% !important;
}

.selectDataAlta {
    width: 100% !important;
}

.btn_ProcesoFirma {
    color: gray;
}

/* No requiere asociacion */
.container_FirmaNoAsociacion {
    display: block !important;
}

.div_NoPermiteAsociacionFirma {
    display: flex;
}

.div_NoPermiteAsociacionFirma div {
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
    margin-top: 50px !important;
}

#div_InputTipoDocumentoSIENA.active {
    display: block;

    width: 300px;
    margin: auto;
}

#InputActiveEntidad {
    display: none;

}

#InputActiveEntidad.active {
    display: block;

}

#TipoDocumentoSiena {
    width: 300px;

}

.container_Permite_Asociacion_Firma {
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

.div_Permite_Asociacion_Firma {
    font-size: 1.1rem;
}

.div_Permite_Asociacion_Firma button {
    background-color: #65b2e2;
    border: none;
    padding: 10px 50px 10px 0px;
    color: white;
}

.div_Permite_Asociacion_Firma2 {
    margin-top: -20px;
}

.div_Permite_Asociacion_Firma2 button {
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
    top: 0;
    right: 0;
    left: unset;
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
    transition-duration: 5000s;
}

/* -------------------------Swich UnicoItem-------------------------------------- */
.btn_Unico_Item {
    display: none;
    animation: fadeOut;
    animation-duration: 500ms;


}

.btn_Unico_Item.active {
    display: block;
    animation: fadeIn;
    animation-duration: 500ms;


}

.Swich_Item_Unico {
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

.Swich_Item_Unico::after {
    padding-top: 20px;
    content: "Si";
    display: block;
    width: 100px;
    height: 60px;
    position: absolute;
    background: #f1f1f1;
    top: 0;
    right: 0;
    left: unset;
    border-radius: 3px;
    border: 1px solid rgba(150, 150, 150, 0.442);
}

.Swich_Item_Unico span {
    width: 100px;
    height: 40px;
    margin-top: 20px;
    display: block;
    background: none;
    color: black;
}

.Swich_Item_Unico.active {
    background: rgba(17, 123, 245, 1.0);
    background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
    background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
    background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
    ;

    color: black;
}

.Swich_Item_Unico.active::after {
    right: unset;
    left: 0;
    content: "No";

}

/* -----------------------------------Fin Switch------------------------------------------------------------ */

/* cuadricula De Documento electronico */
.container_cuadricula_Datos_Firma {
    display: flex;
    justify-content: space-between;
    background-color: #39b3ff;
    width: 98%;
    margin: auto;

    margin-top: 40px;
}

.container_cuadricula_Datos_Firma p {
    margin-left: 20px;
    margin-right: 20px;
    padding-top: 10px;

}

/* Botones de accion con ese nuevo proceso */
.container_btn_Proceso_Firma {
    display: flex;
    justify-content: space-between;
    width: 98%;
    margin: auto;
    margin-top: 50px;
    margin-bottom: 30px;
    bottom: 0px;

}

.container_btn_Proceso_Firma.active {
    transform: initial;

}

.Cancelar_Proceso_Firma {
    border-radius: 5px;
    width: 300px;
    height: 40px;
    border: solid 1px rgb(79, 107, 79);
    color: rgb(79, 107, 79);
}

.Procesar_Proceso_Firma {
    background-color: #9291a2;
    width: 300px;
    height: 40px;
    border-radius: 5px;
    border: none;
}

.Guardar_Proceso_Firma {
    background-color: #39b3ff;
    width: 300px;
    height: 40px;
    border-radius: 5px;
    border: none;
}

/* tabla reactiva */
#divTablaAltaProcesoMasivoDeFirma table {
    width: fit-content;
    display: flex;
    margin-bottom: 100px;
    border: solid 1px rgb(113, 112, 112);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}


#divTablaAltaProcesoMasivoDeFirma table tr td {
    display: block;


}

tr #headerTabla {
    background-color: #65b2e2;
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
    .container_Inputs_Entrada_Data_Firmante {
        display: flex;
        justify-content: space-around;
        margin: auto;
        margin-right: 50px;
    }

    .div_Inputs_Entrada_Data_Firmante {
        width: 200px;
        margin: 0 20px 0 50px;
    }

    .div_Inputs_Entrada_Data_Firmante input {
        width: 300px;
    }

    .grupo_Entrada_Data_Firma {
        width: 100%;

    }

}
</style>


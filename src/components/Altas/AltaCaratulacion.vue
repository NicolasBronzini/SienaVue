<template>
     <!-- Este va a ser el apartado de caratulacion -->
     <div class="Alta_Expedientes_Caratulacion_Conteiner" id="Container_total_Caratulacion">
            <!-- encabezado y fecha -->
            <div class="Encabezado_Alta_Expediente_Caratulacion">
                <span id="" style="font-size:1.4rem;">ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS</span>
                <p>fecha {Fecha dia efectuado}</p>
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
                     <input type="text" class="grupo_Entrada_Data_Caratulacion" required style="width: 100%; height: 40px;" id="referencia_alta_proceso_masivo_firma"/>
               </div>
                <!-- Firmante -->
               <div class="div_Inputs_Entrada_Data_Caratulacion form-control">
                     <p> Firmante</p>
                     <div class=" grupo_Entrada_Data_Caratulacion " role="group">
                           <!-- Chequear su existencia en GDE. Selección única -->
                           <input type="text"  style="width: 100%; height: 40px;" id="firmante_alta_proceso_masivo_firma" />
                     </div>
               </div>
                    <!--Button Tipo de Documento  -->
               <div class="div_Inputs_Entrada_Data_Caratulacion form-control" role="group">
                     <p>Tipo de Documento</p>
                     <div class=" grupo_Entrada_Data_Caratulacion" role="group">
                        <select class="selectDataAlta" name="Seleccionar" id="" style="width:100%; height: 40px;">
                           <option>IDCIN</option>
                           <option>IFGRA</option>
                           <option>CROQU </option>
                           <option>FPCCA</option>
                           <option class="SeleccionarOption" selected>Seleccionar</option>
                           </select>
                     </div>
               </div>
          </div>


            <!-- SWITCHCaratulacion -->
            <div class="container_Permite_Asociacion_Caratulacion container_Permite_Asociacion_Caratulacion2">
                <div class="div_Permite_Asociacion_Caratulacion2 " >
                    <p>¿Trata Única?</p>
                    <button class="Swich_Asociacion" id="switchTrataUnicaCaratulacion" @click="toggleClassTrataUnica" v-bind:class="addedClassTrataUnica" ><span >No</span><span >Si</span></button>
                </div>
                <div class="div_Permite_Asociacion_Caratulacion2">
                    <p>¿Asocia Expediente?</p>
                    <button class="Swich_Asociacion" id="switchAsociaExpedienteCaratulacion" @click="toggleClassAsociaExpediente" v-bind:class="addedClassAsociaExpediente" ><span >No</span><span >Si</span></button>
                </div>
                <div class="div_Permite_Asociacion_Caratulacion2">
                    <p>¿Requiere Asociación SIENA?</p>
                    <button class="Swich_Asociacion" id="switchAsociacionSIENACaratulacion" @click="toggleClassAsociaSiena" v-bind:class="addedClassAsociaSiena"><span >No</span><span >Si</span></button>
                </div>
                
            </div>

            <!--div trata y motivo  -->

            <div class="container_Permite_Asociacion_Caratulacion container_Permite_Asociacion_Caratulacion2">
                
                <div class="div_Inputs_Entrada_Data_Caratulacion Inputs_btnAsocia_Unico_Item animate__animated form-control" >
                    <p>Trata</p>
                    <div  class=" grupo_Entrada_Data_Caratulacion">
                        <select class="select_Data_Alta" id="" style="width: 100%; height: 40px;">
                            <option >Seleccionar</option>
                        </select>
                    </div>
               </div>

                <div class="div_Permite_Asociacion_Caratulacion2">
                    <p>¿Motivo Interno y Descripción <br>
                        Adicional del tramite coinciden ?</p>
                    <button class="Swich_Asociacion" id="switchMotivoInternoEECaratulacion" @click="toggleClassMotivoInterno" v-bind:class="addedClassMotivoInterno" ><span >No</span><span >Si</span></button>
                </div>
                
            </div>

            <!-- Apartado cruadricula Caratulacion -->
            <div class="Datos_CaratulacionEE_Container">
                <div class="container_HeaderCuadricula">
                    <div class="_data_Filtro_Caratulacion">DATOS CARATULA EXPEDIENTE ELECTRÓNICO</div>
                    <div class="btn_data_Filtro_Caratulacion"><button>Primero</button><button>Anterior</button><p>Registros {numero}</p><p>Pàgina{numero} de {numero}</p><button>Siguiente</button><button>Último</button></div>
                </div>
                
                <div class="Container_Cuadricula_Motivo_Interno_Caratulacion">
                    <div class="Header_Cuadricula_Motivo_Interno_Caratulacion">Motivo Interno/ Descripcion Adicional del Tramite</div>
                    <div class="Output_Cuadricula_Motivo_Interno_Caratulacion">

                    </div>
                </div>
            </div>
            <!-- Botones de accion con ese nuevo proceso -->
            <div class="container_btn_Proceso_Caratulacion" id="Alta_firma_container_btn">
                <button class="Cancelar_Proceso_Caratulacion btn btn-danger" id="">X Cancelar </button>
                <button class="Procesar_Proceso_Caratulacion btn btn-primary" id=""> Procesar </button>
                <button class="Guardar_Proceso_Caratulacion btn btn-success" id="">  Guardar </button>
            </div>
        </div>
  </template>
  
  
  <script>
  export default {
    name: 'AltaCaratulacion',
            data() {
            return {
               addedClassTrataUnica: '',
               addedClassAsociaExpediente: '',
               addedClassAsociaSiena:'',
              addedClassMotivoInterno:'',

            }
         },
         methods: {
            toggleClassTrataUnica() {
               this.addedClassTrataUnica = this.addedClassTrataUnica === 'active' ? '' : 'active'
            },
            toggleClassAsociaExpediente(){
               this.addedClassAsociaExpediente = this.addedClassAsociaExpediente === 'active' ? '' : 'active'
            },
            toggleClassAsociaSiena(){
               this.addedClassAsociaSiena = this.addedClassAsociaSiena === 'active' ? '' : 'active'
            },
            toggleClassMotivoInterno(){
               this.addedClassMotivoInterno = this.addedClassMotivoInterno === 'active' ? '' : 'active'
             }
            
         }
      }
  

  </script>
  
  <style lang="css" scoped>
  /* Proceso de alta de expedientes */
.Alta_Expedientes_Caratulacion_Conteiner{
   display: block;
   width: 98%;
   margin: auto;
   background-color: white;
   border: 1px solid gray;
   margin-top: 30px;
   border-radius: 5px;
}


.Encabezado_Alta_Expediente_Caratulacion{
   display: flex;
   justify-content: space-between;
   margin: 0 400px 0 20px;
   color: grey;
}
/* proceso de referencias de datos Nro.Lote Estado Usuario Tipo proceso */
.Referencia_Proceso_Caratulacion_Expedientes{
   display: flex;
   justify-content: space-around;
   color: gray;
}
.Referencia_Proceso_Caratulacion_Expedientes p span{
   color: black;
   
}
/* inputs y buttons referencias y datos de nuevo expediente */
.container_Inputs_Entrada_Data_Caratulacion{
   display: flex !important;

   margin: auto;  
}
.div_Inputs_Entrada_Data_Caratulacion{
   
   width: 30%;
  margin: 0 20px 0 30px;
}
.div_Inputs_Entrada_Data_Caratulacion p{
   font-size: 1.2rem;
   color: gray;
  
}
.div_Inputs_Entrada_Data_Caratulacion button{
   width: 500px;
   text-align: start;   
}
.div_Inputs_Entrada_Data_Caratulacion input{
  width: 500px;
}
.grupo_Entrada_Data_Caratulacion{
   margin-top: -10px;
   text-align: start;
  height: 40px;
 
}
.selectDataAlta{
   width: 500px;
}
.btn_ProcesoCaratulacion{
   color: gray;
}
/* No requiere asociacion */
.container_CaratulacionNoAsociacion{
   display: block !important;
}
.div_NoPermiteAsociacionCaratulacion{
   display: flex;
}

.div_NoPermiteAsociacionCaratulacion div {
   margin-bottom: 70px;
}
#div_UnicoItembtn{
   margin-left: 150px;
}
/* Permite Asociacion */
/* Input Entidad al Asociar Unico Item */

#div_InputTipoDocumentoSIENA{
   margin: auto;
   display: none;
}
.reactive#div_InputTipoDocumentoSIENA.active{
   display: block;
   margin-top: 50px;
}
#InputActiveEntidad{
   display: none;
}
.reactive#InputActiveEntidad.active{
   display: block;
}
#TipoDocumentoSiena{
   width: 300px;
   
}

.container_Permite_Asociacion_Caratulacion{
   display: flex;
   justify-content: space-between;
   margin: auto;
   margin: 50px 100px 0px 200px;
}
.reactive#UbicacionPath2{
   display: block;
}
.reactive#UbicacionPath2.active{
   display: none;
}
#UbicacionPath{
   margin-left: 100px;
   margin-top: 40px;
   display: none;
}
.reactive#UbicacionPath.active{
   display: block;
}

.div_Permite_Asociacion_Caratulacion {
   font-size: 1.1rem;
}
.div_Permite_Asociacion_Caratulacion button{
   background-color: #65b2e2;
   border: none;
   padding: 10px 50px 10px 0px;
   color: white;
}
.div_Permite_Asociacion_Caratulacion2{
   margin-top: -20px;
}
.div_Permite_Asociacion_Caratulacion2 button{
   margin: -5px 0px;
   border: none;
}
/*---------------------------------- Switch------------------------------- */
.Swich_Asociacion{
   background: rgba(17, 123, 245, 1.0);
   background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));;
   border: none;
   border-radius: 5px;
   position: relative;
   cursor: pointer;
   display: flex;
   outline: none;
  
}

.Swich_Asociacion::after{
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
.Swich_Asociacion span{
   width: 100px;
   height: 40px;
   margin-top:20px ;
   display: block;
   background: none;
   color: black;
}
.Swich_Asociacion.active{
   background: rgba(17, 123, 245, 1.0);
   background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
   background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));;
   color: black;
}
.Swich_Asociacion.active::after{
   right: unset;
   left: 0;
   content: "No";
}







/* -------------------------------------------------------------- */
/* TrataUnicaCaratulacion */
#switchTrataUnicaCaratulacion::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchTrataUnicaCaratulacion.active::after{
   right: unset;
   left: 0;
   content: "No";
}




/* Asocia Expediente Caratulacion */
#switchAsociaExpedienteCaratulacion::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchAsociaExpedienteCaratulacion.active::after{
   right: unset;
   left: 0;
   content: "No";
}




/* -------------------------------------------------------------- */
/* Asocia SIENA  Caratulacion */
#switchAsociacionSIENACaratulacion::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchAsociacionSIENACaratulacion.active::after{
   right: unset;
   left: 0;
   content: "No";
}



/* -------------------------------------------------------------- */
/* Asocia Unico Item  Caratulacion */
#switchAsociaUnicoEEPase::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchAsociaUnicoEEPase.active::after{
   right: unset;
   left: 0;
   content: "No";
}

/* -------------------------------------------------------------- */
/* Asocia Unico Item  Caratulacion */
#switchAsociaUnicoEEPase2::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchAsociaUnicoEEPase2.active::after{
   right: unset;
   left: 0;
   content: "No";
}



/* Asocia Motivo Interno  Caratulacion */
#switchMotivoInternoEECaratulacion::after{
   top: 0;
  right: 0;
  left: unset;
}
#switchMotivoInternoEECaratulacion.active::after{
   right: unset;
   left: 0;
   content: "No";
}




/* Fin SWITCH */

/* ----------------------------------------------------------------------------- */


/* cuadricula De Documento electronico */
.container_cuadricula_Datos_Caratulacion{
   display: flex;
   justify-content: space-between;
   background-color: #39b3ff;
   width: 98%;
   margin: auto;
   
   margin-top: 40px;
}
.container_cuadricula_Datos_Caratulacion p{
   margin-left: 20px;
   margin-right: 20px;
   padding-top: 10px;
   
}
/* Botones de accion con ese nuevo proceso */
.container_btn_Proceso_Caratulacion{
   display: flex;
   justify-content: space-between;
   width: 98%;
   margin: auto;
   margin-top: 50px;
   margin-bottom: 30px;
}
.Cancelar_Proceso_Caratulacion{
   border-radius: 5px;
   width: 300px;
   height: 40px;
   border: solid 1px rgb(79, 107, 79);
   color: rgb(79, 107, 79);
}
.Procesar_Proceso_Caratulacion{
   background-color: #9291a2;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}
.Guardar_Proceso_Caratulacion{
   background-color: #39b3ff;
   width: 300px;
   height: 40px;
   border-radius: 5px;
   border: none;
}
/* media querys */
@media screen and (max-width: 1400px){
   .container_Inputs_Entrada_Data_Caratulacion{
       display: flex;
       justify-content: space-around;
       margin: auto;
       margin-right: 50px;
   }
   .div_Inputs_Entrada_Data_Caratulacion{
       width: 200px;
      margin: 0 20px 0 50px;
   }
   .div_Inputs_Entrada_Data_Caratulacion input{
       width: 300px;
   }
  
   
}












/* Cuadricula ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS*/
.Datos_CaratulacionEE_Container{
    width: 98%;
   margin: auto;
   background-color: rgb(242, 240, 240);
   margin-top: 15px;
   padding: 0px 10px;
   padding-bottom: 10px;
   border: #7b7b7b solid 1px;
   border-radius: 10px;
}
.container_Header_Cuadricula{
    display: flex;
    justify-content: space-between;
   
 }
 ._data_Filtro_Caratulacion{
    color: gray;
    margin-top: 10px;
 }
 .btn_data_Filtro_Caratulacion{
    display: flex;
    margin: 10px;
 }
 .btn_data_Filtro_Caratulacion button{
    border: none;
    color: #37bbed;
    font-size: 1.3rem;
    margin: 20 20px;
 }
 .btn_data_Filtro_Caratulacion p{
    margin: 0 5px;
    color: gray;
 }

 /* cuadricula interna motivo Interno */
 .Container_Cuadricula_Motivo_Interno_Caratulacion{
    display: block;
    width: 100%;
    margin-top: 20px;
    border: #6a6969 1px solid;
    text-align: center;
 }
 .Header_Cuadricula_Motivo_Interno_Caratulacion{
    background-color: #39b3ff;
   
    height: 40px;
    font-size: large;
    text-decoration: double;
    color: white;
 }
 .Output_Cuadricula_Motivo_Interno_Caratulacion{
    height: 250px;
 }
  </style>
  
  
<template>
  <!-- Este apartado es el de Vincular -->
  <div class="Alta_Expedientes_Vincular_Conteiner" id="Container_total_Vinculacion">
            <!-- encabezado y fecha -->
            <div class="Encabezado_Alta_Expediente_Vincular">
                <span id="" style="font-size:1.4rem;">VINCULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS</span>
                <p>fecha {Fecha dia efectuado}</p>
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
                    <input type="text" class="grupo_Entrada_Data_Vincular" required style="width: 100%; height: 40px;"/>
                </div>
                        <!-- Firmante -->
                <div class="div_Inputs_Entrada_Data_Vincular Inputs_btnAsocia_Unico_Item  form-control">
                    <p> Firmante</p>
                    <div class=" grupo_Entrada_Data_Vincular" role="group">
                        <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;">
                            <!-- Chequear su existencia en GDE. Selección única -->
                            <option class="Seleccionar_Option" selected>Seleccionar</option>
                            <option>nombre de firmante</option>
                          </select>
                    </div>
                </div>
                            <!--Button Tipo de Documento  -->
                <div class="div_Inputs_Entrada_Data_Vincular Inputs_btnAsocia_Unico_Item  form-control">
                    <p>Tipo de Documento</p>
                    <div class=" grupo_Entrada_Data_Vincular" role="group">
                        <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;">
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
                    <button class="Swich_Asociacion" id="SwitchAsociaUnicoEEPrincipalVincular" ><span >No</span><span >Si</span></button>
                </div>
                <div class="div_Permite_Asociacion_Vincular2">
                    <p>¿Requiere Asociación SIENA?</p>
                    <button class="Swich_Asociacion" id="SwitchAsociaSienaVincular" ><span >No</span><span >Si</span></button>
                </div>
                <div class="div_Permite_Asociacion_Vincular2">
                    <p>¿Asocia a un único Item?</p>
                    <button class="Swich_Asociacion" id="SwitchAsociaUnicoItemVincular" ><span >No</span><span >Si</span></button>
                </div>
                
            </div>

            <!-- Expediente electronico Firmante  -->
            
            <div class="container_Inputs_Entrada_Data_Vincular" id="ContainerVincularInputsEE">
                        <!-- Input Referencia -->
                <div class="div_Inputs_Entrada_Data_Vincular   form-control" id="ExpedienteElectronicoVincular">
                   <p>Expediente Electronico</p>
                    <input type="text" class="grupo_Entrada_Data_Vincular" required placeholder="Ex-Año-XXXXXXXX-APN-Reparticion" style="width: 100%; height: 40px;"/>
                </div>
                        <!-- Firmante -->
                <div class="div_Inputs_Entrada_Data_Vincular form-control" id="EntidadVincularEE">
                    <p> Entidad</p>
                    <div class=" grupo_Entrada_Data_Vincular" role="group">
                        <select class="select_Data_Alta" name="Seleccionar" style="width: 100%; height: 40px;">
                            <!-- Chequear su existencia en GDE. Selección única -->
                            <option class="Seleccionar_Option" selected disabled>Seleccionar</option>
                            <option>nombre de firmante</option>
                        </select>
                    </div>
                </div>
            </div>

             <!-- Apartado cruadricula Vinculacion -->
            <div class="DatosVincularContainer">
                <div class="_dataFiltroVincular"><span>+</span><span>Importar EE generado masivamente</span></div>
                <div class="ContainerCuadriculaMotivoInternoVincular">
                    <div class="HeaderCuadriculaMotivoInternoVincular"><h4>EXPEDIENTE ELECTRÓNICO SECUNDARIO</h4><h4>IDENTIDAD</h4> </div>
                    <div class="OutputCuadriculaMotivoInternoVincular">

                    </div>
                </div>
            </div>
            
            <!-- Botones de accion con ese nuevo proceso -->
            <div class="container_btn_Proceso_Vincular" id="">
                <button class="Cancelar_Proceso_Vincular btn btn-danger" id="">X Cancelar </button>
                <button class="Procesar_Proceso_Vincular btn btn-primary" id=""> Procesar </button>
                <button class="Guardar_Proceso_Vincular btn btn-success" id="">  Guardar </button>
            </div>
        </div>
</template>




 <script>
 export default {
   name: 'AltaVinculacion',
 
 }

 </script>
 
 <style lang="css" scoped>
 
/* Proceso de alta de expedientes */
.Alta_Expedientes_Vincular_Conteiner{
    display: block;
    width: 98%;
    margin: auto;
    background-color: white;
    border: 1px solid gray;
    margin-top: 10px;
    border-radius: 5px;
 }
 .ContainerVincularActive{
   display: block;
 }
 
 .Encabezado_Alta_Expediente_Vincular{
    display: flex;
    justify-content: space-between;
    margin: 0 400px 0 20px;
    color: grey;
 }
 /* proceso de referencias de datos Nro.Lote Estado Usuario Tipo proceso */
 .Referencia_Proceso_Vincular_Expedientes{
    display: flex;
    justify-content: space-around;
    color: gray;
 }
 .Referencia_Proceso_Vincular_Expedientes p span{
    color: black;
    
 }
 /* inputs y buttons referencias y datos de nuevo expediente */
 .container_Inputs_Entrada_Data_Vincular{
    display: flex;
    justify-content: space-around;
    margin: auto;  
 }
 .div_Inputs_Entrada_Data_Vincular{
    width: 32.6%;
   margin: 0 20px 0 50px;
 }
 .div_Inputs_Entrada_Data_Vincular p{
    font-size: 1.2rem;
    color: gray;
   
 }
 .div_Inputs_Entrada_Data_Vincular button{
    width: 500px;
    text-align: start;   
 }
 .div_Inputs_Entrada_Data_Vincular input{
   width: 500px;
 }
 .grupo_Entrada_Data_Vincular{
    margin-top: -10px;
    text-align: start;
   height: 40px;
  
 }
 .selectDataAlta{
    width: 500px;
 }
 .btn_ProcesoVincular{
    color: gray;
 }
 /* No requiere asociacion */
 .container_VincularNoAsociacion{
    display: block !important;
 }
 .div_NoPermiteAsociacionVincular{
    display: flex;
 }
 
 .div_NoPermiteAsociacionVincular div {
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
 
 .container_Permite_Asociacion_Vincular{
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
 
 .div_Permite_Asociacion_Vincular{
    font-size: 1.1rem;
 }
 .div_Permite_Asociacion_Vincular button{
    background-color: #65b2e2;
    border: none;
    padding: 10px 50px 10px 0px;
    color: white;
 }
 .div_Permite_Asociacion_Vincular2{
    margin-top: -20px;
 }
 .div_Permite_Asociacion_Vincular2 button{
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
/* TrataUnicaVincular EE Principal */
#SwitchAsociaUnicoEEPrincipalVincular::after{
   top: 0;
  right: 0;
  left: unset;
}
#SwitchAsociaUnicoEEPrincipalVincular.active::after{
   right: unset;
   left: 0;
   content: "No";
}




/* Asocia Expediente Vincular Asocia Siena */
#SwitchAsociaSienaVincular::after{
   top: 0;
  right: 0;
  left: unset;
}
#SwitchAsociaSienaVincular.active::after{
   right: unset;
   left: 0;
   content: "No";
}




/* -------------------------------------------------------------- */
/* Asocia UnicoItem Principal */
#SwitchAsociaUnicoEEPrincipalVincular::after{
   top: 0;
  right: 0;
  left: unset;
}
#SwitchAsociaUnicoEEPrincipalVincular.active::after{
   right: unset;
   left: 0;
   content: "No";
}







/* Fin SWITCH */

/* ----------------------------------------------------------------------------- */

 /* cuadricula De Documento electronico */
 .container_cuadricula_Datos_Vincular{
    display: flex;
    justify-content: space-between;
    background-color: #39b3ff;
    width: 98%;
    margin: auto;
    
    margin-top: 40px;
 }
 .container_cuadricula_Datos_Vincular p{
    margin-left: 20px;
    margin-right: 20px;
    padding-top: 10px;
    
 }
 
 
 
 
 
 
 
 /* ----------------------------------------------------------------------------------------------- */
 /* Cuadricula ALTA CARATULACIÓN MASIVA DE EXPEDIENTES ELECTRÓNICOS*/
 .DatosVincularEEContainer{
    width: 98%;
   margin: auto;
   background-color: rgb(242, 240, 240);
   margin-top: 15px;
   padding: 0px 10px;
   padding-bottom: 10px;
   border: #7b7b7b solid 1px;
   border-radius: 10px;
 }
 .container_HeaderVincular{
    display: flex;
    justify-content: space-between;
    
 }
 ._dataFiltroVincular{
    background-color: #7ab7c7;
    color: white;
    margin-top: 50px;
    margin-bottom: 10px;
    padding-top: 5px;
    display: flex;
    justify-content: space-around;
    width: 350px;
    height: 40px;
    margin-left: 20px;
 }
 
 
 .btn_dataFiltroVincular{
    display: flex;
    margin: 10px;
   
 }
 .btn_dataFiltroVincular button{
    border: none;
    color: #37bbed;
    font-size: 1.3rem;
    margin: 20 20px;
 }
 .btn_dataFiltroVincular p{
    margin: 0 5px;
    color: gray;
 }


 #ContainerVincularInputsEE{
   width: 100%;
   margin-top: 50px;
 }
 #EntidadVincularEE{
   width: 30% ;
 }
 #ExpedienteElectronicoVincular{
   width: 30%;
 }
 
 
 
 .ContainerCuadriculaMotivoInternoVincular{
    display: block;
    width: 98%;
    margin-top: 15px;
    border: #6a6969 1px solid;
    border-radius: 3px;
    text-align: center;
    margin: auto;
  
 }
 .HeaderCuadriculaMotivoInternoVincular{
    background-color: #39b3ff;
    height: 40px;
    color: white;
    display: flex;
    justify-content: space-around;
 }
 
 .OutputCuadriculaMotivoInternoVincular{
    height: 250px;
 }
 
 
 
 
 
 /* -------------------------------------------------------------------- */
 
 
 /* Botones de accion con ese nuevo proceso */
 .container_btn_Proceso_Vincular{
    display: flex;
    justify-content: space-between;
    width: 98%;
    margin: auto;
    margin-top: 50px;
    margin-bottom: 30px;
 }
 .Cancelar_Proceso_Vincular{
    border-radius: 5px;
    width: 300px;
    height: 40px;
    border: solid 1px rgb(79, 107, 79);
    color: rgb(79, 107, 79);
 }
 .Procesar_Proceso_Vincular{
    background-color: #9291a2;
    width: 300px;
    height: 40px;
    border-radius: 5px;
    border: none;
 }
 .Guardar_Proceso_Vincular{
    background-color: #39b3ff;
    width: 300px;
    height: 40px;
    border-radius: 5px;
    border: none;
 }
 /* media querys */
 @media screen and (max-width: 1400px){
    .container_Inputs_Entrada_Data_Vincular{
        display: flex;
        justify-content: space-around;
        margin: auto;
        margin-right: 50px;
    }
    .div_Inputs_Entrada_Data_Vincular{
        width: 200px;
       margin: 0 20px 0 50px;
    }
    .div_Inputs_Entrada_Data_Vincular input{
        width: 300px;
    }
    .grupo_Entrada_Data_Vincular{
        width: 100% !important;
    }
    
 }
 
 </style>
 
 
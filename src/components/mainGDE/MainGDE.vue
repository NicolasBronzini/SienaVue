            <script>
            
            import AltaCaratulacion from '../Altas/AltaCaratulacion.vue'
             import AltaFirma from '../Altas/AltaFirma.vue'
             import AltaPase from '../Altas/AltaPase.vue'
             import AltaVinculacion from '../Altas/AltaVinculacion.vue'
            
            
            export default {
              name: 'MainGDE',
              components: {
                AltaCaratulacion,
                  AltaFirma,
                 AltaPase,
               AltaVinculacion,   
                  } ,
                  data() {
                    return {
                    selectedOption: '',
                    options: [
                        { text: 'Caratulacion', value: 'AltaCaratulacion' },
                        { text: 'Firma', value: 'AltaFirma' },
                        { text: 'Pase', value: 'AltaPase' },
                        { text: 'Vinculacion', value: 'AltaVinculacion' },
                    ]
                    }
                },
                methods: {
                    showComponent() {
                    
                    }
                } 
                  
            }
            
             
            </script>

<template>
    <div>
        <div class="ltProceso">
            <div class="apartado-btn_ProcesosMasivos">
                <!-- procesos masivos button despegable -->
                <button class="btn_ProcesosMasivos"><a href="/index.html" id="linkHome">Procesos masivos ></a> </button>
            </div>
        </div>
        <div>
            <!-- filtros -->
            <div class="container_Filtros">
                <div class="filtros_Proceso"> 
                    <div class="div_InputsFiltro">
                        <input type="nu" placeholder="Número de Lote " id="Input_filtro-1" />
                        <input type="text" placeholder="Referencia" id="Input_filtro-2"/>
                    </div>
                    <div class="btn_Filtros">
                        <button id="btn_filtrado" class="btn btn-secondary">Filtrar</button>
                        <button id="btn_Alta" class="btn btn-success" >Alta</button>
                    </div>
                </div>
                <hr style="width: 95%; margin:auto;">
                <!-- seteo de filtros -->
                <div class="container_SeteoFiltros">
                    <div class="Filtro_masivo">
                        <!-- Tipo de proceso -->
                        <div class="btn-group" role="group" style="margin:0px 20px ;" >
                            <label for="">Tipo Proceso: ></label>
                            <select name="cbxProceso" id="cbxProceso"  >
                               
                                <option v-for="option in options" v-bind:key="option.value">
                                    {{ option.text }}
                                </option>
                            </select>
                          </div>
                          <!-- Estado del proceso -->
                          <div class="btn-group" role="group" style="margin:0px 20px ;">
                            <label for="">Estado: ></label>
                            <select name="Seleccionar">
                                <option selected>Seleccionar...</option>
                                <option>Pendiente</option>
                                <option>Finalizado</option>
                                <option>Interrumpido</option>
                                <option>Procesar</option>
                            </select>
                            
                          </div>
                          <!-- inputs Aplicar Filtros -->
                       <input type="text" placeholder="Firmante" required maxlength="100"/>
                       <input type="date" placeholder="Fecha Inicial" required/>
                       <input type="date" placeholder="Fecha Final" required/>
                    </div>
                    <div    class="container_btn_Filtro" >
                        <button id="btn_filtroCancelar" class="btn btn-light">X cancelar</button>
                        <button id="btn_filtroAplicar" class="btn btn-primary"><svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                            <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                          </svg>Aplicar</button>
                    </div>
                </div>
            </div>
            
              <!-- outputData -->
              <div class="OutDataContainer">
                <div class="container_dataFiltro">
                    <div class="_dataFiltro">filtros activos {numero}elementos</div>
                    <div class="btn_dataFiltro"><button>Primero</button><button>Anterior</button><p>Registros {numero}</p><p>Pàgina{numero} de {numero}</p><button>Siguiente</button><button>Último</button></div>
                </div>
                <!-- tabla de datos -->
                <table class="tftable" border="1">
                    <tr><th>Numero</th><th>Referencia del Lote</th><th>Tipo de Proceso</th><th>Estado de Lote</th><th>Usuario</th> <th>Firmante</th> <th>Accion</th></tr>
                    <tr class="tr_impar"><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round">  <path stroke="none" d="M0 0h24v24H0z" fill="none"></path>  <path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path> <path d="M16 7h4"></path> <path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                    <tr><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"> <path stroke="none" d="M0 0h24v24H0z" fill="none"></path> <path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path> <path d="M16 7h4"></path> <path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                    <tr class="tr_impar"><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"> <path stroke="none" d="M0 0h24v24H0z" fill="none"></path> <path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path><path d="M16 7h4"></path> <path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                    <tr><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path><path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path><path d="M16 7h4"></path><path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                    <tr class="tr_impar"><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path><path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path><path d="M16 7h4"></path><path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                    <tr><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td><output></output></td><td class="btn_accion"><button class="btn_ver">ver</button><button class="btn_editar"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M7.127 22.562l-7.127 1.438 1.438-7.128 5.689 5.69zm1.414-1.414l11.228-11.225-5.69-5.692-11.227 11.227 5.689 5.69zm9.768-21.148l-2.816 2.817 5.691 5.691 2.816-2.819-5.691-5.689z"/></svg></button><button class="btn_Firma"><svg xmlns="http://www.w3.org/2000/svg" class="icon icon-tabler icon-tabler-writing" width="24" height="24" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" fill="none" stroke-linecap="round" stroke-linejoin="round"><path stroke="none" d="M0 0h24v24H0z" fill="none"></path> <path d="M20 17v-12c0 -1.121 -.879 -2 -2 -2s-2 .879 -2 2v12l2 2l2 -2z"></path> <path d="M16 7h4"></path> <path d="M18 19h-13a2 2 0 1 1 0 -4h4a2 2 0 1 0 0 -4h-3"></path></svg></button></td></tr>
                </table>
    
            </div>
        </div>

        <div>
            <AltaCaratulacion  v-if="selectedOption === 'AltaCaratulacion'" is="Caratulacion"></AltaCaratulacion>
            <AltaFirma  v-if="selectedOption === 'AltaFirma'" is="Firma"></AltaFirma>
           <AltaPase  v-if="selectedOption === 'AltaPase'" is="Pase"></AltaPase>
            <AltaVinculacion  v-if="selectedOption === 'AltaVinculacion'" is="Vinculacion"></AltaVinculacion> 
        </div>
    </div>
</template>


<style lang="css" scoped>

button{
    border: 1px solid;
}
.container_procesosFirmaMasiva {
    
    background-color: rgb(181, 178, 178);
    height: 100%;
    width: 100%;
    margin: auto;
    overflow: hidden;

}
.ltProceso{
    margin-bottom: 10px;
    margin-top: 10px;
}
.title {
    text-align: center;
    margin: 50px;
}

.apartado-btn_ProcesosMasivos{
    width: 98%;
    background-color: rgb(242, 240, 240);
    margin: auto;
    border-radius: 5px;
}
.btn_ProcesosMasivos{
display: flex;
border: none;
height: 50px;
padding-top: 15px;
margin-left: 10px;

}
#linkHome{
   text-decoration: none;
   color: black;
}
/* filtros   container */
.container_Filtros{
margin: auto;
width: 98%;
background-color: rgb(242, 240, 240);
border-radius: 5px;
}
.filtros_Proceso{
display: flex;
justify-content: space-between;
margin-top: 10px;
padding: 10px;
}
/* seteo de filtros */
.container_SeteoFiltros{
display: block;
margin-top: 30px;
}
.Filtro_masivo{
margin-left: 50px;
margin-bottom: 20px;
}
.Filtro_masivo select{
text-align: left;
margin-left: 5px;
width: 150px;
height: 28px;
margin-top: -5px;
}



/* botones filtros */

.div_InputsFiltro{
margin-left: 30px;
}
.btn_Filtros{
margin-right: 70PX;
}
#btn_filtrado{
    color: white;
   
    border: none;
    width: 50px;
    padding: 5px ;
    margin-right: 60px;
 }
 #btn_Alta{
    color: white;
    
    border: none;
   padding: 5px;
    width: 70px;
    
 }
 #Input_filtro-1{
    height: 25px;
 }
 #Input_filtro-2{
    height: 25px;
 }
 /* segundo apartado filtro */
 .container_btn_Filtro{
    display: flex;
    justify-content: end;
    margin-right: 20px;
 }
 .container_btn_Filtro button{
    margin-left: 10px;
    margin-bottom: 20px;
 }
 #btn_filtroAplicar{
    border: none;
    padding: 3px;
 }
 
 #btn_filtroCancelar{
    padding: 3px;
 }
 /* encabezado filtro tabla */
 .container_dataFiltro{
    display: flex;
    justify-content: space-between;
    margin-right: 10px;
    margin-left: 10px;
 }
 ._dataFiltro{
    color: gray;
 }
 .btn_dataFiltro{
    display: flex;
    margin: 10px;
 }
 .btn_dataFiltro button{
    border: none;
    color: #37bbed;
    font-size: 1.3rem;
    margin: 0 20px;
 }
 .btn_dataFiltro p{
    margin: 0 5px;
    color: gray;
 }
 /* Output Data tabla */
 .OutDataContainer{
     width: 98%;
    margin: auto;
    background-color: rgb(242, 240, 240);
    margin-top: 15px;
    padding-top: 20px;
    padding-bottom: 10px;
    border: #7b7b7b solid 1px;
    border-radius: 10px;
 }
 .OutDataContainer.SacarApartadoOutputData{
    display: none;
 }
 .tftable {font-size:12px;color:#333333;width:96%;border-width: 1px;border-color: #7b7b7b;border-collapse: collapse; margin: auto; margin-top: 10px; margin-bottom: 10px;}
.tftable th {font-size:12px;background-color:#0072bb;border-width: 1px;padding: 8px;border-style: solid;border-color: #729ea5;text-align:left;}
.tftable tr {background-color:#fdfdfd; height: 50px;}
.tftable td {font-size:12px;padding: 8px; height:30px;}
.tr_impar{background-color: #37bced3c !important;}
.tftable tr:hover {background-color:#ffffff;}


/* btn Accion form */
.btn_accion{
    display: flex;
    width: 70px;  
    margin: auto;
    margin-left: 20px;
    justify-content: space-between;
    
}
.btn_accion button{
   height: 35px;
    max-width: 50px;
    margin-left: 5px;
}
.btn_ver{
    background-color:#0072bb;
    border-radius: 5px;
    border: none;
    padding: 10px;
    font-size: large;
}
.btn_editar{
    margin-bottom: 5px;
    padding: 10px;
    border-radius: 25%;
    border: none; 
    background: rgba(17, 123, 245, 1.0);
    background: -webkit-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
    background: -moz-linear-gradient(bottom, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));
    background: linear-gradient(to top, rgba(17, 123, 245, 1.0), rgba(100, 159, 205, 1.0));;
}
.btn_Firma{
    border-radius: 45%;
    border: none;
    background-color: #204aa3;
    padding: 10px;
}
/* Mediaquery Form */
@media screen and (max-width: 1400px) {
   .btn_accion{
      width: 70px;
     
   }
   .btn_accion button{
      height: 35px;
      width: 35px;
      margin-left: 3px !important;
      margin: auto;

   }
   .btn_accion svg{
      width: 20px;
   }
  
}
@media screen and (max-width: 1000px){
   .btn_accion{
      width: 80px !important;
     margin-right: 10px;
   }
}
</style>


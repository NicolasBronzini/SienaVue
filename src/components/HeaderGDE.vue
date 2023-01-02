<template>
  <div class="header">
         <div class="navbar-header"> <a class="navbar-brand"
          href="https://www.argentina.gob.ar/bienesdelestado/tramitesaabe" id="navbar-brand"
          aria-label="Argentina.gob.ar Presidencia de la Nación" target="_blank">
                 <img src="../assets/logo_argentina-blanco.svg" alt="Argentina.gob.ar" height="50" width="254"> </a> <a
                 class="btn btn-mi-argentina btn-login visible-xs" href="https://mi.argentina.gob.ar"
                 aria-label="Ingresar a Mi Argentina"></a> <a
                 onclick="jQuery('.navbar.navbar-top').addClass('state-search');"
                 class="btn btn-mi-argentina btn-login visible-xs" href="#" aria-labelledby="edit-keys" ></a>
         </div>
     </div>
</template>

                 <script>
                 export default {
                   name: 'HeaderGDE',
                   props: {
                     msg: String
                   }
                 }
                 </script>


<style lang="css" scoped>

.header {
 height: 60px;
 width: 100%;
 background-color: #37bbed;
 display: flex;
 
}
.header img{
  margin-left: 20px;
}
</style>


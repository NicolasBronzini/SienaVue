<template>
    <div>
        <div class="ltProceso">
            <div class="apartado-btn_ProcesosMasivos">
                <!-- procesos masivos button despegable -->
                <button class="btn_ProcesosMasivos"><a id="linkHome">Procesos masivos ></a> </button>
            </div>
        </div>
        <div>
            <!-- filtros -->
            <div class="container_Filtros">
                <div class="filtros_Proceso">
                    <div class="div_InputsFiltro">
                        <input type="nu" placeholder="Número de Lote " id="Input_filtro-1" />
                        <input type="text" placeholder="Referencia" id="Input_filtro-2" />
                    </div>
                    <div class="btn_Filtros">
                        <button id="btn_filtrado" class="btn btn-secondary">Filtrar</button>
                        <!-- ACAAAA -->
                        <button id="btn_Alta" class="btn btn-success" @click="showSelectedProcess">Alta</button>
                    </div>
                </div>
                <hr style="width: 95%; margin:auto;">
                <!-- seteo de filtros -->
                <div class="container_SeteoFiltros">
                    <div class="Filtro_masivo">
                        <!-- Tipo de proceso -->
                        <div class="btn-group" role="group" style="margin:0px 20px ;">
                            <label for="">Tipo Proceso: ></label>
                            <select name="cbxProceso" id="cbxProceso" v-model="selectedOption">
                                <option value="">Seleccionar...</option>
                                <option value="Caratulacion">Caratulacion EE</option>
                                <option value="Firma">Firma</option>
                                <option value="Pase">Pase EE</option>
                                <option value="Vinculacion">Vinculacion EE</option>
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
                        <input type="text" placeholder="Firmante" required maxlength="100" />
                        <input type="date" placeholder="Fecha Inicial" required />
                        <input type="date" placeholder="Fecha Final" required />
                    </div>
                    <div class="container_btn_Filtro">
                        <button id="btn_filtroCancelar" class="btn btn-light">X cancelar</button>
                        <button id="btn_filtroAplicar" class="btn btn-primary"><svg xmlns="http://www.w3.org/2000/svg"
                                width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                <path
                                    d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z" />
                            </svg>Aplicar</button>
                    </div>
                </div>
            </div>

            <!-- outputData -->
            <div class="OutDataContainer">
                <div class="container_dataFiltro">
                    <div class="_dataFiltro">filtros activos {numero}elementos</div>
                    <div class="btn_dataFiltro"><button @click="goToFirstPage">Primero</button><button
                            @click="changePage(-1)">Anterior</button>
                        <p style="margin-right: 20px;">Registros {{ datos.length }}</p>
                        <span>Página {{ currentPage }} de {{ totalPages }}</span><button
                            @click="changePage(1)">Siguiente</button><button @click="goToLastPage">Último</button>
                    </div>
                </div>
                <!-- tabla de datos -->
                <table class="tftable">
                    <thead>
                        <tr>
                            <th>Numero</th>
                            <th>Referencia del Lote</th>
                            <th>Tipo de Proceso</th>
                            <th>Estado de Lote</th>
                            <th>Usuario</th>
                            <th>Firmante</th>
                            <th>Accion</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="item in paginatedData" :key="item.id" class="tr_impar">
                            <td>{{ item.idAltaPadre }}</td>
                            <td>{{ item.referencia }}</td>
                            <td>{{ item.tipoProceso }}</td>
                            <td>{{ item.estadoLote }}</td>
                            <td>{{ item.usuario }}</td>
                            <td>{{ item.firmante }}</td>
                            <td></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
        <div>
            <AltaCaratulacion v-if="processToShow === 'Caratulacion'"></AltaCaratulacion>
            <AltaFirma v-if="processToShow === 'Firma'"></AltaFirma>
            <AltaPase v-if="processToShow === 'Pase'"></AltaPase>
            <AltaVinculacion v-if="processToShow === 'Vinculacion'"></AltaVinculacion>
        </div>
    </div>
</template>

<script>
import AltaCaratulacion from '../Altas/AltaCaratulacion/AltaCaratulacion.vue'
import AltaFirma from '../Altas/AltaFirma/AltaFirma.vue'
import AltaPase from '../Altas/AltaPase/AltaPase.vue'
import AltaVinculacion from '../Altas/AltaVinculacion/AltaVinculacion.vue'
import axios from 'axios';
import './styles.css';

export default {

    name: 'MainGDE',
    components: {
        AltaCaratulacion,
        AltaFirma,
        AltaPase,
        AltaVinculacion,

    },
    data() {
        return {
            selectedOption: '',
            processToShow: '',
            currentPage: 1,
            perPage: 5,
            datos: [],
        }
    },
    computed: {
        totalPages() {
            return Math.ceil(this.datos.length / this.perPage);
        },
        paginatedData() {
            const start = (this.currentPage - 1) * this.perPage;
            const end = start + this.perPage;
            return this.datos.slice(start, end);
        },
    },
    methods: {
        showSelectedProcess() {
            if (this.selectedOption !== '') {
                this.processToShow = this.selectedOption
            }
        },
        changePage(offset) {
            if (!this.datos.length) {
                return;
            }
            if (this.currentPage === 1 && offset === -1) {
                return;
            }
            this.currentPage += offset;
            if (this.currentPage > this.totalPages) {
                this.currentPage = this.totalPages;
            }
        },
        goToFirstPage() {
            this.currentPage = 1;
        },
        goToLastPage() {
            this.currentPage = this.totalPages;
        },
    },
    created() {
        axios.get('https://localhost:5001/api/AltaPadre')
            .then(response => {
                this.datos = response.data;
            })
            .catch(error => {
                console.error(error);
            });
    },
};
</script>
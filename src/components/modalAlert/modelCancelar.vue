<!-- <template>
    <div>
        <button @click="showModal = true">X Cancelar</button>
        <Modal v-if="showModal" @close="showModal = false" v-model="showModal" class="containerModal">
            <h3 slot="header">¿Está seguro?</h3>
            <div slot="body">
                ¿Desea realmente continuar con esta acción?
            </div>
            <div slot="footer">
                <button @click="showModal = false">No</button>
                <button @click="continueAction">Sí</button>
            </div>
        </Modal>

    </div>
</template>

<script>


export default {
    name: 'ModalCancelar',

    data() {
        return {
            showModal: true
        };
    },
    methods: {
        continueAction() {
            this.showModal = false;
            // Aquí se puede escribir el código que se ejecutará al presionar el botón "Sí"
        }
    }
};
</script>
<style>
.modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 10;
}

.containerModal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    padding: 1rem;
    border-radius: 0.5rem;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    z-index: 11;
}
</style> -->
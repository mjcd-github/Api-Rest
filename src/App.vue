<script>
import userView from './components/userView.vue'
import chatView from './components/chatView.vue'

export default {
    components: {
        userView,
        chatView,
    },
    data() {
        return {
            mensajes: [],       
           
        }
    },
    methods: {

        agregarMensaje(mensaje, usuario, colorBoton,id) {
            this.mensajes.push({
                texto: mensaje,
                usuario: usuario,
                colorBoton: colorBoton,
                id: id

            });
            this.$refs.chatComponent.scrollToBottom();
            
        },      
    }
       
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col col-md-4">
                <userView id="usr1" @enviarMensaje="agregarMensaje" colorBoton="#ccebff"/>
            </div>
            <div class="col col-md-4">
                <chatView ref="chatComponent" :mensajes="mensajes"/>
            </div>
            <div class="col col-md-4" style="text-align: right;">
                <userView id="usr2" @enviarMensaje="agregarMensaje" colorBoton="#fffefa"/>
           
            </div>
        </div>
    </div>

</template>

<style scoped>
.container {
    display: flex;
    justify-content: center;
}

.row {
    display: flex;
}
.col{
    margin: 10px;
}
</style>

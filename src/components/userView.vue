<script>
import axios from 'axios';
export default {
    name: 'userView',
    data() {
        return {
            user: {
                name: { first: '', last: '' }, 
                picture: { large: '' }
            },
            colorUser: this.colorBoton,
            chat: '',
            
        }
    },
    props: {
        colorBoton: {
            type: String,
            default: '#ff0000'
        },
        id: {
            type: String,
            default: 'usr1'
        }
    },
    async mounted() {
        await this.listarUser();
    },
    computed: {
        infoUser() {
            return {
                name: this.user.name.first,
                last: this.user.name.last,
                foto: this.user.picture.large,
            }
        }
    },
    methods: {
        async getUser() {
            const url = 'https://randomuser.me/api?results=1';
            const { data } = await axios.get(url);
            return data.results[0];
        },

        async listarUser() {
            this.user = await this.getUser();
        },
        enviarMensaje() {
            if (this.chat.trim()) {
                const mensaje = this.chat; 
                this.$emit('enviarMensaje', mensaje, `${this.infoUser.name} ${this.infoUser.last}`, this.colorUser, this.id); 
                this.chat = ''; 
                             
            }
            
        },
        

    },
}
</script>

<template>
    <div class="usuario" id="usr1">
        <img :src="infoUser.foto" alt="">
        <h5 > {{ infoUser.name }} {{ infoUser.last }}</h5>
        <input class="inputColor" type="color" v-model="colorUser">
        <textarea ref="textarea" cols="30" rows="8" v-model="chat" @keydown.enter.prevent="enviarMensaje"></textarea>
        <button @click="enviarMensaje">Enviar</button>
    </div>
</template>

<style scoped>
.usuario {
    display: flex;
    flex-direction: column;
}

.inputColor {
    width: 100%;
}
textarea {
    resize: none;
}
</style>
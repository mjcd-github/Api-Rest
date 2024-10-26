<script>
export default {

    props: {
        mensajes: {
            type: Array,
            required: true
        }
    },
    
    methods: {
        scrollToBottom() {
            this.$nextTick(() => {
                const container = this.$refs.chatContainer;
                if (container) {
                    container.scrollTop = container.scrollHeight;
                }
            });
        }

    }
}
</script>

<template>
    <div>
        <div class="chat" ref="chatContainer">
            <div v-for="(msg, index) in mensajes" :key="index" class="message" :class="msg.id == 'usr2' ? 'usr2' : ''">
                <div class="nomMsg">{{ msg.usuario }}</div>
                <div class="formatoMsg" :style="{ backgroundColor: msg.colorBoton }">{{ msg.texto }}</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.chat {
    width: 500px;
    height: 460px;
    padding: 10px;
    background-color: #efe7dd;
    border: 2px solid grey;
    border-radius: 5px;
    overflow-y: scroll;

}

.formatoMsg {
    display: inline-block;
    padding: 10px;
    border-radius: 50px;
}

.usr2 {
    text-align: right;
}
.nomMsg{
    font-style: italic;
    font-size: 12px;
    color: grey;
    margin-top: 8px;
}
</style>
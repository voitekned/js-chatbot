<template>
    <div id="chatContainer">
        <div class="chatBody" id="chat-room">
            <div class="messages" v-for="message in messages" :key="message.id">
                <div class="messageRow user" v-if="message.id % 2 == 0">
                    <div class="message user">
                        <p>{{ message.message }}</p>
                    </div>
                </div>
                <div class="messageRow bot" v-else>
                    <div class="message bot">
                        <p>{{ message.message }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div class="chatFooter">
            <form @submit.prevent="sendMessage()">
                <input
                    v-model="messageContent"
                    id="createMessage"
                    placeholder="Type your message ..."
                />
                <input type="submit" value="send" />
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import { ref } from 'vue';
export default {
    name: 'App',
    setup() {
        const messages = ref([]),
            messageContent = ref('');

        //Sends the message on form submit
        function sendMessage() {
            if (messageContent.value == '') return;
            createMessage(messageContent.value);
            getResponse(messageContent.value);
            messageContent.value = '';
        }

        //Create a message
        function createMessage(message) {
            let id = 0;
            if (messages.value[messages.value.length - 1]) {
                id = messages.value[messages.value.length - 1].id + 1;
            }
            messages.value.push({
                id: id,
                message: message,
            });
        }

        async function getResponse(message) {
            const postData = {
                message: message,
            };
            const { data } = await axios.post('http://localhost:8000/chat', postData);
            const { response } = data;
            createMessage(response);
        }

        return { messages, messageContent, sendMessage };
    },
};
</script>

<style>
#chatContainer {
    background-color: #e4dcdc;
    height: 700px;
    width: 40%;
    margin: 30px auto;
    display: flex;
    flex-direction: column;
    position: relative;
}
.chatFooter {
    background-color: #d3caca;
    position: absolute;
    bottom: 0px;
    width: 100%;
    margin-bottom: 0px;
}
.chatFooter form {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 95%;
    margin: 0 auto;
    margin-top: 15px;
}
.chatBody {
    overflow-y: scroll;
    width: 500px;
    height: 83%;
    margin: 0 auto;
    background-image: url('../src/assets/logo-EIGO.png');
    background-size: contain;
    background-repeat: no-repeat;
    background-position: bottom;
    background-color: rgba(133, 127, 127, 0);
}
#createMessage {
    width: 70%;
    padding: 25px;
    margin-bottom: 15px;
    border: 0;
    font-size: 20px;
}
input:not(#createMessage) {
    background-color: rgb(73, 121, 73);
    border: 0;
    color: white;
    padding: 25px;
    margin-bottom: 15px;
    margin-left: 10px;
    font-size: 20px;
}
input:not(#createMessage):hover {
    opacity: 0.8;
}
.messageRow {
    display: flex;
    justify-content: flex-end;
}
.messageRow.bot {
    justify-content: flex-start;
}
.message p {
    color: white;
    padding: 0px 15px 0px 15px;
}
.message {
    border-radius: 20px;
    text-align: center;
    margin: 20px;
}
.messageRow.user .message {
    background-color: #79aeea;
    position: relative;
    padding: 10px;
}

.messageRow.user .message:before {
    content: '';
    position: absolute;
    display: block;
    width: 0;
    height: 0;
    right: -15px;
    top: 20px;
    border-left: 15px solid #79aeea;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
}

.messageRow.bot .message {
    background-color: #71a173;
    position: relative;
    padding: 10px;
}

.messageRow.bot .message:before {
    content: '';
    position: absolute;
    display: block;
    width: 0;
    height: 0;
    left: -15px;
    top: 20px;
    border-right: 15px solid #71a173;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
}

.chatBody::-webkit-scrollbar {
    width: 0px;
    height: 100%;
}
</style>

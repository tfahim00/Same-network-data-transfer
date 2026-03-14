<script setup>
import { ref, onMounted } from "vue"

const ws = ref(null)
const message = ref("")
const messages = ref([])

onMounted(() => {
  ws.value = new WebSocket("ws://192.168.0.177:3000")

  ws.value.onopen = () => {
    console.log("Connected to websocket")
  }

  ws.value.onmessage = (event) => {
    messages.value.push(event.data)
  }
})

function sendMessage() {
  if (message.value && ws.value) {
    ws.value.send(message.value)
    message.value = ""
  }
}
</script>

<template>
  <div class="container">
    <h2>Realtime Messages</h2>

    <input
      v-model="message"
      placeholder="Type message..."
      @keyup.enter="sendMessage"
    />

    <button @click="sendMessage">Send</button>

    <div class="messages">
      <p v-for="(msg, index) in messages" :key="index">
        {{ msg }}
      </p>
    </div>
  </div>
</template>

<style scoped>
.container{
  max-width:600px;
  margin:auto;
}

.messages{
  margin-top:20px;
  border:1px solid #ddd;
  padding:10px;
}
</style>
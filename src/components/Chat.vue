<template>
  <div class="chat-box">
    <div
      v-for="(message, index) in messages"
      :key="index"
      class="message"
      :style="{ backgroundColor: message.color }"
    >
      <strong>{{ message.name }}: </strong>{{ message.content }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    messages: Array
  }
};
</script>

<style scoped>
.chat-box {
  height: 100%;
  overflow-y: auto;
  padding: 15px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
}

.message {
  padding: 15px;
  margin-bottom: 15px;
  border-radius: 10px;
  color: #333;
  background-color: #e1e1e1;
  width: 100%;
  box-sizing: border-box;
  word-wrap: break-word;
}
</style>

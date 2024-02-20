<template>
    <div>
      <div class="message-box">
        <h1>Hello, user!</h1>
        <p>
          Express yourself anonymously with our message-sharing app where users
          can post anything from random thoughts to heartfelt confessions in a
          safe space.
        </p>
  
        <!-- Textbox -->
        <div class="textbox-container">
          <textarea
            v-model="message"
            placeholder="Ex: Hello World! -John Doe"
            rows="5"
          ></textarea>
          <div v-if="successMessage" class="error-message">{{ successMessage }}</div>
          <button class="s-btn" @click="sendMessage"><i class="bx bxs-send"></i></button>
        </div>
      </div>
  
      <!-- Container for Messages -->
      <div class="messages-container">
        <div v-for="(message, index) in messages" :key="index" class="message">
          <p>{{ message.content }}</p>
          <span>{{ message.timestamp }}</span>
          <button class="d-btn" @click="deleteMessage(index)"><i class='bx bx-x-circle'></i></button>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const message = ref('');
  const successMessage = ref('');
  const messages = ref([]);
  
  //LOAD MESSAGE
  onMounted(() => {
    const savedMessages = JSON.parse(localStorage.getItem('messages'));
    if (savedMessages) {
      messages.value = savedMessages;
    }
  });
  
  //INPUT MESSAGE
  const sendMessage = () => {
    if (message.value.trim() !== '') {
      const newMessage = {
        content: message.value,
        timestamp: new Date().toLocaleString()
      };
      messages.value.unshift(newMessage);
      message.value = '';
      successMessage.value = '';
    //SAVE MESSAGE
      localStorage.setItem('messages', JSON.stringify(messages.value));
    } else {
      successMessage.value = 'Please enter a message before sending.';
    }
  };
  
  //DELETE
  const deleteMessage = (index) => {
    messages.value.splice(index, 1);
    localStorage.setItem('messages', JSON.stringify(messages.value));
  };
  
  </script>
  


<style lang="scss" scoped>
.message-box {
    padding: 1rem;
    background-color: #202020;
    border-radius: 5px;
    margin: 1rem;
}

.success-message {
    color: rgb(83, 161, 83);
    margin-top: 0.5rem;
    font-size: 14px;
}

.error-message {
    color: red;
    font-size: 14px;
}

h1 {
    color: #f5a576;
    font-size: 25px;
}

p {
    color: #b6b6b6;
}

.textbox-container {
    margin-top: 1rem;
}

textarea {
    width: 100%;
    padding: 0.5rem;
    border-radius: 5px;
    border: 1px solid #ccc;
}

.textbox-container {
    margin-top: 1rem;
}

textarea {
    font-family: 'Inter', sans-serif;
    width: 100%;
    padding: .8rem;
    border-radius: 5px;
    font-size: 15px;
    color: #202020;
    border: 1px solid #ccc;
}

textarea::placeholder {
    font-size: 14px;
}

.s-btn {
    background-color: #f5a576;
    color: #ffffff;
    padding: 0.5rem 2rem;
    border: none;
    border-radius: 5px;
    font-size: 15px;
    cursor: pointer;
    margin-top: 0.5rem;
    transition: all ease 0.8s;
}

.s-btn:hover {
    background-color: #fc8947;
}

i {
    font-size: 20px;
}

/* Messages container styles */
.messages-container {
    border-radius: 5px;
    margin: 1rem;
    padding: 1rem;
    max-height: 300px; 
    overflow-y: auto;
    background-color: #202020;
}
.message {
    background-color: #f5f5f50c;
    padding: 0.5rem;
    border-radius: 5px;
    border: 1px solid #3d3c3c;
    margin-bottom: 10px;
    position: relative;
}
.d-btn {
    position: absolute;
    top: 0;
    right: 0;
    color: rgb(112, 112, 112);
    background-color: transparent;
    border: none;
}
.message p {
    margin: 0;
    color: #b6b6b6;
}

.message span {
    font-size: 12px;
    color: #999;
}

@media screen and (min-width: 768px) {
    .button-container {
        display: flex;
        justify-content: center;
    }
}
</style>
  
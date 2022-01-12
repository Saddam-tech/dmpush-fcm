<template>
  <div class="container">
    <h1>Send notifications</h1>
    <input
      type="text"
      id="token"
      v-model="token"
      placeholder="Enter user token"
    />
    <input type="text" id="Title" v-model="title" placeholder="Title" />
    <input type="text" id="msg" v-model="msg" placeholder="MSG" />
    <button @click="sendNotification">Send</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      token: "",
      title: "",
      msg: "",
    };
  },
  methods: {
    sendNotification() {
      let body = {
        to: this.token,
        notification: {
          title: this.title,
          message: this.msg,
        },
      };
      console.log(body);
    },
  },
};
</script>

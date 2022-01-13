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
          body: this.msg,
          image:
            "https://images.unsplash.com/photo-1582266255765-fa5cf1a1d501?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxzZWFyY2h8MXx8YW5vbnltb3VzfGVufDB8fDB8fA%3D%3D&w=1000&q=80",
          click_action: "https://saddamtech.com",
        },
      };
      let options = {
        method: "POST",
        headers: new Headers({
          Authorization:
            "key=AAAAPY9g9ws:APA91bFB6Mz6WVv2MadtzfXOBw4fbYJPsghrFj4rWq3SrEnWG5bCiJKF-dorhMXSjNflFEuXiL8DFrQ6ZqAWLOs6UtwvYcEDBAwu9GLVskxA4Ln02nxIMKllqUHJ-RSuMXK7HIKF8dvi",
          "Content-Type": "application/json",
        }),
        body: JSON.stringify(body),
      };

      fetch("https://fcm.googleapis.com/fcm/send", options)
        .then((res) => {
          console.log(res);
          console.log("Sent");
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>

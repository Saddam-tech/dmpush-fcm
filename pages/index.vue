<template>
  <div class="container">
    <h1>FCM push notifications</h1>
    <a @click="authenticate">Authenticate</a>
    <NuxtLink to="/send">Send Notification</NuxtLink>
  </div>
</template>

<script>
import { getAuth, signInAnonymously } from "firebase/auth";
import { getMessaging, onMessage, getToken } from "firebase/messaging";
import { messaging } from "@/plugins/firebase";

export default {
  name: "IndexPage",
  mounted() {
    const messaging = getMessaging();

    onMessage(messaging, (payload) => {
      const body = payload.notification.body;
      const title = payload.notification.title;
      const img = payload.notification.image;

      alert(body, title, img);
      console.log("Message on client: ", payload);
    });
  },
  methods: {
    async authenticate() {
      Notification.requestPermission().then(async (permission) => {
        console.log(permission);
        await signInAnonymously(getAuth());
        this.activate();
      });
    },
    async activate() {
      const token = await getToken(messaging, {
        vapidKey:
          "BHVpfN_OJcA9743IK5yHv4mTuOHKPE8Gh_y62i_SUcKt8Ue1CGhHX4JEOsMCMwAfrfMMZtzZ98p19Hpq-1XDHlQ",
      });

      if (token) {
        console.log(token);
      }
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  text-align: center;
}

.container a {
  margin-top: 20px;
  cursor: pointer;
}
</style>

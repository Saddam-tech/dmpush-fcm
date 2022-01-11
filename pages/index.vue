<template>
  <div class="container">
    <h1>FCM push notifications</h1>
    <a @click="authenticate">Authenticate</a>
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

      alert(body);
      console.log("Message on client: ", payload);
    });
  },
  methods: {
    async authenticate() {
      await signInAnonymously(getAuth());
      this.activate();
    },
    async activate() {
      const token = await getToken(messaging, {
        vapidKey:
          "BHVpfN_OJcA9743IK5yHv4mTuOHKPE8Gh_y62i_SUcKt8Ue1CGhHX4JEOsMCMwAfrfMMZtzZ98p19Hpq-1XDHlQ",
      });

      if (token) {
        console.log(token);
      } else {
        // Request permission
      }
    },
  },
};
</script>

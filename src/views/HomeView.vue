<template>
  <div class="home">
    <NavBar :user="user" />
    <img alt="Vue logo" src="../assets/logo.png" />
    <Form />
  </div>
</template>

<script>
import Form from "@/components/Form.vue";
import NavBar from "@/components/NavBar.vue";

export default {
  name: "HomeView",
  components: {
    Form,
    NavBar,
  },
  data() {
    return {
      user: undefined,
    };
  },
  mounted() {
    this.getUserInfo()
  },
  methods: {
    async getUserInfo() {
      try {
        const response = await fetch("/.auth/me");
        const payload = await response.json();
        const { clientPrincipal } = payload;

        if (clientPrincipal) {
          this.user = clientPrincipal
          console.log(`clientPrincipal = ${JSON.stringify(clientPrincipal)}`);
        }
      } catch (error) {
        console.error("No profile could be found " + error.message.toString());
      }
    },
  },
};
</script>

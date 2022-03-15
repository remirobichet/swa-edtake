<template>
  <div class="home">
    <div>
      <input
        type="text"
        id="name"
        className="App-input"
        placeholder="Name"
        v-model="name"
      />
      <button className="App-button" @click="getDataFromApi">Submit</button>
    </div>
    <div>
      <h5>Message: {{ message }}</h5>
    </div>
  </div>
</template>

<script>
export default {
  name: "Form",
  components: {},
  data() {
    return {
      name: undefined,
      message: undefined,
    };
  },
  methods: {
    async getDataFromApi() {
      try {
        const data = await fetch(`/api/hello?name=${this.name}`);
        const json = await data.json();
        if (json.message) {
          this.message = json.message;
        }
      } catch (err) {
        console.log(`error:`, err);
        this.message = "Error: you must be connected !";
      }
    },
  },
};
</script>

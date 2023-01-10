<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required />
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>
  
<script>
export default {
  name: "EditProject",
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
    };
  },
  mounted() {
    fetch(`http://localhost:3000/projects/${this.id}`)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      });
  },
  methods: {
    handleSubmit() {
      fetch(`http://localhost:3000/projects/${this.id}`, {
        method: "PATCH", // passing on a second argument with multiple atrributes
        headers: { "Content-Type": "application/json" }, // informations about the file we are sending - json apllication
        body: JSON.stringify({ title: this.title, details: this.details }), //what we are acti\ually sending ()
      })
        .then(() => this.$router.push("/"))
        .catch((err) => console.log(err));
    },
  },
};
</script>
  

<style scoped>
form {
  background: white;
  padding: 20px;
  border-radius: 5px;
}
label {
  display: block;
  color: #bbb;
  font-size: 14px;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  display: block;
  border: none;
  border-bottom: 1px solid #ddd;
  width: 100%;
  padding: 10px;
  box-sizing: border-box;
  cursor: pointer;
}
input:focus {
  outline: none;
  border-bottom: 2px solid rgba(71, 129, 93, 0.25);
}
textarea {
  border: 1px solid #ddd;
  width: 100%;
  height: 100px;
  box-sizing: border-box;
  padding: 10px;
  cursor: pointer;
}
textarea:focus {
  outline: none;
  border: 2px solid rgba(71, 129, 93, 0.25);
}
form button {
  display: block;
  border: none;
  margin: 20px auto 0;
  font-size: 16px;
  padding: 10px;
  background: rgb(71, 129, 93);
  border-radius: 6px;
  color: white;
  cursor: pointer;
}
</style>
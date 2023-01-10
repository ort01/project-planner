<template>
  <form @submit.prevent="handleSubmit">
    <label>Title:</label>
    <input type="text" v-model="title" required />
    <label>Details:</label>
    <textarea v-model="details" required></textarea>
    <button>Add Project</button>
  </form>
</template>

<script>
export default {
  name: "AddProject",
  props: [],
  data: () => {
    return {
      title: "",
      details: "",
    };
  },
  methods: {
    handleSubmit() {
      let newProject = {
        title: this.title,
        details: this.details,
        complete: false,
      };
      fetch("http://localhost:3000/projects", {
        //route taht i want to connect with
        method: "POST", //methof
        headers: { "Content-Type": "application/json" }, //type of data
        body: JSON.stringify(newProject), //what i am sending (turning it into JSON string)
      })
        .then(() => {
          this.$router.push("/"); //redirecting to home route after the post request is finished
        })
        .catch((err) => console.log(err));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
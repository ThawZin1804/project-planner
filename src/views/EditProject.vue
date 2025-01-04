<template>
  <h1>Edit Project</h1>
  <form @submit.prevent="updateProject">
    <label>Project Title</label>
    <input type="text" v-model="name" />
    <label>Project Detail"></label>
    <input type="text" v-model="detail" />
    <button @click="updateProject">Update Project</button>
  </form>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      name: "",
      detail: "",
    };
  },
  mounted() {
    fetch(`http://localhost:3000/projects/` + this.id)
      .then((res) => {
        return res.json();
      })
      .then((datas) => {
        this.name = datas.name;
        this.detail = datas.detail;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  methods: {
    updateProject() {
        fetch("http://localhost:3000/projects/" + this.id, {
          method: "PATCH",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            name: this.name,
            detail: this.detail,
          }),
        })
          .then(() => {
            this.$router.push("/");
          })
          .catch((err) => {
            console.log(err);
          });
    },
  },
};
</script>

<style></style>

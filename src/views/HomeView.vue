<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id">
      <SingleComponent :project="project"></SingleComponent>
    </div>
  </div>
</template>

<script>
import SingleComponent from "../components/SingleComponent";
// @ is an alias to /src

export default {
  name: "HomeView",
  components: {
    SingleComponent,
  },
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects")
      .then((response) => {
        return response.json();
      })
      .then((data) => {
        this.projects = data;
      })
      .catch(() => {});
  },
};
</script>

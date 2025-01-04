<template>
  <div class="home">
    <h1>Home</h1>
    <div v-for="project in projects" :key="project.id" >
      <SingleComponent :project="project" @delete="deleteProject" @complete="completeProject"></SingleComponent>
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
  methods: {
    deleteProject(id){
      this.projects = this.projects.filter(project => {
      return project.id !== id;
    })
    },
    completeProject(id){
      let findProject = this.projects.find(project => {
        return project.id === id
      })
      findProject.complete = !findProject.complete
    }
  },
  /**
   * Lifecycle hook which is called when the component is mounted.
   * Fetches the list of projects from the db.json file.
   */
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

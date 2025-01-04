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
/*************  ✨ Codeium Command ⭐  *************/
/******  aa6f0076-c76b-4007-a6d3-61fd4a11299b  *******/
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
/*************  ✨ Codeium Command ⭐  *************/
  /**
   * Lifecycle hook which is called when the component is mounted.
   * Fetches the list of projects from the db.json file.
   */
/******  93d8fbb0-46de-465d-9daa-edbed2941d11  *******/
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

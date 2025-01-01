<template>
  <div class="project" >
    <div class="flexing">
      <div>
        <h3 @click="showDetail = !showDetail">{{ project.name }}</h3>
      </div>
      <div>
        <span class="material-icons"> delete </span>
        <span class="material-icons"> edit </span>
        <span class="material-icons"> done </span>
      </div>
    </div>
    <p v-if="showDetail">{{ project.detail }}</p>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetail: false,
    };
  },
};
</script>

<style>
.project {
  padding: 20px;
  background-color: #f2f2f2;
  margin: 10px;
  border-radius: 6px;
  border-left: 6px solid red;
}

h3 {
  color: indigo;
  cursor: pointer;
}

.flexing {
  display: flex;
  justify-content: space-between;
  align-items: center;
  
}

span{
  margin-left: 15px;
}

span:hover{
  cursor: pointer;
  color: #777
}
</style>

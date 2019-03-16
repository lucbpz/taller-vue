<template>
  <div id="Projects">
    <input type="text" v-model="inputText" placeholder="search...">
    <div v-if="showProjects">
      <ProjectCard
        v-for="(project, index) of filteredProjects"
        :key="index"
        v-bind:name="project.name"
        v-bind:description="project.description"
        v-bind:id="project.id"
        :onRemove="remove"
      />
    </div>
    <div v-if="!showProjects">
        No projects found
        <button @click="add">Add</button>
    </div>
  </div>
</template>


<style lang="scss">
</style>




<script>
import ProjectCard from "../components/ProjectCard";
export default {
  name: "Projects",
  components: {
    ProjectCard
  },
  data: () => ({
      i: 3,
    projects: [
      {
        id: 1,
        name: "NombreASDF",
        description: "descripcion"
      },
      {
        id: 2,
        name: "Nombre2",
        description: "descripcion2"
      }
    ],
    inputText: ""
  }),
  computed: {
    filteredProjects: function() {
      return this.projects.filter(
        p => p.name.toLowerCase().indexOf(this.inputText.toLowerCase()) > -1
      );
    },
    showProjects: function() {
      return this.filteredProjects.length !== 0;
    }
  },
  methods: {
    remove: function(id) {
      this.projects = this.projects.filter(p => p.id != id);
    },
    add: function() {
      this.projects.push({ id: this.getKey(), name: this.inputText, description: "" });
      this.inputText = "";
    },
    getKey: function() {
        return this.i++;
    }
  }
};
</script>

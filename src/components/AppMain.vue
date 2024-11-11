<script>
import axios from "axios";
export default {
  data() {
    return {
      projects: [],
    };
  },
  mounted() {
    this.getProjects();
  },
  methods: {
    getProjects() {
      axios.get("http://127.0.0.1:8000/api/projects").then((res) => {
        this.projects = res.data.data.projects.data;
        console.log(this.projects);
      });
    },
  },
};
</script>

<template>
  <main>
    <div class="post-container">
      <div class="card" v-for="project in projects" :key="project.id">
        <h3>{{ project.title }}</h3>

        <h5 v-if="project.type">
          {{ project.type.name }}
        </h5>

        <div
          class="technology-container"
          v-if="project.technologies && project.technologies.length > 0"
        >
          <div v-for="technology in project.technologies" :key="technology.id">
            {{ technology.name }}
          </div>
        </div>
      </div>
    </div>
  </main>
</template>


<style scoped>
.post-container {
  display: flex;
  justify-content: space-around;
}
</style>
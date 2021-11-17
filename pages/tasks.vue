<template>
  <div class="container mx-auto my-2 bg-blue-300 bg-opacity-25">
    <NavBar />
    <div class="grid sm:grid-cols-2 md:grid-cols-3">
      <TaskForm class="pl-2 col-span-1" :updateTasks="loadTasks"/>
      <div class="pl-2 pt-2 pr-2 md:col-span-2">
        <div
          class="
            task-container
            place-items-center
            grid grid-cols-1
            gap-2
            md:grid-cols-2
            place-items-stretch
          "

        >
          <Task v-for="(task, index) in tasks"
          :key="index" :id="task._id" :title="task.title" :description="task.description" :ready="task.ready" :updateTasks="loadTasks"/>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import config from "../config";
export default {
  data() {
    return {
      tasks: [],
    };
  },
  async beforeMount() {
    await this.loadTasks()
  },
  methods: {
    async loadTasks() {
      const token = window.localStorage.getItem("token");
      if (!token) {
        window.localStorage.clear();
        this.$router.push("/signin");
      }
      const user_id = window.localStorage.getItem('user');
      try {
        const res = await fetch(config.HOSTNAME + `/tasks/all/${user_id}`, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
        });
        const data = await res.json();
        if (data.err) {
          alert(data.err);
        }
        this.tasks = data;
      } catch (err) {
        alert(err.message);
      }
    },
  },
};
</script>

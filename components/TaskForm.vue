<template>
  <div class="task-form flex justify-center pt-2">
    <form class="bg-white shadow-md rounded px-8 pt-6 pb-6 mb-4">
      <div>
        <h2 class="mb-4 text-center text-2xl font-extrabold text-gray-900">
          Create Task
        </h2>
      </div>
      <div class="mb-4">
        <input
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          v-model="title"
          id="task"
          type="text"
          placeholder="Task title"
        />
      </div>
      <div class="mb-2">
        <textarea
          v-model="description"
          class="
            shadow
            appearance-none
            border
            rounded
            w-full
            py-2
            px-3
            text-gray-700
            mb-3
            leading-tight
            focus:outline-none focus:shadow-outline
          "
          id="description"
          type="text"
          placeholder="Task Description"
        />
      </div>
      <div class="flex justify-center">
        <button
          class="
            bg-blue-500
            hover:bg-blue-700
            text-white
            font-bold
            py-2
            px-4
            rounded
            focus:outline-none focus:shadow-outline
          "
          type="button"
          @click="createTask()"
        >
          Submit
        </button>
      </div>
    </form>
  </div>
</template>
<script>
import config from "../config";
export default {
  data() {
    return {
      title: "",
      description: "",
    };
  },
  props: {
    updateTasks: {
      type: Function,
      required: true,
    },
  },
  methods: {
    async createTask() {
      if (!this.title || !this.description) {
        alert("Bad request, required fields missing!");
        return;
      }
      const hostname = config.HOSTNAME + "/tasks/create-task";
      const token = window.localStorage.getItem("token");
      const user_id = window.localStorage.getItem("user");

      if (!user_id) {
        this.$router.push("/signin");
        return;
      }
      const body = {
        title: this.title,
        description: this.description,
        user_id,
      };
      console.log(body);
      try {
        const res = await fetch(hostname, {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
          body: JSON.stringify(body),
        });

        const data = await res.json();

        if (data.error) {
          alert(data.error);
          return;
        }

        this.title = "";
        this.description = "";

        this.updateTasks();
      } catch (err) {
        alert(err.message);
      }
    },
  },
};
</script>

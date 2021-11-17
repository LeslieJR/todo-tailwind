<template>
  <div class="bg-white max-w-sm rounded overflow-hidden shadow-lg">
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{ title }}</div>
      <p class="text-gray-700 text-base">
        {{ description }}
      </p>
      <button
        @click="onEdit"
        class="
          bg-blue-500
          hover:bg-blue-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        Edit
      </button>
      <button
        @click="onRemove(id)"
        class="
          bg-red-500
          hover:bg-red-700
          text-white
          font-bold
          py-2
          px-4
          rounded
        "
      >
        Remove
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
    ready: {
      type: Boolean,
      default: false,
    },
    updateTasks: {
      type: Function,
      required: true,
    },
  },

  methods: {
    onEdit() {},
    async onRemove(id) {
      const hostname = `http://localhost:4200/tasks/remove/${id}`;
      const token = window.localStorage.getItem("token");
      const user_id = window.localStorage.getItem("user");
      if (!token || !user_id) {
        localStorage.clear();
        return this.$router.push("/signin");
      }
      const body = JSON.stringify({
        user_id,
      });
      try {
        const res = await fetch(hostname, {
          method: "delete",
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`,
          },
          body,
        });

        const data = await res.json();
        if (data.err) {
          alert(data.err);
          return;
        }

        this.updateTasks();
      } catch (err) {
        alert(err.message);
      }
    },
  },
};
</script>

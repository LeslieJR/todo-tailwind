<template>
  <div class="container mx-auto my-2 bg-blue-300 bg-opacity-25">
    <NavBar />
    <div class="task-details flex justify-center pt-2">
      <form class="bg-white shadow-md rounded px-8 pt-6 pb-6 mt-4 mb-4">
        <div>
          <h2 class="mb-4 text-center text-2xl font-extrabold text-gray-900">
            Update Task
          </h2>
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="task">
            Task
          </label>
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
            id="task"
            type="text"
            placeholder="Task title"
            v-model="title"
          />
        </div>
        <div class="mb-2">
          <label
            class="block text-gray-700 text-sm font-bold mb-2"
            for="description"
          >
            Description
          </label>
          <textarea
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
            v-model="description"
          />
        </div>
         <div class="md:flex md:items-center mb-6">
    <div class="md:w-1/3"></div>
    <label class="md:w-2/3 block text-gray-500 font-bold">
      <input v-model="ready" class="mr-2 leading-tight" type="checkbox">
      <span class="text-sm">
        Ready
      </span>
    </label>
  </div>
        <div class="flex justify-center">
          <button
          @click="updateTask"
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
          >
            Submit
          </button>
        </div>
        <div class="flex justify-center">
          <a
            class="
              inline-block
              align-baseline
              font-bold
              text-sm text-blue-500
              hover:text-blue-800
            "
            href="/tasks"
          >
            Go to Tasks
          </a>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import config from '../../../config'
export default{
  data() {
    return{
      title:'',
      description:'',
      ready: false
    }
  },
  beforeMount(){
    this.loadTask()
  },
  methods:{
    async loadTask(){
      const task_id = this.$route.params.id;
      const hostname = config.HOSTNAME + `/tasks/get/${task_id}`
      const token = window.localStorage.getItem("token");
      if (!token) {
        window.localStorage.clear();
        this.$router.push("/signin");
      }
      
      try {
        const res = await fetch(hostname, {
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`
          },
        });
        const data = await res.json();
        if (data.err) {
          alert(data.err);
        }
        
        this.title = data.title;
        this.description = data.description;
        this.ready = data.ready;
        
      } catch (err) {
        alert(err.message);
      }
    },
    async updateTask(){
      const task_id = this.$route.params.id;
      const hostname = config.HOSTNAME +`/tasks/update/${task_id}`;
      const token = window.localStorage.getItem("token");
      if (!token) {
        window.localStorage.clear();
        this.$router.push("/signin");
      }
      const body = {
        title: this.title,
        description: this.description,
        ready: this.ready
      }
      try {
        const res = await fetch(hostname, {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
            Authorization: `Bearer ${token}`
          },
          body: JSON.stringify(body),
        });
        const data = await res.json();
        if (data.err) {
          alert(data.err);
        }
        console.log(data)
        this.$router.push('/tasks')
      } catch (err) {
        alert(err.message);
      }
    }
  }
}
</script>

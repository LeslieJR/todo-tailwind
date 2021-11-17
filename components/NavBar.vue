<template>
  <div class="task-navbar">
    <nav class="bg-gray-800">
      <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
        <div class="relative flex items-center justify-between h-16">
          <div
            class="
              flex-1 flex
              items-center
              justify-end
              sm:items-stretch sm:justify-end
            "
          >
            <button
            @click="onLogout"
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
              Logout
            </button>
          </div>
        </div>
      </div>
    </nav>
  </div>
</template>
<script>
export default {
  methods:{
    onLogout(){
      try{
        const token = window.localStorage.getItem('token')
        if(!token){
          console.log('no token saved')
        }
        window.localStorage.clear()
        this.$router.push('/signin')
      }catch(err){
        console.log(err.message)
      }
    }
  }
}
</script>

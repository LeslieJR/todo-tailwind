<template>
  <div class="container mx-auto my-2 bg-blue-300 bg-opacity-25">
    <NavBar />
    <div class="grid sm:grid-cols-2 md:grid-cols-3">
      <TaskForm class="pl-2 col-span-1" />
      <div class="pl-2 pt-2 pr-2 md:col-span-2">
         <div class="task-container place-items-center grid grid-cols-1 gap-2 md:grid-cols-2 place-items-stretch">
        <Task />
        <Task />
        <Task />
        <Task />
        <Task />
      </div> 
      </div>
      
    </div>
  </div>
</template>
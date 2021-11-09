<template>
  <div class="container mx-auto my-2 bg-blue-300 bg-opacity-25">
    <NavBar />
    <div class="grid grid-cols-3">
      <TaskForm class="col-span-1" />
      <div class="col-span-2 pt-2">
         <div class="task-container grid grid-cols-2 gap-2">
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
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
          id="task"
          type="text"
          placeholder="Task title"
        />
      </div>
      <div class="mb-2">
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
        >
          Submit
        </button>
      </div>
    </form>
  </div>
</template>
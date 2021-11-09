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
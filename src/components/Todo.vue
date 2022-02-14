<template>
  <div class="container mx-auto text-center">
    <!-- tle -->
    <h3 class="text-xl mb-6">MY VUE TODO APP</h3>
    <!-- image  -->
    <div class="w-32 h-32 bg-lime-600 mx-auto mb-8">
      <img
        class="w-full h-full rounded"
        src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSrmcC1UZr_OuGvQEkDecUevL8cFoW5x1Tsew&usqp=CAU"
        alt=""
      />
    </div>
    <!-- add  task -->
    <div class="flex justify-center mb-8">
      <div class="w-80 h-12 border rounded">
        <input
          v-model="task"
          class="w-full h-full text-center"
          type="text"
          placeholder="Ex: I must take a bath"
        />
      </div>
      <div class="w-24 h-12 bg-yellow-300 rounded flex items-center">
        <button @click="submitTask()" class="mx-auto" type="submit">
          Add Task
        </button>
      </div>
    </div>
    <!-- data table -->
    <div class="">
      <table class="border-collapse border border-slate-400 ... w-1/2 mx-auto">
        <thead>
          <tr>
            <th class="border border-slate-300 ...">Task</th>
            <th class="border border-slate-300 ...">Statut</th>
            <th class="border border-slate-300 ...">Edit</th>
            <th class="border border-slate-300 ...">Remove</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td class="border border-slate-300 ... ">
              <span :class="{ 'line-through': task.status === 'finished' }">
                       {{ task.name }}
              </span>
            </td>
            <td class="border border-slate-300">
              <span  id="pointeur"
               @click="changeStatus(index)"
              :class="{
                ' text-bold text-red-500 ': task.status === 'to-do',
                'text-bold  text-green-500 ': task.status === 'finished',
                ' text-bold text-orange-500 ': task.status === 'in-progress',
              }"
                class="
                  px-2
                  inline-flex
                  text-xs
                  
                "
              >
                {{ task.status }}
              </span>
            </td>
            <td class="border border-slate-300 ...">
              <!-- edit button -->
              <button @click="editTask(index)">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
                  />
                </svg>
              </button>
            </td>
            <td class="border border-slate-300 ...">
              <!-- remove button -->
              <button @click="deletetask(index)">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                  />
                </svg>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      ​
    </div>
  </div>
</template>


<script>
export default {
  name: "todo",
  data() {
    return {
   task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],

      /* Status could be: 'to-do' / 'in-progress' / 'finished' */
      tasks: [
        {
          name: "Steal bananas from the supermarket.",
          status: "to-do",
        },
        {
          name: "Eat 1 kg chocolate in 1 hour.",
          status: "in-progress",
        },
        {
          name: "Create YouTube video.",
          status: "finished",
        },
      ],
    };
  },
  
  methods: {
    /**
     * Capitalize first character
     */
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    /**
     * Change status of task by index
     */
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

    /**
     * Deletes task by index
     */
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    /**
     * Edit task
     */
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    /**
     * Add / Update task
     */
    submitTask() {
      if (this.task.length === 0) return;

      /* We need to update the task */
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        /* We need to add new task */
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      }

      this.task = "";
    },
  },
};
</script>


<style scoped>
#pointeur{
  cursor: pointer;

}
</style>


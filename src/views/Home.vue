<template>
  <div class="container">
    <div class="column">
      <h3>TODO</h3>
      <draggable class="custom-draggable" :list="tasks1" group="tasks">
        <li
          v-for="task in tasks1"
          :key="task.id"
          @dblclick="deleteTask1(task.id)"
        >
          {{ task.title }}

          <button class="edit-button" @click="editTask1(task.id)">
            <i class="edit-icon material-icons">edit</i>
          </button>
        </li>

        <input
          type="text"
          placeholder="Add a new task..."
          v-model="title1"
          @keyup.enter="addTask1()"
        />
      </draggable>
    </div>

    <div class="column">
      <h3>DONE</h3>
      <draggable class="custom-draggable" :list="tasks2" group="tasks">
        <li
          v-for="task in tasks2"
          :key="task.id"
          @dblclick="deleteTask2(task.id)"
        >
          {{ task.title }}

          <button class="edit-button" @click="editTask2(task.id)">
            <i class="edit-icon material-icons">edit</i>
          </button>
        </li>

        <input
          type="text"
          placeholder="Add a new task..."
          v-model="title2"
          @keyup.enter="addTask2()"
        />
      </draggable>
    </div>

    <EditTaskModal
      v-if="isShownTaskModal"
      v-model="isShownTaskModal"
      :task="taskToEdit"
      @save-edited-task="saveEditedTask"
    ></EditTaskModal>
  </div>
</template>

<script>
import { VueDraggableNext } from 'vue-draggable-next'
import EditTaskModal from '@/components/board/EditTaskModal'

export default {
  name: 'Home',
  display: 'Two Lists',
  order: 1,
  components: {
    draggable: VueDraggableNext,
    EditTaskModal,
  },
  data() {
    return {
      tasks1: [
        { id: 1, title: 'Tarea1', description: '' },
        { id: 2, title: 'Tarea2', description: '' },
      ],
      tasks2: [{ id: 3, title: 'Tarea3', description: '' }],
      title1: '',
      title2: '',
      isShownTaskModal: false,
    }
  },
  methods: {
    // Tasks1
    addTask1() {
      this.tasks1.push({ title: this.title1, id: this.nextTaskId() })
      this.title1 = ''
    },
    editTask1(id) {
      const index = this.tasks1.findIndex(task => task.id === id)
      this.taskToEdit = this.tasks1[index]
      this.isShownTaskModal = true
    },
    deleteTask1(id) {
      const index = this.tasks1.findIndex(task => task.id === id)
      this.tasks1.splice(index, 1)
    },

    // Tasks2
    addTask2() {
      this.tasks2.push({ title: this.title2, id: this.nextTaskId() })
      this.title2 = ''
    },
    editTask2(id) {
      const index = this.tasks2.findIndex(task => task.id === id)
      this.taskToEdit = this.tasks2[index]
      this.isShownTaskModal = true
    },
    deleteTask2(id) {
      const index = this.tasks2.findIndex(task => task.id === id)
      this.tasks2.splice(index, 1)
    },

    // Common
    nextTaskId() {
      return (
        Math.max.apply(
          Math,
          this.tasks1.concat(this.tasks2).map(task => task.id)
        ) + 1
      )
    },
    closeModal() {
      this.taskToEdit = {}
      this.isShownTaskModal = false
    },
    saveEditedTask(id, task) {
      const index1 = this.tasks1.findIndex(task => task.id === id)
      const index2 = this.tasks2.findIndex(task => task.id === id)
      if (index1 !== -1) {
        this.tasks1[index1].description = task.description
      }
      if (index2 !== -1) {
        this.tasks2[index2].description = task.description
      }
      this.closeModal()
    },
  },
}
</script>

<style lang="scss" scoped>
h3 {
  color: #37474f;
  text-align: left;
  margin: 1.5rem;

  span {
    color: #546e7a;
  }
}

.container {
  text-align: left;
  box-sizing: border-box;
  align-items: flex-start;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;
}

.column {
  box-sizing: border-box;
  background-color: #eceff1;
  border-radius: 3px;
  box-shadow: 0 0 0 0.5px rgba(49, 49, 93, 0.03),
    0 2px 5px 0 rgba(49, 49, 93, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.08);
  margin: 1rem;
  padding: 1rem;
  width: 100%;

  @media screen and (min-width: 600px) {
    width: calc(50% - 2rem - 2px);
  }
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fafafa;
  border-radius: 3px;
  border-bottom: 1px solid #ccc;
  margin: 0.25rem 0;
  padding: 1rem;

  .edit-button {
    background-color: transparent;
    border: none;
  }
}

input {
  box-sizing: border-box;
  background-color: #eceff1;
  border: none;
  border-radius: 3px;
  font-size: 1rem;
  margin: 0.5rem;
  outline: 0;
  padding: 0.75rem 0;
  transition: background-color 600ms ease;
  width: 100%;

  &:focus,
  &:active {
    background-color: #fafafa;
    border-bottom: 1px solid #ccc;
    margin: 0.25rem 0;
    padding: 1rem;
  }

  &::placeholder {
    color: #90a4ae;
  }
}
</style>

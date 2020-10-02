<template>
  <div
    :modelValue="isShownTaskModal"
    @update:modelValue="isShownTaskModal = $event"
    id="myModal"
    class="modal"
  >
    <div class="modal-content">
      <i class="close-icon material-icons" @click="closeModal()">close</i>
      <h2>{{ task.title }}</h2>
      <textarea
        class="textarea"
        rows="10"
        placeholder="Add a description..."
        v-model="descriptionToEdit"
      />
      <div class="button-container">
        <button @click="saveEditedTask(task.id, task)">Save</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'EditTaskModal',
  props: {
    modelValue: {
      type: String,
    },
    task: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isShownTaskModal: false,
      descriptionToEdit: '',
    }
  },
  created() {
    this.descriptionToEdit = this.task.description
  },
  methods: {
    saveEditedTask(id, task) {
      this.$emit('save-edited-task', id, {
        ...task,
        description: this.descriptionToEdit,
      })
    },
    closeModal() {
      this.$emit('update:modelValue', false)
    },
  },
}
</script>

<style lang="scss" scoped>
.modal-content {
  background-color: white;
  width: calc(100% - 2rem - 2px);
  padding: 10px 20px;
  margin: 20% auto;
  position: relative;

  .close-icon {
    position: absolute;
    top: 8px;
    right: 8px;
    cursor: pointer;
    display: flex;
  }

  @media screen and (min-width: 600px) {
    width: calc(50% - 2rem - 2px);
  }
}

.modal {
  background-color: rgba(0, 0, 0, 0.8);
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  opacity: 1;
  pointer-events: auto;
  transition: all 0.5s;
}

.textarea {
  width: 100%;
}

.button-container {
  display: flex;
  justify-content: center;

  button {
    cursor: pointer;
    border: seagreen;
    background-color: rgb(127, 206, 161);
    font-weight: bold;
    margin-top: 15px;
    margin-bottom: 5px;
    width: 50%;
    height: 30px;
    text-align: center;
  }
}
</style>

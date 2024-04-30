<template>
  <div class="add-task-bar">
    <span class="add-plus" id="add-task">+</span>
    <input
      class="add-task-input"
      type="text"
      :placeholder="'Add New Task'"
      @focus="$emit('focus');"
      @blur="$emit('blue')"
      @input="$emit('task-name', this.taskName)"
      v-model="taskName"
    />
  </div>
</template>

<script>
export default {
  name: "AddTaskBar",
  emits: ["focus", "blue", "task-name"],
  props: {
    newTaskName: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      taskName: "",
    };
  },
  watch: {
    newTaskName(newValue, oldValue) {
      if (newValue !== oldValue) {
        this.taskName = newValue;
      }
    },
  },
  methods: {
  },
};
</script>

<style scoped>
/* outer div */
.add-task-bar {
  cursor: text;
  margin: 5px 10px;
  padding: 5px 15px;
  max-width: 100%;
  transition: border-color 0.3s ease;
  position: relative;
  overflow: hidden;
}

.add-task-bar::after {
  content: "";
  display: block;
  position: absolute;
  left: 50%;
  width: 0%;
  height: 2px;
  background-color: #333;
  transition: width 0.3s ease;
  transform: translateX(-50%);
}

.add-task-bar:hover::after {
  width: calc(100% - 30px);
}

/* input box */
.add-task-input {
  vertical-align: middle;
  width: 90%;
  border: none;
}

.add-task-input:focus {
  outline: none;
}

/* plus sign */
.add-plus {
  vertical-align: middle;
  font-size: 23px;
  font-weight: 500;
  margin-right: 22px;
  margin-left: 3px;
  margin-top: -2px;
}
</style>

<template>
  <div class="detail-info-bar">
    <h4 class="task-h4">Task:</h4>
    <div class="main-task">
      <input
        type="text"
        :placeholder="'Add New Task'"
        v-model="this.localTaskName"
        @input="$emit('detail-bar-taskName', this.localTaskName)"
      />
      <textarea
        name=""
        id=""
        cols="30"
        rows="10"
        :placeholder="'Description'"
        v-model="this.localTaskDescription"
      ></textarea>
      
      <div class="tags">
        <label class="tags-label" for="tags">Tags: </label>
        <select class="tags-select" name="tags" id="tags">
          <option v-for="(_, tag) in this.tags" :key="tag" :value="tag">{{ tag }}</option>
        </select>
      </div>
      
      <label for="due-date">Due date: </label>
      <section>
        <date-picker
          v-model:value="time"
          type="datetime"
          placeholder="Select datetime"
          :show-time-panel="showTimePanel"
          @close="this.showTimePanel = false"
        >
          <template #footer>
            <button
              class="mx-btn mx-btn-text"
              @click="this.showTimePanel = !this.showTimePanel"
            >
              {{ showTimePanel ? "select date" : "select time" }}
            </button>
          </template>
        </date-picker>
      </section>
      <p>{{ this.time }}</p>
    </div>

    <div class="sub-task">
      <span>Subtasks:</span>
      <span>...</span>
    </div>
  </div>
</template>

<script>
import DatePicker from "vue-datepicker-next";
import "vue-datepicker-next/index.css";
import tasksData from "../assets/userData.json";
export default {
  name: "DetailInfoBar",
  emits: ["detail-bar-taskName"],
  components: {
    DatePicker,
  },
  props: {
    taskName: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      localTaskName: "",
      localTaskDescription: "",
      time: null,
      showTimePanel: false,
      tags: tasksData["tag-list"],
    };
  },
  watch: {
    taskName(newValue) {
      this.localTaskName = newValue;
    },
  },
};
</script>

<style scoped>
.task-h4 {
  font-weight: bolder;
}

.detail-info-bar {
  font-weight: bolder;
  flex-grow: 1;
  min-width: 50%;
  padding: 10px 20px;
  background: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.main-task input,
.main-task textarea {
  width: 90%;
  border: none;
  padding: 8px;
  border-radius: 8px;
  background-color: #ffffff;
  transition: background-color 0.3s ease;
}

.main-task input:focus,
.main-task textarea:focus,
.main-task input:hover,
.main-task textarea:hover {
  background-color: #f0f0f0;
  outline: none;
}

.tags {
  display: flex;
  align-items: center;
}

.tags-label {
  font-weight: bolder;
}

.tags-select {
  margin-left: 5%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  background: transparent;
  transition: background-color 0.3s ease;
}

.tags-select:hover {
  background-color: #f0f0f0;
}

.main-task label {
  display: block;
  margin: 5px 0;
  color: #333;
  font-size: 14px;
}
</style>

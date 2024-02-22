<template>
  <div id="app">
    <div class="wrapper">
      <Sidebar :handle-menu-item-click="handleMenuItemClick" />
      <TodoList
        v-if="currentView === 'today'"
        listName="Today"
        :tasks="tasksForDate(today)"
      />
      <TodoList
        v-if="currentView === 'upcoming'"
        listName="Upcoming"
        :tasks="tasksNotForDate(today)"
      />
    </div>
  </div>
</template>

<script>
import Sidebar from "./components/Sidebar.vue";
import TodoList from "./components/TodoList.vue";
import tasksData from "@/assets/userData.json";

export default {
  name: "App",
  components: {
    Sidebar,
    TodoList,
  },
  data() {
    return {
      currentView: "Today",
      tasksByDate: tasksData["tasks"],
      today: "",
    };
  },
  mounted() {
    this.getTodayDate();
  },
  methods: {
    handleMenuItemClick(action) {
      if (action === "today") {
        this.currentView = "today";
        console.log("Showing tasks...");
      } else if (action === "upcoming") {
        this.currentView = "upcoming";
      }
    },
    getTodayDate() {
      const now = new Date();
      const year = now.getFullYear().toString().slice(-2);
      const month = (now.getMonth() + 1).toString().padStart(2, "0");
      const day = now.getDate().toString().padStart(2, "0");
      this.today = `${year}-${month}-${day}`;
    },
    tasksForDate(date) {
      return this.tasksByDate.filter((tasksByDate) => tasksByDate.date <= date);
    },
    tasksNotForDate(date) {
      return this.tasksByDate.filter((tasksByDate) => tasksByDate.date > date);
    },
  },
};
</script>

<style>
#app {
  font-family: "Comic Sans MS", cursive;
  display: flex;
  height: 100vh;
}

.wrapper {
  display: flex;
  flex: 1;
}

/* You can add global styles here */
</style>

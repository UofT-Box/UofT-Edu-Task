<template>
  <div class="todo-list">
    <div class="header">
      <h2 class="header-title">{{listName}}</h2>
      <span class="header-divider">|</span>
      <span class="task-count">{{ tasks.length }}</span>
    </div>
    <div class="task-list">
      <li class="add-task-btn"><span class="add-plus">+</span>Add New Task</li>
      <ul>
        <li v-for="task in tasks" :key="task.id" class="task-item">
          <div class="task-details">
            <label class="custom-checkbox">
              <input type="checkbox" class="actual-checkbox" />
              <span class="checkbox-indicator"></span>
            </label>
            <span class="task-title">{{ task.title }}</span>
            <span class="nav-arrow">></span>
          </div>
          <div class="task-meta">
            <span class="task-date" v-if="task.date"
              ><img src="/images/date.svg" class="task-img" />{{
                task.date
              }}</span
            >
            <span class="subtask-count" v-if="task.subtasks.length">
              <span class="subtask-count-text">
                <span class="background">{{ task.subtasks.length }}</span>
                Subtasks
              </span>
            </span>
            <span class="tags" v-if="task.tags.length">
              <span class="tag" v-for="tag in task.tags" :key="tag">
                <span class="tag-color" :style="{ backgroundColor: getTagColor(tag) }"></span>
                <!-- 颜色方块 -->
                <span class="tag-name">{{ tag }}</span>
                <!-- 标签名称 -->
              </span>
            </span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  data() {
    return {
      tagsColors: {
        "Work": "#ffadad",
        "Urgent": "#ffd6a5",
        "Personal": "#fdffb6",
        "Networking": "#caffbf"
      },
    };
  },
  methods: {
    getTagColor(tag) {
      return this.tagsColors[tag] || '#dddddd';
    }
  },
  props:{
    listName: String,
    tasks: Array,
  }
};
</script>

<style scoped>
.todo-list {
  min-width: 800px;
  margin: 0 auto; /* 居中显示 */
  padding: 0px 20px 15px 25px; /* 上10px，右20px，下15px，左25px */
  background: white; /* 背景色 */
  border-radius: 8px; /* 圆角 */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* 轻微的阴影效果 */
}

.header {
  display: flex; /* 使用flex布局使元素水平排列 */
  align-items: center; /* 垂直居中对齐子元素 */
  font-size: 24px; /* 设置字体大小，可以根据需要调整 */
  font-weight: bold; /* 加粗字体 */
  color: #333; /* 字体颜色 */
  padding: 0px;
}

.header-title {
  margin-right: 18px; /* 在标题和分隔符之间添加一些空间 */
}

.header-divider {
  margin-right: 8px; /* 在分隔符和计数器之间添加一些空间 */
  color: #d6d5d5; /* 分隔符颜色，可以根据需要调整 */
  font-size: 60px;
  font-weight: 100;
}

.header h2 {
  font-size: 50px; /* 标题字体大小 */
  font-weight: bold; /* 标题字体加粗 */
  color: #333; /* 标题字体颜色 */
}

.header .task-count {
  color: rgb(9, 6, 6); /* 计数字体颜色 */
  padding: 5px 10px; /* 计数内边距 */
  border-radius: 15px; /* 圆形背景 */
  font-weight: 300;
  font-size: 50px; /* 计数字体大小 */
}

.add-task-btn {
    margin-left: -20px;
}

.add-plus {
    font-size: 23px;
    font-weight: 500;
    margin-right: 17px;
    margin-top: -2px;
}

.tasks {
  list-style-type: none; /* 移除列表标记 */
  padding: 0; /* 移除内边距 */
}

.task-item {
  align-items: start;
  flex-direction: column;
  justify-content: space-between;
  padding: 10px 0;
  border-top: 1px solid #eee; /* 添加底部边框作为分隔线 */
  text-align: left;
}

.tasks li {
  border-bottom: 1px solid #eee; /* 项目之间的分隔线 */
  padding: 15px 0; /* 项目的内边距 */
  display: flex; /* 采用flex布局 */
  align-items: center; /* 垂直居中 */
  justify-content: space-between; /* 内容分布在两端 */
}

.actual-checkbox {
  display: none;
}

.custom-checkbox {
  display: inline-block;
  position: relative;
  padding-left: 25px; /* 留出空间放置自定义的复选框指示器 */
  cursor: pointer;
  user-select: none; /* 防止选中标签文本 */
  margin-right: 10px;
}

.custom-checkbox .checkbox-indicator::before {
  content: "";
  position: absolute;
  left: 0;
  top: -5px;
  transform: translateY(-50%);
  width: 16px;
  height: 16px;
  background: white;
  border: 2px solid #ccc;
  border-radius: 5px;
}

.actual-checkbox:checked + .checkbox-indicator::before {
  background: #4a90e2;
}

.actual-checkbox:checked + .checkbox-indicator::after {
  content: "";
  position: absolute;
  left: 4px;
  top: 50%;
  transform: translateY(-50%) scale(0.8);
  color: white;
  font-size: 14px;
}

.task-title {
  font-weight: 500;
  font-size: 16px;
  color: #333;
}

.task-details {
  width: 100%;
}

.nav-arrow {
  margin-left: auto;
}

.task-meta {
  margin-left: 34px;
  margin-top: 5px;
}

.task-meta span {
  margin-right: 10px;
}

.subtask-count-text .background {
  display: inline-block;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  padding: 1px 8px;
  border-radius: 3px;
  line-height: 1;
  font-size: 12px;
  margin-right: 2px;
  top: -5px;
  vertical-align: 2px;
}

.task-img {
  margin-top: -5px;
}
.subtasks-count,
.tags {
  font-size: 14px;
  color: #666;
}

.tag-color {
  display: inline-block;
  width: 16px;
  height: 16px;
  margin-right: 3px;
  border-radius: 5px;
  vertical-align: -1px;
}

.tags .tag {
  color: rgb(3, 3, 3);
  border-radius: 3px;
  padding: 2px 6px;
  margin-right: 5px;
}

.tag-name{
    font-size: 16px;
}
</style>

<template>
  <div class="sidebar">
    <!-- 顶部菜单行 -->
    <div class="menu-header">
      <span class="menu-title">Menu</span>
      <!-- <img src="/images/menu.svg" class="menu-icon" alt="menu" /> -->
    </div>
    <!-- 搜索栏 -->
    <div class="search-bar">
      <img src="/images/search-icon.svg" class="search-icon" alt="Search" />
      <input
        type="text"
        placeholder="Search..."
        @input="handleSearchInput"
      />
    </div>
    <!-- 菜单项 -->
    <div class="menu-section-list">
      <div v-for="menu in menus" :key="menu.title" class="menu-section">
        <menu-items
          :title="menu.title"
          :items="menu.items"
          :handleMenuItemClick="handleMenuItemClick"
        >
          <!-- 定义插槽内容 -->
          <template v-slot:default="{ item }">
            <!-- 用于显示图标的地方 -->
            <img v-if="item.icon" :src="getIconPath(item.icon)" alt="Icon" />
          </template>
        </menu-items>
      </div>
    </div>

    <!-- 底部设置区域 -->
    <div class="sidebar-footer">
      <div class="settings-item"><img src="/images/setting.svg" />Settings</div>
      <div class="signout-item"><img src="/images/sign-out.svg" />Sign out</div>
    </div>
  </div>
</template>

<script>
import MenuItems from "./MenuItems.vue";

export default {
  name: "SidebarMenu",
  components: {
    MenuItems,
  },
  data() {
    return {
      menus: [
        {
          title: "TASKS",
          items: [
            {
              text: "Upcoming",
              icon: "upcoming",
              count: 12,
              isColorBlock: false,
            },
            { text: "Today", icon: "today", count: 5, isColorBlock: false },
            {
              text: "Calendar",
              icon: "calendar",
              count: 0,
              isColorBlock: false,
            },
            { text: "KanBan", icon: "kanban", count: 0, isColorBlock: false },
          ],
        },
        {
          title: "My Lists",
          items: [
            { text: "CSC 165", icon: "#ff8737", count: 4, isColorBlock: true },
            { text: "CSC 148", icon: "#ff6262", count: 0, isColorBlock: true },
          ],
        },
      ],
    };
  },
  props: {
    handleMenuItemClick: Function,
  },
  methods: {
    menuItemClicked(action) {
      if (this.handleMenuItemClick) {
        this.handleMenuItemClick(action);
      }
    },
    getIconPath(iconName) {
      return `${iconName}.svg`;
    },
  },
};
</script>

<style scoped>
.sidebar {
  width: 250px;
  background-color: #ffffff;
  height: 100vh;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.menu-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

.menu-title {
  font-size: 24px;
  font-weight: bold;
}

.menu-icon {
  width: 24px;
  height: 100%;
}

.search-bar {
  margin-left: 8px;
  margin-right: 8px; /* 对齐 */
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  padding: 0 20px;
}

.search-icon {
  width: 16px; /* 或根据您的设计调整 */
  margin-right: 10px;
}

input[type="text"] {
  width: 100%;
  height: 70%;
  padding: 10px;
  border: none;
  /* box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1); */
  outline: none;
  border: 1px solid #e7e7e7;
  border-radius: 8px; /* 给搜索框添加边框 */
}

.menu-section-list {
  flex-grow: 2;
}

.menu-section {
  flex-grow: 1;
  margin-bottom: 20px;
  border-top: 1px solid #e7e7e7; /* 给每个menu-section划区 */
  padding-top: 10px;
}

.sidebar-footer {
  padding: 20px;
  background-color: #f3f3f3;
  text-align: center;
}

.settings-item,
.signout-item {
  cursor: pointer;
  padding: 10px;
  border-top: 1px solid #e7e7e7;
}

.settings-item:hover,
.signout-item:hover {
  background-color: #e7e7e7;
}

.sidebar-footer img {
  margin-right: 10px;
  width: 20px;
  height: 20px;
}
</style>

<template>
  <div class="menu-items">
    <div class="menu-subtitle">{{ title }}</div>
    <ul>
      <li
        v-for="item in items"
        :key="item.text"
        @click="callChangeEvent(item.icon)"
      >
        <img
          v-if="!item.isColorBlock"
          :src="'./images/' + item.icon + '.svg'"
        />
        <div
          v-else
          class="color-block"
          :style="{ backgroundColor: item.icon }"
        ></div>
        {{ item.text }}
        <span class="badge" v-if="item.count">{{ item.count }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MenuItems",
  props: {
    title: String,
    items: Array,
    handleMenuItemClick: Function,
  },
  methods: {
    callChangeEvent(icon) {
      if (this.handleMenuItemClick) {
        this.handleMenuItemClick(icon);
      }
    },
  },
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

li {
  cursor: pointer;
  padding: 10px 20px;
  border-left: 5px solid transparent;
  display: flex;
  align-items: center;
  /* font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif; */
  font-size: 16px;
  color: #333;
  transition: background-color 0.3s, border-left-color 0.3s;
}

li:hover {
  background-color: #e7e7e7;
  border-left: 5px solid #4a90e2;
}

li img {
  margin-right: 10px;
  width: 20px;
  height: 20px;
}

li.active {
  background-color: #4a90e2;
  color: white;
}

.badge {
  margin-left: auto;
  background-color: #f08e8e;
  color: white;
  border-radius: 10px;
  padding: 2px 8px;
  font-size: 12px;
  line-height: 1;
}

ul {
  list-style: none;
}

.menu-subtitle {
  padding-left: 20px;
  font-weight: bold;
}

.color-block {
  width: 16px;
  height: 16px;
  border-radius: 5px;
  margin-right: 10px;
}

@media (max-width: 600px) {
  li {
    padding: 10px 15px;
    font-size: 14px;
  }
}
</style>

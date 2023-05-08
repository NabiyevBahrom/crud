<template>
  <div id="demo"></div>
  <form>
    <h3>Create New Item</h3>
    <label for="name">Name</label>
    <input type="text" id="name" v-model="newItemName" />
    <label for="todo">Todo</label>
    <input id="todo" v-model="newItemTodo" />
    <label for="time">Time</label>
    <input type="date" id="time" v-model="newItemTime" />
    <button type="button" class="btn" @click="addItem">Add Item</button>
  </form>

  <div class="boxtodo">
    <div class="boxhead">
      <ul>
        <li>ism</li>
        <li>berilgan&nbsp;vazifa</li>
        <li>tugash&nbsp;vaqti</li>
        <li>yangilash</li>
        <li>o`chirish</li>
      </ul>
    </div>
    <div class="boxtodotwo">
      <ol v-for="item in items" :key="item.id">
        <div class="boxtwo">
          <div class="textbox">{{ item.name }}</div>
          <div class="textbox">{{ item.todo }}</div>
          <div class="textbox">{{ item.time }}</div>
          <div style="display: flex; justify-content: space-between">
            <button
              style="margin-right: 30px"
              type="button"
              @click="editItem(item)"
            >
              Edit</button
            ><button type="button" @click="deleteItem(item)">Delete</button>
          </div>
        </div>
      </ol>
    </div>
  </div>

  <form v-if="selectedItem">
    <h3>Yangilash</h3>
    <label for="name">ism:</label>
    <input type="text" id="name" v-model="selectedItem.name" />
    <label for="todo">vazifa</label>
    <input type="text" id="todo" v-model="selectedItem.description" />
    <label for="Time">vaqt</label>
    <input type="text" id="Time" v-model="selectedItem.time" />
    <button type="button" @click="updateItem">Yangilash</button>
    <button type="button" @click="resetForm">Bekor qilish</button>
  </form>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      items: [],
      newItemName: "",
      newItemTodo: "",
      newItemTime: "",
      selectedItem: null,
    };
  },

  mounted() {},

  methods: {
    addItem: function () {
      var item = {
        name: this.newItemName,
        todo: this.newItemTodo,
        time: this.newItemTime,
      };
      this.items.push(item);
      this.newItemName = "";
      this.newItemTodo = "";
      this.newItemTime = "";
    },
    editItem: function (item) {
      this.selectedItem = item;
      document.getElementById("demo").innerHTML = "yangilash";
    },
    updateItem: function () {
      this.selectedItem = null;
      document.getElementById("demo").innerHTML = "yangilandi";
    },
    deleteItem: function (item) {
      var index = this.items.indexOf(item);
      if (index !== -1) {
        this.items.splice(index, 1);
      }
      document.getElementById("demo").innerHTML = "O`chirildi";
    },
    resetForm: function () {
      this.selectedItem = null;
    },
  },
};
</script>

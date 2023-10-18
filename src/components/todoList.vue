<template>
  <div id="todo">
    <main>
      <header>
        <h1>T O D O</h1>
        <img src="@/assets/images/icon-moon.svg" alt="theme-icon" />
      </header>
      <section>
        <input
          type="text"
          id="add-todo"
          placeholder="Create a new todo..."
          v-model="newTodo"
          @keyup.enter="addTodo"
        />
        <article>
          <div v-if="lists.length === 0">
            <p class="emptylist-message">You currently have no to-dos.</p>
          </div>
          <ul v-else>
            <li v-for="(list, index) in filteredLists" :key="index">
              <div class="todo-details">
                <input
                  type="checkbox"
                  id="option1"
                  name="options"
                  v-model="list.isChecked"
                />
                <label for="option" :class="{ cancelled: list.isChecked }">{{
                  list.label
                }}</label>
              </div>
              <img
                src="@/assets/images/icon-cross.svg"
                alt="delete-icon"
                id="icon-delete"
                v-on:click="deleteTodo(index)"
              />
            </li>
          </ul>
          <div id="footer">
            <p id="todo-left">{{quantity}} items left</p>
            <div class="filtering">
              <p
                v-on:click="toggleFilter('all')"
                :class="{ selected: filter === 'all' }"
              >
                All
              </p>
              <p
                v-on:click="toggleFilter('incomplete')"
                :class="{ selected: filter === 'incomplete' }"
              >
                Active
              </p>
              <p
                v-on:click="toggleFilter('completed')"
                :class="{ selected: filter === 'completed' }"
              >
                Completed
              </p>
            </div>
            <p
              id="todo-cleared"
              v-on:click="clearCompleted"
            >
              Clear Completed
            </p>
          </div>
        </article>
      </section>
      <div class="filter">
        <p
          v-on:click="toggleFilter('all')"
          :class="{ selected: filter === 'all' }"
        >
          All
        </p>
        <p
          v-on:click="toggleFilter('incomplete')"
          :class="{ selected: filter === 'incomplete' }"
        >
          Active
        </p>
        <p
          v-on:click="toggleFilter('completed')"
          :class="{ selected: filter === 'completed' }"
        >
          Completed
        </p>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      lists: [],
      newTodo: "",
      filter: "all",
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== "") {
        this.lists.push({
          label: this.newTodo,
          completed: false,
        });
        this.newTodo = "";
      }
    },
    deleteTodo(index) {
      this.lists.splice(index, 1);
    },
    toggleFilter(status){
     this.filter = status;
    },
    clearCompleted() {
      if (this.lists.length > 0) {
        this.lists = this.lists.filter((list) => !list.isChecked);
      }
    },
  },
  computed: {
    filteredLists() {
      if (this.filter === "all") {
        return this.lists;
      } else if (this.filter === "completed") {
        return this.lists.filter((list) => list.isChecked);
      } else if (this.filter === "incomplete") {
        return this.lists.filter((list) => !list.isChecked);
      }
      return this.lists;
    },
    quantity() {
      return this.lists.filter((list) => !list.isChecked).length;
    },
  },
};
</script>

<style scoped>
#todo {
  font-family: Josefin Sans;
}
header {
  margin: 0;
  align-items: center;
  display: flex;
  justify-content: space-between;
}
main {
  position: absolute;
  left: 37%;
  top: 100px;
}
@media (max-width: 768px) {
  main {
    left: 5%;
    top: 60px;
  }
}
h1 {
  color: white;
}
#add-todo {
  margin-bottom: 0.5rem;
  padding-left: 32px;
  padding-right: 280px;
  padding-top: 10px;
  padding-bottom: 10px;
  border-radius: 2px;
  border: none;
}
@media (max-width: 768px) {
  #add-todo {
    padding-bottom: 1rem;
    padding-top: 1rem;
    padding-right: 140px;
  }
}
input {
  outline: none;
}
input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 1px solid hsl(236, 33%, 92%);
  border-radius: 50%;
  cursor: pointer;
}

input[type="checkbox"]:checked {
  background-image: url("@/assets/images/icon-check.svg");
  background-color: blue;
}

input::placeholder {
  color: hsl(236, 9%, 61%);
}
.cancelled {
  text-decoration: line-through;
  color: hsl(234, 39%, 85%);
}
article {
  background: white;
  margin-top: 1rem;
  box-shadow: 0px 0px 2px hsl(234, 11%, 52%);
}
li {
  position: relative;
  list-style-type: none;
  margin-left: -2.5rem;
  padding-bottom: 0.7rem;
  padding-top: 0.7rem;
  border-bottom: 1px solid hsl(236, 33%, 92%);
  color: hsl(235, 19%, 35%);
  font-size: 14px;
}
@media (max-width: 768px) {
  li {
    padding-bottom: 1.2rem;
    padding-top: 1.2rem;
  }
}
.emptylist-message {
  color: hsl(235, 19%, 35%);
  padding-top: 1rem;
  padding-bottom: 0.5rem;
  margin-left: -2.5rem;
  text-align: center;
}
.todo-details {
  display: flex;
  gap: 10px;
  align-items: center;
  padding-left: 8px;
}
@media (max-width: 768px) {
  .todo-details {
    padding-left: 2px;
  }
}
#icon-delete {
  left: 26.5rem;
  position: absolute;
  top: 0.8rem;
  width: 16px;
  cursor: pointer;
}
@media (max-width: 768px) {
  #icon-delete {
    left: 17rem;
  }
}
#footer {
  display: flex;
  gap: 60px;
  padding-left: 18px;
  margin-top: -1.2rem;
  font-size: 14px;
  padding-right: 4px;
}
@media (max-width: 768px) {
  #footer {
    gap: 0;
    padding-left: 4px;
    padding-right: 0;
  }
}
.filtering {
  display: flex;
  gap: 8px;
  color: hsl(234, 11%, 52%);
  cursor: pointer;
}
.selected {
  color: blue;
}
@media (max-width: 768px) {
  .filtering {
    visibility: hidden;
  }
}
#todo-left {
  color: hsl(234, 39%, 85%);
}
#todo-cleared {
  color: hsl(234, 39%, 85%);
  cursor: pointer;
}
@media (max-width: 768px) {
  #todo-cleared {
    padding-right: 8px;
  }
}
.filter {
  display: flex;
  justify-content: center;
  gap: 18px;
  align-items: center;
  color: hsl(234, 11%, 52%);
  cursor: pointer;
  padding-left: 2rem;
  visibility: hidden;
  background: white;
  margin-top: 1rem;
  box-shadow: 0px 0px 2px hsl(234, 11%, 52%);
}
@media (max-width: 768px) {
  .filter {
    visibility: visible;
  }
}
.disabled {
  cursor: not-allowed;
}
</style>

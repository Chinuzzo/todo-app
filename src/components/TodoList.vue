<template>
  <div>
    <p class="ui basic content center aligned segment">
      Totaal openstaande todos: {{ amountOfOpenTodos }}
    </p>
    <div class="ui basic content center aligned segment">
      <input type="checkbox" v-model="checkedTodo" />
      <input type="text" v-model="inputToSearch" />
    </div>
    <todo-list-item
      v-for="todo in searchTodos"
      :todo="todo"
      :key="todo.id"
      @delete-todo="deleteTodo"
      @complete-todo="completeTodo"
    />
  </div>
</template>

<script>
import TodoListItem from '@/components/todo/TodoListItem';

export default {
  name: 'TodoList',
  components: { TodoListItem },
  props: ['todos'],
  data() {
    return {
      checkedTodo: false,
      inputToSearch: '',
    };
  },
  computed: {
    searchTodos() {
      return this.filteredTodos.filter((todo) =>
        todo.title.toLowerCase().includes(this.inputToSearch.toLowerCase())
      );
    },
    // alle gefilterde todos
    filteredTodos() {
      if (this.checkedTodo) {
        return this.todos.filter((todo) => !todo.done);
      }
      return this.todos;
    },
    // aantal todos met de status open
    amountOfOpenTodos() {
      return this.todos.filter((todo) => !todo.done).length;
    },
  },
  methods: {
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
    },
    deleteTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
  },
};
</script>

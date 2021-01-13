<template>
    <div class='ui centered card'>
        <div class="content" v-show="!isEditing">
            <div class='header'>
                {{ todo.title }}
            </div>
            <div class='meta'>
                {{ todo.project }}
            </div>
            <div class='extra content'>
                <span class='right floated edit icon' @click="showForm">
                    <button class="ui button small blue"><i class='edit icon'></i></button>
                </span>
                <span class='right floated trash icon' @click="deleteTodo(todo)">
                    <button class="ui button small orange"><i class='trash icon'></i></button>
                </span>
            </div>
        </div>
        <div class="content" v-show="isEditing">
            <div class='ui form'>
                <div class='field'>
                    <label>Titel</label>
                    <input type='text' v-model="todo.title" >
                </div>
                <div class='field'>
                    <label>Project</label>
                    <input type='text' v-model="todo.project" >
                </div>
                <div class='ui two button attached buttons'>
                    <button class='ui basic blue button' @click="hideForm">
                        Sluiten
                    </button>
                </div>
            </div>
        </div>
        <div class='ui bottom attached green basic button' v-show="!isEditing &&todo.done" disabled>
            Voltooid
        </div>
        <div class='ui bottom attached red basic button' v-show="!isEditing && !todo.done" @click="completeTodo(todo)">
            Lopend
        </div>
    </div>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    completeTodo (todo) {
      this.$emit('complete-todo', todo)
    },
    deleteTodo (todo) {
      this.$emit('delete-todo', todo)
    },
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    }
  }
}
</script>

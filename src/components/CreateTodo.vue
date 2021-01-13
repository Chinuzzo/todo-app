<template>
    <div class='ui basic content center aligned segment'>
        <button class='ui basic button icon' @click="openForm" v-show="!isCreating">
            <i class='plus icon'></i>
        </button>
        <div class='ui centered card' v-show="isCreating">
            <div class='content'>
                <div class='ui form'>
                    <div class='field'>
                        <label>Titel</label>
                        <input v-model="titleText" type='text' ref='title'>
                    </div>
                    <div class='field'>
                        <label>Project</label>
                        <input type='text' v-model="projectText" ref='project'>
                    </div>
                    <div class='ui two button attached buttons'>
                        <button class='ui basic blue button' @click="sendForm">
                            Aanmaken
                        </button>
                        <button class='ui basic red button' @click="closeForm">
                            Annuleren
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'CreateTodo',
  data () {
    return {
      titleText: '',
      projectText: '',
      isCreating: false
    }
  },
  methods: {
    openForm () {
      this.isCreating = true
    },
    closeForm () {
      this.isCreating = false
    },
    sendForm (todo) {
      if (this.titleText.length > 0 && this.projectText.length > 0) {
        const title = this.titleText
        const project = this.projectText
        this.$emit('create-todo', title, project, todo)
      }
      this.isCreating = false
    }
  }
}
</script>

<template>
  <div class="ui centerd card">
    <!-- shows when in view mode -->
    <div class="contenet" v-show="!isEditing">
      <div class="content">
        <div class="hearder">
          {{ todo.title | capitalize }}
        </div>
        <div class="meta">
          {{ todo.project }}
        </div>
        <div class="extra content">
          <span class="right floated edit icon" v-on:click="showForm">
            <i class="edit icon"></i>
          </span>
          <span class="right floated edit icon" v-on:click="deleteTodo(todo)">
            <i class="trash icon"></i>
          </span>
        </div>
      </div>
    </div>
  
    <!-- show editing form -->
    <div class="content" v-show="isEditing">
      <div class="ui form">
        <div class="field">
          <label for="">Title</label>
          <input type="text" v-model="todo.title">
        </div>
        <div class="field">
          <label for="">Project</label>
          <input type="text" v-model="todo.project">
        </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>
  
    <div class='ui bottom attached green basic button' v-show="!isEditing && todo.done" disabled>
      Completed
    </div>
    <div class='ui bottom attached red basic button' v-show="!isEditing && ! todo.done">
      Pending
    </div>
  
  </div>
</template>


<script>
export default {
  props: ['todo'],
  data () {
    return {
      isEditing: false
    }
  },
  methods: {
    showForm () {
      this.isEditing = true
    },
    hideForm () {
      this.isEditing = false
    },
    deleteTodo (todo) {
      this.$emit('delete-todo', todo)
    }
  },
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
}
</script>


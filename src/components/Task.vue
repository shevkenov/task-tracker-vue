<template>
  <div @dblclick="toggleReminder(task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>{{ task.text }} 
        <i @click="deleteTask(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{task.day}}</p>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: Object,
  },
  methods: {
      deleteTask(id){
          this.$emit('delete-task', id);
      },
      toggleReminder(id){
          this.$emit('toggle-reminder', id);
      }
  }
};
</script>

<style scoped>
.fas {
    color: red
}
.task {
    background: #f4f4f4;
    margin: 5px;
    padding: 10px 20px;
    cursor: pointer;
}
.task h3{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.task.reminder{
    border-left: green 3px solid;
}
</style>
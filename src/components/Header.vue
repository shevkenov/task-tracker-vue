<template>
  <header>
    <h1>Task tracker</h1>
    <Button
      v-show="homePage"
      @show-form="$emit('show-form')" 
      :text="showForm ? 'Close' : 'Add task'" 
      :color="showForm ? 'red' : 'green'"
      />
  </header>
</template>

<script>
import Button from './Button';

export default {
  components: { Button },
  name: "Header",
  props: {
    showForm: Boolean
  },
  computed: {
    homePage(){
      if(this.$route.path === '/'){
        return true;
      }else{
        return false;
      }
    }
  }
};
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>
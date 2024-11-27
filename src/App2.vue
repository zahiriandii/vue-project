<script setup>
 import {ref,onMounted} from 'vue';

  const name = ref('Andi Zahiri');
  const status = ref('active');
  const tasks = ref(['Task One' , 'Task two' , 'Task Three']);
  const newTask = ref('');

  const changeStatus = () =>
    {
      if (status.value === 'active')
        {
          status.value = 'inActive';
        }
        else if (status.value === 'inActive')
        {
          status.value = 'Pending';
        }
        else{
          status.value = 'active'
        }
    };

    const addNewTask = () =>
    {
      if (newTask.value.trim() !== '')
        {
          tasks.value.push(newTask.value);
          newTask.value = '';
        }
    };

    const deleteTask = (index) =>
    {
       tasks.value.splice(index, 1);
    };

    onMounted(async ()=> {
      try {
        const tasksFromWeb = await fetch ('https://jsonplaceholder.typicode.com/todos');
        const data = await tasksFromWeb.json();

        const titles = data.map(t => t.title);
        tasks.value = titles;
      } catch (error) {
        console.log('error while fetching the json file'); 
      }
    });
    
</script>

<template>
  <h1>{{ name }}</h1>
  <h5><p>User state is {{ status }} </p></h5>
  <button @click="changeStatus">Change Status</button>
  <h3>Add new task:</h3>
  <form @submit.prevent="addNewTask">
  <input type="text" id="newTask" v-model="newTask" name="newTask">
  <button type="submit">Add Task</button>
  </form>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task,index) in tasks">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>   


</template>



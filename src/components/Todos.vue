<template>
   <div class="hello">
  <ul>
    
    <li v-for="todo in todos" :key="todo.id">
    
     <p v-if="todo.completed == true"> <strong>Título do todo:</strong> {{ todo.title}}
     <ul>
           <li v-for="user in todo.users" :key="user.id">
              <p>Nome do usuário: {{ user.name}}</p> 
              <p> Username: {{ user.username }}</p> 
              <p> email: {{ user.email }}</p>
            </li>
            <hr>
            
        </ul>
         
     </p> 
    </li>
   
  </ul>
  </div>
</template>

<script>
 import api from "../services/api"

export default {
    name: 'Todos',
  
  data () {
    return {
      users: [],
      todos: [],
      }
  },

  async mounted (){
    const result = await api.get("/todos")
    this.todos = result.data;

     const result1 = await api.get("/users")
    this.users = result1.data;

    this.todos = result.data.map(todo => {
        return {
          ...todo,
          users: this.users.filter(user => user.id === todo.userId)
          
        }
      })

  }
  

}
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: list-item;
  margin: 0 10px;
}
</style>

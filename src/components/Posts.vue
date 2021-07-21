<template>
  <div class="hello">
    
  <ul>
     <li v-for="post in posts" :key="post.id">
        <h3>Título do post: {{ post.title}}</h3> 
        <p>Corpo do post: {{ post.body}}</p>
         
        <ul>
           <li v-for="comment in post.comments" :key="comment.id">
              <h3>Nome do comentário: {{ comment.name}}</h3> 
              <p> Corpo do comentário: {{ comment.body }}</p> 
              <p> email: {{ comment.email }}</p>
            </li>
        </ul>
        <ul>
          <li v-for="user in post.users" :key="user.id">
           <h3>Usuário</h3>
           <p>Nome: {{ user.name}}</p> 
           <p>Username: {{ user.username }}</p> 
           <p>email: {{ user.email }}</p> 
           
          </li>
        </ul>
        <hr>
     </li>
      
  </ul>
  
   
  </div>
</template>

<script>
import api from "../services/api"

export default {
  name: 'Posts',
 
  data() {
   return{
      posts: [],
      comments: [],
      users:[]

    }
  },
 async  mounted () {
      
      const result= await api.get("/posts");
      this.posts = result.data;

      const resul= await api.get("/comments");
      this.comments = resul.data;

      const resul1= await api.get("/users");
      this.users = resul1.data;
      
      this.posts = result.data.map(post => {
        return {
          ...post,
          comments: this.comments.filter(comment => comment.postId === post.id),
          users: this.users.filter(user => user.id === post.userId)
          
        }
      })
    
  }
}
</script>



<style scoped>
h3 {
  margin: 10px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}

</style>

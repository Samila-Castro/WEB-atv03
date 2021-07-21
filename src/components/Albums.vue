<template>
  <div class="hello">
    <ul>
      <li v-for="album in albums" :key="album.id">
        <h3>Título do album: {{ album.title}} </h3>
        <ul>
          <li v-for="user in album.users" :key="user.id">
            <h3>Informações do usuário: {{user.name}} - {{ user.username}}</h3>
            <ul>
              <li v-for="photo in album.photos" :key="photo.id">
    
               <div class="img"><img :src="photo.url" ></div>
     
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import api from "../services/api";

export default {
    name: "Albums",
    props: {
        msg: String,
    },
     data() {
   return{
      albums: [],
      photos: [],
      users: []
    }
  },
  async  mounted() {
        const result = await api.get("/albums");
        this.albums = await result.data;

        const result1 = await api.get("/users");
        this.users = await result1.data;

        const result2 = await api.get("/photos");
        this.photos = await result2.data;

         this.albums = result.data.map(album => {
        return {
          ...album,
          users: this.users.filter(user => user.id === album.userId),
          photos: this.photos.filter(photo => photo.albumId === album.id)
          
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
  margin: 5px 10px;
}

img{
  width: 120px;
  
}


</style>
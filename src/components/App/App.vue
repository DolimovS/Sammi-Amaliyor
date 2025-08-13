<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel :updateTermHandle="updateTermHandle" />
        <AppFilter  :filterName="filter" :updateFilterHandler="updateFilterHandler"/>
      </div>
      <Box v-if="!movies.length && !isloading" >
        <p  class="text-center fs-3 text-danger"  >Kinolar yo'q :(</p>
       </Box>
       <Box v-if="isloading" > 
        <p  class="text-center fs-3 "  >Loading...</p>
       </Box>
      <MovieList 
      v-else
      :movies="onFilterHandler(onSearchHendler(movies,term),filter )" 
      @onToggle="onToggleHandler" 
      @onRemove="onRemoveHendler" />
      <MovieAddForm @movieAdded="moviePush" />
    </div>
  </div>

</template>


<script>
import axios from 'axios';
import AppFilter from '../app-filter/AppFilter.vue';
import AppInfo from '../app-info/Appinfo.vue';
import MovieAddForm from '../movie-add-form/MovieAddForm.vue';
import MovieList from '../movie-list/MovieList.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';
import Box from '../../ui-components/Box.vue';
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
    Box,

  },
  data() {
    return {
      movies: [],
      term:'',
      filter:'all',
      isloading:false,
    }
  },

  methods: {
    moviePush(item) {
      this.movies.push(item);
    },
    onToggleHandler({id,prop}) {
      console.log(prop);
      
      this.movies= this.movies.map(item => {
        console.log(item);
        
        if (item.id == id) {
          return {...item,[prop]:!item[prop] }

          }
        return item
      })
    },
    onRemoveHendler(id){
      this.movies=this.movies.filter(item=>item.id!=id)
    },
    onSearchHendler(arr, term){
      if(term.length==0){
        return arr
      }
      return arr.filter(c=>c.name.toLowerCase().indexOf(term)>-1)
    },
    updateTermHandle(term){
      this.term=term
    },
    onFilterHandler(arr,filter){
      switch(filter){
        case "popular":
          return arr.filter(c=> c.like)
        case "mostWiewers":
          return arr.filter(s=>s.viewers>500)

          default:
            return arr
      }
    },
    updateFilterHandler(filter){
      this.filter=filter
    },
    async fatchMovie(){
      this.isloading=true;
      try{
       setTimeout(async()=>{
         const  {data}=await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=1")
        const newArr=data.map(item=>({
          id:item.id,
          name:item.title,
          like:false,
          favourite:false,
          viewers:item.id * 200,
        }))
        this.movies=newArr
        this.isloading=false
       },3000)
      }catch(error){
        alert(error.message);
      }
  
    }
  },
  mounted(){
    this.fatchMovie()
  }
}
</script>

<style scoped>
.app {
  height: 100vh;
  color: black;
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  margin-bottom: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
}
</style>
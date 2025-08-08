<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <div class="search-panel">
        <SearchPanel :updateTermHandle="updateTermHandle" />
        <AppFilter  :filterName="filter" :updateFilterHandler="updateFilterHandler"/>
      </div>
      <MovieList 
      :movies="onFilterHandler(onSearchHendler(movies,term),filter )" 
      @onToggle="onToggleHandler" 
      @onRemove="onRemoveHendler" />
      <MovieAddForm @movieAdded="moviePush" />
    </div>
  </div>
</template>


<script>
import AppFilter from '../app-filter/AppFilter.vue';
import AppInfo from '../app-info/Appinfo.vue';
import MovieAddForm from '../movie-add-form/MovieAddForm.vue';
import MovieList from '../movie-list/MovieList.vue';
import SearchPanel from '../search-panel/SearchPanel.vue';
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,

  },
  data() {
    return {
      movies: [
        {
          id: 1,
          name: 'Omar',
          viewers: 890,
          favourite: false,
          like: true,
        },
        {
          id: 2,
          name: 'Emoire of osman',
          viewers: 356,
          favourite: false,
          like: false,
        },
        {
          id: 3,
          name: 'Ertugrul',
          viewers: 494,
          favourite: true,
          like: false,
        }
      ],
      term:'',
      filter:'all',
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
    }

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
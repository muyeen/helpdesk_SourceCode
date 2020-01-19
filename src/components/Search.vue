<template>
  <div>
      <form 
      v-on:submit="$emit('search-run', searchKeyWord)"
      v-on:submit.prevent > 
      
        <input type="text" v-model="searchKeyWord" name="search" class="search-text" id="search-text" placeholder="User ID, Organization ID or Tiket ID">
        <input type="submit" value="Search">

      </form>
  </div>
</template>

<script>
export default {
    name: "Search",
    data (){
        return {
            searchKeyWord : ''
        }
    }
}
</script>

<style scoped>
  .search-text{
    width: 300px;
  }
</style>
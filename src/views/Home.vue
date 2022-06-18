<template>
  <div>    
      <section class="form-wrapp">
        <form v-on:submit.prevent="addSearch(search)">
          <input list="my-list" class="seach-field" type="text" v-model="search" placeholder='Search people...' @keyup="getAllStarWarsPeople">                  
          <datalist id="my-list" v-if="this.search">
              <option
                v-for="person in filteredPeople" :key="person.id"
              >
                {{ person.name }}</option>
          </datalist>
        </form>
        <Vue-button 
          class="search_btn"
          :PROPS_NAME="'Clean'" 
          :PROPS_ICON="'close'" 
          @click="clean()" 
          />  
      </section>
      <section>
        <Vue-history
          :PROPS_DATA ="searchData"
          :PROPS_TIME ="date"
        />
      </section>     
  </div>
</template>

<script>
import Button from '@/components/Button.vue';
import History from '@/components/History.vue';

export default {
   components: {
    "Vue-button": Button,
    "Vue-history": History,
  },

  data: function () {
    return {
      people: [],
      search: "",      
      searchData:[],
      date:[],
      person:[],
      
      
    }
  },
  
  methods: {   
    getAllStarWarsPeople() {
      fetch("https://swapi.dev/api/people/")
        .then(response => response.json())
        .then(res => {
          this.people = res.results          
        });        
    },
    addSearch(value){
      this.date.push((new Date()).toLocaleString("en-US"));  
      for (let i = 0; i < this.people.length; i++){
        if(value === this.people[i].name){
           return this.searchData.push(this.people[i]); 
        }        
      }
        
      this.date.push((new Date()).toLocaleString("en-US"));           
      this.search=""     
    },
    clean(){
      this.search=""
    },
  },
  created() {
    this.getAllStarWarsPeople();
  },

  computed: {
    filteredPeople() {
      if (this.people) {
        return this.people.filter((person) => {            
          return person.name.match(this.search);
        });
      }
      return false;
    }
  }
} 
</script>

<style scoped>
  
  .seach-field{
    width: 100%;
    box-sizing: border-box;
    border-radius: 10px;
    line-height:34px;
    outline: none;
    color: #767676;
    background-color: #fff;
    background-image: none;
    border: 1px solid #ccc;
    border-color:#ccc;    
    box-shadow: inset 0 1px 1px rgb(0 0 0 / 8%); 
    padding-left: 10px;   
  }  
  .form-wrapp{
    position: relative;
  }
  .search_btn{
    position: absolute;
    display: flex;
    align-items: center;
    justify-content: center;
    right: 5px;
    top: 0;
    bottom: 0;
    margin: auto;
    cursor: pointer;
  }
</style>

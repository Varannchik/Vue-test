<template>
  <div >
       <button @click="click"><span class="btn_name_mob">{{this.PROPS_NAME}}</span></button>
  </div>
</template>

<script>
  export default {
    data: function () {
      return{        
      }
    },
    props: {
      PROPS_NAME: String,
               
    },
    methods:{
      click(){
        this.$emit('click')
      }
    }    
    
  }
</script>

<style scoped>
  button{        
    width: auto; 
    position: relative;
    padding-right: 50px;
    padding-left: 10px;
    cursor: pointer;
    line-height: 24px;
    min-height: 24px;
    font-size: 12px;        
    font-weight: 500;
    border-radius:10px;
    outline: none;
    border: 1px solid lightgray;
    
  }
  button:hover{
    background-color: lightgray;
  }
  button::after{
    content:'\00D7';
    position: absolute;
    width: 20px;
    height: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: white;
    text-align: center;    
    font-size: 16px;       
    top: 0;
    bottom: 0;
    right: 5px;
    margin: auto;
    border-radius: 50%;
    z-index: 10;
  }
  .btn_name_mob{
    display: inline-block;
  }  
  
  @media (max-width: 420px){    
    .btn_name_mob{
      display: none;
    }
    button{      
      padding-right: 25px;      
      font-size: 12px;
      background: transparent;
      border: 1px solid transparent;    
    }
  }  
</style>

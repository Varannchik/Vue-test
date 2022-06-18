<template>
    <div>
        <table>
           <thead>
               <tr>
                   <th colspan="2">Search history</th>                  
                   <th><span @click="clean_history()" class="clean">Clean search history</span></th>
               </tr>
           </thead>
           <tbody>
               <tr v-for="(row, index) in searchData" :key="row.id">                   
                   <td @click="showModal(row.name)" class="link_style">{{ row.name }}</td>
                    
                   <td class="date_block"><time>{{time[index]}}</time></td>
                   <td>                     
                        <Vue-button
                        :PROPS_NAME="'Delete'"
                        :PROPS_ICON="'close'" 
                        @click="delete_item(index)"                       
                        />                
                    </td>
               </tr>
           </tbody>
        </table> 
        <Vue-modal ref="modal" :PROPS_PEOPLE ="this.people"></Vue-modal>       
    </div>
</template>

<script>
import Button from '@/components/Button.vue';
import ModalWindow from '@/components/Modal.vue';

  export default {
       components: {
            "Vue-button": Button,
            "Vue-modal": ModalWindow
        },
    data: function () {
      return{ 
        searchData:this.PROPS_DATA, 
        time:this.PROPS_TIME,
        people:{},
          
      }
    },
    props: {
      PROPS_DATA: Array,     
      PROPS_TIME: Array,
    },
    methods:{
      showModal(value) {
        this.$refs.modal.show = true;
        for (let i = 0; i < this.searchData.length; i++){
        if(value === this.searchData[i].name){
           this.people = this.searchData[i];
           console.log(typeof this.people);           
           return this.people; 
        }        
      }

      }, 
      delete_item(index){      
        this.searchData.splice(index, 1);      
      },
      clean_history(index){      
        this.searchData.splice(index);
      },      
    }  
  }
</script>

<style scoped>
    table{
        width: 100%;
        margin-top: 20px;
        font-size: 14px;
        border-radius: 10px;
        border-spacing: 0;
    }
    th{
        padding: 10px 20px;
        background: #BCEBDD;
        color: black;    
        padding: 10px 20px;
        font-size: 0.8em;
    }
    th, td {
        border-style: solid;
        border-width: 0 1px 1px 0;
        border-color: white;
    }
    tr th:first-child, tr td:first-child{
        text-align: left;
    }
    tr th:last-child, tr td:last-child{
        text-align: right;
    }
    th:first-child {
        border-top-left-radius: 10px;
        }
    th:last-child {
        border-top-right-radius: 10px;
        border-right: none;
    }
    td {
        padding: 10px 20px;
        background: #F8E391;
    }
    tr:last-child td:first-child {
        border-radius: 0 0 0 10px;
    }
    tr:last-child td:last-child {
        border-radius: 0 0 10px 0;
    }
    tr td:last-child {
        border-right: none;
    }  
    .clean{
        cursor: pointer;
    }
    .clean:hover{
        color:blue;
    }
    .date_block{
        font-size: 13px;
        color: grey;
    }
    .link_style{
        cursor: pointer;
        text-decoration: underline;
    }
    .link_style:hover{
        cursor: pointer;
        text-decoration: none;
    }
    @media (max-width: 420px){
        table{    
        font-size: 12px;    
        }
        .date_block{
        font-size: 10px;
        color: grey;
        }
        tr td:last-child{
        text-align: center;
        }
}
</style>
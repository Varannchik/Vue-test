<template>
  <div v-if="show" class="modal-shadow" >
        <div class="modal">
            <div class="modal-close" @click="closeModal">&#10006;</div>
            <div>              
                <h3 class="modal-title">{{this.PROPS_PEOPLE.name}}</h3>
              
                <div class="modal-content">                    
                    <div v-for="(val, key) in this.PROPS_PEOPLE"  :key="val.id" class="persone-container">                     
                      <span>{{ key }}: </span><span>{{ val }}</span>
                    </div>
                </div>             
              
                <div class="modal-footer">
                    <button class="modal-footer_button" @click="closeModal">
                        Ок
                    </button>
                </div>

              </div>           
            
        </div>
    </div>
</template>

<script>
  export default {
    data: function () {
      return{ 
        show: false,
                
      }
    },
    methods: {
        closeModal: function () {
            this.show = false            
        }
    },
    props: {
      PROPS_PEOPLE: Object,
    },
    
    
  }
</script>

<style scoped >
  .modal-shadow {
        position: absolute;
        z-index: 100;
        top: 0;
        left: 0;
        min-height: 100%;
        width: 100%;
        background: rgba(0, 0, 0, 0.39);
    }
 
    .modal {
        background: #fff;
        border-radius: 8px;
        padding: 15px;
        min-width: 420px;
        max-width: 480px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);  
        
        
    }
    .modal-footer_button {
                background-color: #BCEBDD;
                color: black;
                border: none;
                text-align: center;
                padding: 8px;
                font-size: 17px;
                font-weight: 500;
                border-radius: 8px;
                min-width: 150px;
                cursor: pointer;
            }
    .modal-title {
            color: black;
        }
 
        .modal-content {
            margin-bottom: 20px
        }
 
    .modal-close {
            border-radius: 50%;
            color: #fff;
            background: #BCEBDD;
            display: flex;
            align-items: center;
            justify-content: center;
            position: absolute;
            top: 7px;
            right: 7px;
            width: 30px;
            height: 30px;
            cursor: pointer;
        }
    .persone-container{
      text-align: left;
    }
  @media (max-width: 480px){    
    .modal {        
        min-width: 320px;
        max-width: 100%;
    }
  }  
</style>

<template class="addItem">
    <div>
       <input type="text" v-model="item.name" placeholder="insert todo item"/>
       <font-awesome-icon 
       icon="plus-square"
       @click="addItem()"
       :class="[item.name ? 'active' : 'inactive' , 'plus']" />
        
    </div>
</template>

<script>
import axios from 'axios';

    export default{
        data :function(){
            return {
                item:{
                    name:""
                }
             
            }
        },
        methods:{
            addItem(){
                if(this.item.name== ''){
                    return ;
                }
                axios.post('api/item/store',{
                   item:this.item 
                })
                .then(res=>{
                    if(res.status==201){
                        this.item.name="";
                        this.$emit('relodelist');
                    }
                })
                .catch(error=>{
                    console.log(error);
                })
            }
        }
    }
</script>
<style>
    .addItem{
        display: felx;
        justify-content: center;
        align-items: center;
    }
    input {
        background-color: #f7f7f7;
        border: 0px;
        outline: none;
        padding:  10px;
        margin-right: 10px;
        width: 100%;
    }
    .plus{
        font-size: 20px;
    }
    .active{
        color: #00CE25
    }
    .inactive{
        color: #9999;
    }
</style>
<template>
    <div class="todolistContiner">
<div class="heading">
<h2 id="title">Todo List</h2>
<add-item-form 
v-on:relodelist="getList()"></add-item-form>
</div>

<!-- pass prop clled item with item store here to list view -->
<list-view 
:items="items" 
v-on:relodelist="getList()"></list-view>
    </div>
</template>

<script>
 import axios from "axios"
import addItemForm from "./addItemForm.vue"
import listView from "./listView.vue"
export default{
    components:{
        addItemForm,
        listView
    },
    data: function(){
        return{
            items:[]
        }
    },
    methods:{
        getList(){
            axios.get('api/items')
            .then(res=>{
                this.items=res.data
            })
            .catch(err=>{
                console.log(err);
            }
            )
        }
    },
    created(){
        this.getList();
    }
}
</script>
<style scoped>
.todoListContiner{
    width: 100%;
    margin:  auto;
}
.heading{
   
    background-image: url("../../images/4023414.jpg");
    background-repeat: no-repeat, repeat;
    background-size: cover;
    padding: 200px;

}
#title{
    justify-content: center;
    text-align: center;
    color: white;
    font-family: 'Courier New', Courier, monospace;
    
}
</style>
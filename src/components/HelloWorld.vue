<template>
  <div>
    hello
    <ul>
        <li v-for="(item,index) in todos" :key="item.id">{{item.deskripsi}}<button @click="hapus(item.id,index)">X</button></li>

    </ul>
    
    <input v-model="myText"/>
    <button @click="tambahkan">klik saya</button>
    
  </div>
</template>

<script>
import axios from 'axios'
export default{
    data:()=>{
        
        return {
        todos:[]
    ,
        myText:"haha"
        }
    },
    mounted:function(){
        axios.get('http://localhost:3000/todo')
        .then(result=>{
            this.todos=result.data
        })
    }
    ,
    methods:{
        tambahkan: function(){
            let newItem={deskripsi:this.myText}
            axios.post('http://localhost:3000/todo',newItem)
            this.todos.push(newItem)
        },
        hapus:function(id,idx){ 
        axios.delete(`http://localhost:3000/todo/${id}`)
        this.todos.splice(idx,1)
        }
    }
}
</script>


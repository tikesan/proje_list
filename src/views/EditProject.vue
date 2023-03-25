<template>
  <h1>Edit Project{{id}}</h1>
  <form @submit.prevent="editProject">
      <label>Project Title</label>
      <input type="text" v-model="title">
      <label>Project Detail</label>
      <input type="text" v-model="detail">
      <button>Edit Project</button>
  </form>
</template>

<script>
export default {
    props:['id'],
    data(){
        return{
            title:"",
            detail:""
        }
    },
    mounted(){
        fetch("http://localhost:3000/projects/"+this.id)
        .then((res)=>{
            return res.json();
        })
        .then((datas)=>{
            this.title = datas.title,
            this.detail = datas.detail
        })
    },
    methods:{ 
        editProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"
                },
                body:JSON.stringify(
                    {
                        title:this.title,
                        detail:this.detail
                    }
                )
            })
            .then(()=>{
                // redirect
                this.$router.push("/")
            })
            .catch((err)=>{
                console.log(err);
            })
        }
    }

}
</script>

<style>

</style>
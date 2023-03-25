<template>
  <div class="project" :class="{complete:project.complete}">
    <div class="flexing">
        <div>
            <h3 @click="showDetail =!showDetail">{{project.title}}</h3>
        </div>
        <div>
            <span class="material-icons" @click="deleteProject" style="color:red;">delete</span>
            <router-link :to="{name:'EditProject',params:{id:project.id}}">
                <span class="material-icons" style="color:#f0bb59">edit</span>
            </router-link>
            <span class="material-icons" @click="completeProject" :class="{icolor:project.complete}">done</span>
        </div>
    </div>
          <p v-if="showDetail">{{project.detail}}</p>
  </div>
</template>

<script>
export default {
    props:['project'],
    data(){
        return{
            showDetail:false,
            api:"http://localhost:3000/projects/"
        }
    },
    methods:{
        deleteProject(){
            let deleteRoute = this.api+this.project.id;
            fetch(deleteRoute,{method:"Delete"})
            .then(()=>{
                this.$emit('delete',this.project.id);
            })
            .catch((err)=>{
                console.log(err);
            })
        },
        completeProject(){
            let completeUpdateRoute = this.api+this.project.id;
            console.log(completeUpdateRoute);
            fetch(completeUpdateRoute,{
                method:"PATCH",
                headers:{
                    "Content-Type":"application/json"  
                },
                body:JSON.stringify(
                    {
                        complete:!this.project.complete
                    }
                )
            })
            .then(()=>{
                console.log(this.project.complete)
                this.$emit('complete',this.project.id)
            }
            )
            .catch((error)=>{
                console.log(error);
            })
        }
    }

}
</script>

<style>
.project{
    padding: 20px;
    margin:10px;
    background-color: white;
    border-radius:10px;
    border-left: 8px solid crimson;
}
h3{
    color: indigo;
    cursor: pointer;
}
.flexing{
    display: flex;
    justify-content: space-between;
    align-items: center;
}
span:hover{
    color: #777;
    cursor: pointer;
}
.icolor{
    color:#7de398;
}
.complete{
    border-left: 8px solid #7de398;
}
</style>
<template>
   <FilterNavbar @firstValue="current=$event" :current="current"></FilterNavbar>
   <div v-for="project in filterPro" :key="project.id">
    <SingleProject :project="project" @delete="deleteProject" @complete="completeProject"></SingleProject>
   </div>
</template>

<script>
import FilterNavbar from '../components/FilterNavbar'
import SingleProject from '../components/SingleProject'
export default {
  components: {
    FilterNavbar, SingleProject },
  data(){
    return{
      current:"all",
      projects:[]
    }
  },
  methods:{
    deleteProject(id){
      this.projects=this.projects.filter(pr=>{
        return pr.id !=id;
      })
    },
    completeProject(id){
      let findProject = this.projects.find(pr=>{
        return pr.id ==id;
      });
      findProject.complete = !findProject.complete;
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then((response)=>{
      return response.json();

    })
    .then((datas)=>{
      this.projects = datas;
    })
    .catch((error)=>{
      console.log(error);

    })
  },
  computed:{
    filterPro(){
      if(this.current=="complete"){
        return this.projects.filter(p=>{
          return p.complete;
        })
      }
      if(this.current=="ongoing"){
        return this.projects.filter(p=>{
          return !p.complete;
        })
      }
      return this.projects;


    }
  }

}
</script>

<style>

</style>

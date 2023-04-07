<template>
    <div class="submit-form">
        <div v-if="!submitted">
            <div class="form-group">
                <label for="title">Title</label>
                <input type="text" v-model="tutorial.title" class="form-control" placeholder="title" name="title"/>
                <label for="Description">Description</label>
                <input  type="textbox" v-model="tutorial.description" placeholder="description" class="form-control" name="description"/>
                <button class="form-control" @click = "saveData">Submit Data</button>
            
            </div>
            
            

        </div>
        <div v-else>
            <h4>You have sumitted sucessfully</h4>
            <router-link to="/add" class="nav-link">Add</router-link>

        </div>
        
    </div>


</template>
<script>
import  TutorialDataService  from '../services/TutorialDataService';

export default{
    name:'AddTutorial',
    data(){
        return{
            tutorial:{
                title:'',
                description:'',
                id:''
            },
            submitted:false
        }

    },
    methods:{
        saveData(){
            var data= {
                title:this.tutorial.title,
                description:this.tutorial.description
            }
            TutorialDataService.create(data)
            .then(response=>{
                this.tutorial.id=response.data.id;
                console.log(response.data)
                this.submitted=true;
            })
            .catch(e=>{
                console.log(e);
            })

        },

        newTutorial(){
            this.submitted==false;
            this.tutorial={};

        }

    }
}

</script>
<style>
</style>
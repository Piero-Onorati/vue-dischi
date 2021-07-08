<template>
    <div class="container">
        <h2>ciao</h2>
        <!-- <Card/> -->
    </div>
</template>

<script>
import axios from 'axios'
// import Card from '@/components/Card.vue'

export default {
    name:'MainContent',
    components:{
        // Card,
    },
    data(){
        return{
            apiURL : 'https://flynn.boolean.careers/exercises/api/array/music',
            records:[]
        }
    },
    created(){
        this.getTheRecord()
    },

    methods:{
        getTheRecord(){
            axios
                .get(this.apiURL)
                .then(res=>{
                    this.records= res.data.response;
                })
                .catch(error =>{
                    console.log('Errore', error);
                });

        }

    }

}
</script>

<style>

</style>
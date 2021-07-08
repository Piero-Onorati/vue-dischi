<template>
    <section>
        <div class="container-sm py-4">
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 gx-4" v-if="!loading">
                <Card v-for="(record,index) in records" :key="index" :details="record"/>
            </div>
            <Loader/>
        </div>
    </section>
</template>

<script>
import axios from 'axios'
import Card from '@/components/Card.vue'
import Loader from '@/components/Loader.vue'

export default {
    name:'MainContent',
    components:{
        Card,
        Loader
    },
    data(){
        return{
            apiURL : 'https://flynn.boolean.careers/exercises/api/array/music',
            records:[],
            loading : true
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
                    this.records = res.data.response;
                    this.loading = false;
                })
                .catch(error =>{
                    console.log('Errore', error);
                });
        }

    }

}
</script>

<style lang='scss'>
@import '../style/vars.scss';

section{
    background-color: $dark;
}





</style>
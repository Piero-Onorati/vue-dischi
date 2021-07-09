<template>
    <section>
        <div class="container-sm pb-4">
            <div class="col-6 select py-4">
                <span class="px-3">Select genre...</span>
                <select v-model="selected">
                    <option >All</option>
                    <option v-for="(option,index) in options" :key="index">{{option}}</option>
                </select>

                <span class="px-3">Sort by date...</span>
                <select v-model="dateSelected">
                    <option>Random</option>
                    <option>Newest</option>
                    <option>Oldest</option>
                </select>
            </div>   
           
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 row-cols-lg-4 row-cols-xl-5 gx-4" v-if="!loading">
                <Card v-for="(record,index) in filterRecords" :key="index" :details="record"/>
            </div>
            <Loader v-else/>
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
            loading : true,
            selected:'',
            dateSelected:'',
            options:[],
            new:[]
        }
    },


    created(){
        this.getTheRecord()
    },

    computed:{

        filterRecords: function(){
            return this.filterByDate(this.filterByGenre(this.records))
        }

        // filterRecords(){

        //     return this.records.filter(element =>{
        //         if (this.selected == '' || this.selected == 'All') {
        //             return this.records
        //         }
        //         else{
        //             return element.genre == this.selected
        //         }
        //     });

        // }

    },

    methods:{
        getTheRecord(){
            axios
                .get(this.apiURL)
                .then(res=>{
                    this.records = res.data.response;
                    this.loading = false
                    this.createList()
                })
                .catch(error =>{
                    console.log('Errore', error);
                });
        },

        createList(){
            console.log(this.records)
            this.records.forEach(element => {
                if (!this.options.includes(element.genre)) {
                     this.options.push(element.genre)
                }
            });
        },

        filterByGenre(array){
            return array.filter(element =>{
                if (this.selected == '' || this.selected == 'All') {
                    return array
                }
                else{
                    return element.genre == this.selected
                }
            });
        },

        filterByDate(array){
            if (this.dateSelected =='Newest') {
                array = array.sort((a,b) => {
                   return b.year- a.year 
                })
                return array
                
            }else if(this.dateSelected =='Oldest'){
                array = array.sort((a,b) => {
                   return a.year - b.year
                })
                return array

            }else{
                return array
            }
            
        }
    }


}
</script>

<style lang='scss'>
@import '../style/vars.scss';

section{
    background-color: $dark;
    height: 100vh;
    overflow-y:scroll ;
    .select{
        color:$text-light;

        select{
            padding: 5px;
            background-color: lightgrey;
            width: 100px;
        } 

    }
  
  
}





</style>
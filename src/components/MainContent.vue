<template>
    <section>
        <div class="container-sm py-5">
            <!-- 1) if the Select is the Component with the list that needed to be sorted -->
            <!-- <div class="col-6 select py-4">
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
            </div>   -->
            
            <!-- 2) if the Select is a Child Component -->
            <!-- <Select :details="options" @vModelGenre="genreReceived"  @vModelDate="dateReceived"/>  -->
           
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
import { component } from 'vue/types/umd'
/* 2) if the Select is a Child Component */
// import Select from '@/components/Select.vue'


export default {
    name:'MainContent',
    components:{
        Card,
        Loader,
        /* 2) if the Select is a Child Component */
        // Select
    },

    data(){
        return{
            apiURL : 'https://flynn.boolean.careers/exercises/api/array/music',
            records:[],
            loading : true,
            selected:'',
            dateSelected:'',
            options:[],
        }
    },

    created(){
        this.getTheRecord()
    },

    computed:{

        /* apply both filters (for genre and for date)*/
        filterRecords: function(){
            return this.filterByDate(this.filterByGenre(this.records))
        }

        /* apply only one filter*/
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


    /* 3) Receive and assaign the V-model values when the 'Select.vue' is a non related component*/
    mounted(){
        this.$root.$on('vModelGenre',(arg1)=>{ 
            this.selected=arg1
        });
        
        this.$root.$on('vModelDate',(arg2)=>{ 
            this.dateSelected=arg2
        });

    },

    methods:{
        getTheRecord(){
            axios
                .get(this.apiURL)
                .then(res=>{
                    this.records = res.data.response;
                    this.loading = false
                    this.$root.$emit('sendArray', this.records)
                    /* 1) e 2) Used when the select is in the same component or in a child component*/
                    // this.createList()
                })
                .catch(error =>{
                    console.log('Errore', error);
                });
        },

        /* 1) e 2) Used when the select is in the same component or in a child component*/
        // createList(){
        //     this.records.forEach(element => {
        //         if (!this.options.includes(element.genre)) {
        //              this.options.push(element.genre)
        //         }
        //     });
        // },

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
            
        },

        /* 2) Assaign the V-model values of child to the v-models of parents when 'Select.vue' is a Child Component */
        // genreReceived(arg1){
        //     console.log
        //     this.selected=arg1
        // },

        // dateReceived(arg2){
        //     this.dateSelected=arg2
        // }
    }

}
</script>

<style lang='scss'>
@import '../style/vars.scss';

section{
    background-color: $dark;
    height: 100vh;
    overflow-y:scroll ;

    /* 1) style for select */
    /* .select{
            color:$text-light;

            select{
                padding: 5px;
                background-color: lightgrey;
                width: 100px;
            } 

    } */

}

</style>
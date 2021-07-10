<template>
  <div class="col-6 select py-4">
                <span class="px-3">Select genre...</span>
                <select v-model="selecting" @change="selectGenre">
                    <option >All</option>
                    <option v-for="(detail,index) in details" :key="index">{{detail}}</option>
                </select>

                <span class="px-3">Sort by date...</span>
                <select v-model="dateSelecting" @change="selectDate">
                    <option>Random</option>
                    <option>Newest</option>
                    <option>Oldest</option>
                </select>
            </div>  
</template>

<script>
export default {
    name:'Select',
    /* if the Select is a Child Component use props*/
    props:["details"],
    data(){
        return{
            selecting:'',
            dateSelecting:''
        }
    },

    methods:{
        /* if the Select is a Child Component*/
        selectGenre(){
            this.$emit('vModelGenre', this.selecting)
        },

        /* if the Select is a Child Component*/
        selectDate(){
            this.$emit('vModelDate', this.dateSelecting)
        }


    }




}
</script>

<style>

</style>
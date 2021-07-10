<template>
  <div class="col-6 select">
                <span class="px-3">Select genre...</span>
                <select v-model="selecting" @change="selectGenre">
                    <option >All</option>
                    <!-- 2) if the Select is a Child Component -->
                    <!-- <option v-for="(detail,index) in details" :key="index">{{detail}}</option> -->
                    <option v-for="(option,index) in options" :key="index">{{option}}</option>
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
    /* 2) if the Select is a Child Component use props*/
    // props:["details"],
    data(){
        return{
            selecting:'',
            dateSelecting:'',
            options:[]
        }
    },

    /* 3) if the Select is a non related Component, in "created" we use a function for populate the options of select*/
    created(){
        this.$root.$on('sendArray',(arr)=>{ 
            arr.forEach(element => {
                if (!this.options.includes(element.genre)) {
                     this.options.push(element.genre)
                }
            })
        })
        

    },

    methods:{
        /* 2) if the Select is a Child Component*/
        // selectGenre(){
        //     this.$emit('vModelGenre', this.selecting)
        // },

        // selectDate(){
        //     this.$emit('vModelDate', this.dateSelecting)
        // }

        /* 3) if the Select is a non related Component*/
        selectGenre(){
            this.$root.$emit('vModelGenre', this.selecting)
        },
        
        selectDate(){
            this.$root.$emit('vModelDate', this.dateSelecting)
        }
    }
    
}
</script>

<style lang='scss'>
@import '../style/vars.scss';

    .select{
        display: flex;
        justify-content: flex-end;
        color:$text-light;
        padding-right: 35px;

        select{
            padding: 5px;
            background-color: lightgrey;
        } 

    } 

</style>
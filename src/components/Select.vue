<template>
  <div class="col-6 select">
                <span class="px-3">Select genre...</span>
                <select v-model="selecting" @change="selectGenre">
                    <option >All</option>
                    <!-- if the Select is a Child Component -->
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
    /* if the Select is a Child Component use props*/
    // props:["details"],
    data(){
        return{
            selecting:'',
            dateSelecting:'',
            options:[]
        }
    },

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
        /* if the Select is a Child Component*/
        // selectGenre(){
        //     this.$emit('vModelGenre', this.selecting)
        // },

        selectGenre(){
            this.$root.$emit('vModelGenre', this.selecting)
        },

        /* if the Select is a Child Component*/
        // selectDate(){
        //     this.$emit('vModelDate', this.dateSelecting)
        // }
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
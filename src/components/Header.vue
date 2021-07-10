<template>
    <header class="d-flex justify-content-between align-items-center"> 
        <div class="img-container">
            <img src="../assets/img/spotify-icon.png" class="my-2 mx-4" alt="logo">
        </div>    
        
        <Select/> 
        
    </header>
</template>

<script>

import Select from '@/components/Select.vue'
export default {
    name: 'Header',
    components:{
        Select
    }

}
</script>

<style lang='scss'>
@import '../style/vars.scss';


header{
    background-color: $light; 

    .img-container{
        width: 50px;

        img{
            width: 100%;
        }
    }
}

</style>




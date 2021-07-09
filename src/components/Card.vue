<template>
    <div class="col pb-4 px-4">
        <div class="my_card text-center h-100">
        <img :src="details.poster" class="img-fluid my_img h-50" :alt="details.title">
        <div class="card-body">
            <h5 class="card-title">{{details.title}}</h5>
            <div class="card-text">
                <span class="name-author">{{details.author}}</span>
                <span>{{details.year}}</span>
            </div>
        </div>
        </div>
    </div>
</template>

<script>
export default {
    name:'Card',
    props: ['details']

}
</script>

<style lang='scss'>
@import '../style/vars.scss';

.my_card{
    background-color: $light;

    &:hover{
        cursor: pointer;
        background-color: rgba(128, 128, 128, 0.322);
    }

    .my_img{
        padding-top: 10px;
        width:70%
    }

        .card-title{
            font-weight:$bold-w ; 
            color: $text-light;
            text-transform: uppercase;
            height: 70px;
        }

    

        .card-text{
            height: 20%;
            color:$text-dark;

            .name-author{
                display: block;
                font-weight: $light-w;
                font-size:18px
            }
        }

}




</style>
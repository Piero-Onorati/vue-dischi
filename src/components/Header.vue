<template>
    <header>
        <img src="../assets/img/spotify-icon-marilyn-scott-0.png" alt="logo">
    </header>
</template>

<script>
export default {
    name: 'Header'

}
</script>

<style lang='scss'>
@import '../style/mixins.scss';

header{
    @include glass;

    img{
        width: 50px;
    }
}

</style>




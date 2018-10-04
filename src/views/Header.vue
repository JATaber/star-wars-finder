<template>
    <header>
        <h1><font-awesome-icon :icon="['fab', 'rebel']" pulse/> Star Wars Character Info <font-awesome-icon :icon="['fab', 'empire']" spin/></h1>
    </header>
</template>

<style lang="scss" rel="stylesheet/scss">

h1{
    text-align: center;
    margin: 20px auto;
    font-size: 48px;
    max-width: 800px;
    color: #FFDD2B;

    .fa-rebel{
        font-size: 58px;
        color: #40BFAB;
    }

    .fa-empire{
        font-size: 58px;
        color: #D30C34;
    }
}
</style>

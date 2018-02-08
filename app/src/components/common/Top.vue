<template>
     <div class="com-top" :style="{background:$store.state.bgColor}">
         <router-link to="/">
            <span class="com-top-btn">首页</span>
        </router-link>
        <h2>
            {{$store.state.title}}
        </h2>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style scoped>
    .com-top{
        height: 1rem;
        background:#c8eeff; 
        position: fixed;
        top:0;
        left: 0;
        width: 100%;
        z-index: 1;

    }
    .com-top-btn{
        color: #fff;
        position: absolute;
        left:0.2rem;
        top:50%;
        transform: translateY(-50%);
        font-size: 0.23rem;
    }
    .com-top h2{
        line-height: 1rem;
        text-align: center;
        color: #fff;
    }
    h2{
        font-size: 0.45rem;
    }
</style>
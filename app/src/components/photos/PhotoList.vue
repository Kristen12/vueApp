<template>
    <ul class="photoData">
        <li v-for="(obj,index) in photoData" :key="index">
            <router-link :to="'/photoDetail/'+index">
                <img :src="obj.src" alt="">
            </router-link>
        </li>
    </ul>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                photoData: []
            }
        },
        mounted:function(){
            this.$store.commit('change',{bgColor:'#1f1f1f',title:'Photo'});
             //ajax
            axios.get('/static/data/photodata.json').then(res=>{
                this.photoData = res.data.photoData;
                this.$store.state.photoData = this.photoData
            })
        }
    }
</script>

<style scoped>
     .photoData{
        overflow: hidden;
        margin: 1rem 0;
    }
    .photoData li{
        width:100%;
        margin: 0.05rem 0;
    }
    .photoData li img{
        width: 100%;
        display: block
    }
    a{
        outline: none;
    }
</style>
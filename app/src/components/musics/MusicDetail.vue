<template>
    <div class="music-box">
        <aplayer autoplay="null" :music="musicData" v-if="isShow"></aplayer>
    </div>
</template>

<script>
    import axios from 'axios';
    import Aplayer from 'vue-aplayer';
    export default {
        data() {
            return {
                musicData: [],
                isShow:false//当aplayer执行时，由于异步加载，数据还未加载完报错。
            }
        },
        components: {
            Aplayer//引组件
        },
        mounted:function(){
            this.$store.commit('change',{bgColor:'#1f1f1f',title:'Music'});
            axios.get('/static/data/musicdata.json').then(res=>{
                var arr=res.data.musicData;
                for(var i=0; i<arr.length; i++){
                    arr[i].lrc = '/static/'+arr[i].lrc;
                     //解构
                    var {title,author,src:url,musicImgSrc:pic,lrc} = arr[i];
                    //对象属性简写
                    var obj = {title,author,url,pic,lrc}
                    this.musicData.push(obj);
                    // /static/lrc/我要你.lrc
                }
                this.isShow = true;
            })
            console.log(this.musicData);
        }
    }
</script>

<style scoped>
    .music-box{
        margin: 1rem 0;
    }
</style>
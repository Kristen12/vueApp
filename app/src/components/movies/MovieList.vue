<template>
    <div class="movieList">
        <ul>
            <li v-for="(obj,index) in movies" :key="index" @click="fn(obj.id)">
                <div class="img-box">
                    <img :src="obj.img" alt="">
                </div>
                <div class="info-box">
                    <h2 class="title">{{obj.nm}}</h2>
                    <p>{{obj.ver}}</p>
                    <p>{{obj.star}}</p>
                    <p>{{obj.showInfo}}</p>
                </div>
            </li>
        </ul>
        <div class="load" v-show="isLoad">
            <img src="@/assets/images/5-121204194035.gif" alt="">
        </div>
        <div class="end" v-show="isEnd">
            到底了，亲~
        </div>
    </div>
</template>

<script>
        import axios from "axios"
        export default {
            data() {
                return {
                    movies:[],
                    isLoad:true,
                    isEnd:false,
                    flag:true //没有请求
                }
            },
            methods:{
                load(){
                    if(this.flag){//经验型问题：当前没有请求的时候才发送
                        this.flag = false;//我正在发请求
                        axios.get(API_INTERFACE+'http://m.maoyan.com/movie/list.json?type=hot&offset='+this.movies.length+'&limit=10').then((res)=>{
                            if(res.data.data.movies.length < 10){
                                this.isEnd = true;//当请求数小于10
                            }
                            this.movies = [...this.movies,...res.data.data.movies];//ES6扩展运算符，数组的合并，数组不能+=
                            this.isLoad = false;//每次请求完数据就隐藏
                            this.flag = true;
                        }).catch(()=>{
                            console.log('请求失败');
                        });
                    }
                },
                fn(id){
                    this.$router.push('/movieDetail/'+id);
                }
            },
            mounted:function(){
                this.$store.commit('change',{bgColor:'#1f1f1f',title:'Movie'});
                //axios请求
                this.load();
                //下拉框下拉时加载图片
                window.onscroll=()=>{
                    //滚动条滚动高度（页面上）
                    var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
                    //可视区高度
                    var clientHeight = document.documentElement.clientHeight;
                    //整个页面的高度
                    var scrollHeight = document.documentElement.scrollHeight;
                    if(scrollTop + clientHeight == scrollHeight){
                        if(!this.isEnd){//数据没有加载完 再发请求 loading show
                            this.load();
                            this.isLoad = true;//因为请求完后隐藏，所以再次请求时出现
                        } 
                    }
                }
            }
        }
</script>

<style scoped> 
    .movieList{
        margin:1rem 0;
    }
     .movieList li{
        display: flex;
        padding: 0.2rem;
        border-bottom:0.02rem solid #ccc;
    }
    .img-box{
        flex-grow: 1;
        width: 0;
        margin-right: 0.2rem;
    }
    .img-box img{
        width:100%;
    }
    .info-box{
        flex-grow: 2;
        width: 0;
    }
    .title{
        font-size: 0.33rem;
        font-weight: bold;
    }
    .info-box p{
        font-size: 0.27rem;
    }
    .load{
        text-align:center;
    }
    .end{
        text-align:center;
    }
</style>
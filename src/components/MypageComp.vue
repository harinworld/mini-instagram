<template>
    <div style="padding : 10px" class="mypage-bg">
      <h4>팔로워</h4>
      <input placeholder="?" @input="search($event.target.value)"/>
      <div class="post-header" v-for="(a,i) in follower" :key="i">
        <div class="profile" :style="`background-image:url(${a.image})`"></div>
        <span class="profile-name">{{a.name}}</span>
      </div>
    </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import axios from 'axios';

export default {
    name:'MypageComp',
    props:{
        one : Number,
    },

    setup(){
        let follower = ref([]);
        let followerOriginal = ref([]);

        onMounted(()=>{
            axios.get('/follower.json').then((a)=>{
                follower.value = a.data;
                followerOriginal.value = [...a.data];
            })
        });

        function search(keyword){
            let newFollower = followerOriginal.value.filter((a)=>{
                return a.name.indexOf(keyword) != -1
            });
            follower.value = [...newFollower]
        }
        return {follower, search}
    }
}
</script>

<style>
    .mypage-bg{
        background-color: #fff;
    }
</style>
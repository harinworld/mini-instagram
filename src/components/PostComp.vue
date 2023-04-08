<template>
    <div class="post">
        <div class="post-header">
            <div class="profile"></div>
            <span class="profile-name">{{contents.name}}</span>
        </div>
        <div @click="$store.commit('likeNum')" :class="contents.filter" class="post-body" :style="{ backgroundImage : `url(${contents.postImage})` }" ></div>
        <div class="post-content">
            <p>{{$store.state.likes}} Likes</p>
            <p><strong>{{contents.name}}</strong> {{contents.content}}</p>
            <p class="date">{{contents.date}}</p>
        </div>
    </div> 
</template>

<script>
export default {
    name:"PostComp",
    props:{
        contents : Object,
    }
}
</script>

<style>
.post {
  width: 100%;
  background-color: #fff;
}
.profile {
  background-image: url("https://placeimg.com/100/100/arch");
  width: 30px;
  height: 30px;
  background-size: 100%;
  border-radius: 50%;
  float: left;
}
.profile-name {
  display: block;
  float: left;
  padding-left: 10px;
  padding-top: 7px;
  font-size: 14px;
}
.post-header {
  height: 30px;
  padding: 10px;
}
.post-body {
  background-image: url("https://wwws.dior.com/couture/ecommerce/media/catalog/product/cache/1/grid_image_3/460x497/17f82f742ffe127f42dca9de82fb58b1/d/H/1677671454_M0455CBER_M041_E03_GH.jpg?imwidth=750");
  height: 450px;
  background-position: center;
  background-size: cover;
}
.post-content {
  padding-left: 15px;
  padding-right: 15px;
  font-size: 14px;
}
.date {
  font-size: 11px;
  color: grey;
  margin-top: -8px;
} 
</style>
<template>
    <div>
        <div v-if="step == 0">
            <PostComp :contents = "contents[i]" v-for="(a,i) in contents" :key="i" />
        </div>

        <!-- 필터선택페이지 -->
        <div v-if="step == 1" class="container-bg">
            <div :class="selectfilter" class="upload-image" :style="`background-image:url(${image})`"></div>
            <div class="filters">
                <FilterBox v-for="filter in filters" :key="filter" :image = "image" :filter = "filter" >
                    <span>{{ filter }}</span>
                </FilterBox>
            </div>
        </div>

        <!-- 글작성페이지 -->
        <div v-if="step == 2">
            <div :class="selectfilter" class="upload-image" :style="`background-image:url(${image})`"></div>
            <div class="write">
                <textarea @input="$emit('write', $event.target.value)" class="write-box">write!</textarea>
            </div>
        </div>

        <div>
            <MypageComp :one="1"/>
        </div>
    </div>
</template>

<script>
import FilterBox from './FilterBox.vue';
import MypageComp from './MypageComp.vue';
import PostComp from './PostComp.vue';

export default {
    name:"ContainerComp",
    data(){
        return{
            filters : [ "aden", "_1977", "brannan", "brooklyn", "clarendon", "earlybird", "gingham", "hudson", "inkwell", "kelvin", "lark", "lofi", "maven", "mayfair", "moon", "nashville", "perpetua", "reyes", "rise", "slumber", "stinson", "toaster", "valencia", "walden", "willow", "xpro2"],
            selectfilter : '',
        }
    },
    mounted(){
        this.emitter.on('firebtn', (a)=>{
            this.selectfilter = a
        })
    },
    components: { 
        PostComp,
        FilterBox,
        MypageComp,
    },
    props:{
        contents : Array,
        step : Number,
        image : String,
    }
}
</script>

<style>
/* .container-bg{
    background-color: aqua;
} */
.upload-image{
width: 100%;
height: 450px;
background: cornflowerblue;
background-size : cover;
}
.filters{
overflow-x:scroll;
white-space: nowrap;
}
.filter-1 {
width: 100px;
height: 100px;
background-color: cornflowerblue;
margin: 10px 10px 10px auto;
padding: 8px;
display: inline-block;
color : white;
background-size: cover;
}
.filters::-webkit-scrollbar {
height: 5px;
}
.filters::-webkit-scrollbar-track {
background: #f1f1f1; 
}
.filters::-webkit-scrollbar-thumb {
background: #888; 
border-radius: 5px;
}
.filters::-webkit-scrollbar-thumb:hover {
background: #555; 
}
.write-box {
border: none;
width: 90%;
height: 100px;
padding: 15px;
margin: auto;
display: block;
outline: none;
background-color: #fff;
}
</style>
<template>
  <div class="header">
      <ul class="header-button-left">
        <li>Cancel</li>
      </ul>
      <ul class="header-button-right">
        <li v-if="step == 1" @click="step++">Next</li>
        <li v-if="step == 2" @click="publish">POST</li>
      </ul>
      <!-- <img src="./assets/logo.png" class="logo" /> -->
    </div>

    <!-- <p>{{ myname }} {{ age }} {{ likes }}</p>

    <h4>안녕 {{ $store.state.age }} </h4>
    <button @click="plusOne(10)">버튼</button>

    <p>{{ $store.state.more }}</p>
    <button @click="$store.dispatch('getData')">더보기</button> -->

    <ContainerComp @write="postcontent = $event" :contents = "contents" :step = "step" :image = "image" />

    <!-- <button @click="more">더보기</button> -->

    <div class="footer">
      <ul class="footer-button-plus">
        <input @change="upload" type="file" id="file" class="inputfile" />
        <label for="file" class="input-plus">Posting</label>
      </ul>
    </div>

</template>

<script>
import ContainerComp from './components/ContainerComp.vue';
import data from './assets/data';
import axios from 'axios'
import { mapMutations, mapState } from 'vuex';


export default {
  name: 'App',
  data(){
    return{
      contents : data,
      button : 0,
      step : 0,
      image : '',
      postcontent : '',
      selectfilter : '',
      counter : 0,
    }
  },
  mounted(){
    this.emitter.on('firebtn', (a)=>{
      this.selectfilter = a
    })
  },
  components: {
    ContainerComp,
  },
  computed:{
    name(){
      return this.$store.state.name
    },
    ...mapState(['name', 'age', 'likes']),
    ...mapState({ myname : 'name', })
  },
  methods: {
    ...mapMutations(['setMore', 'likeNum', 'plusOne']),
    now(){
      return new Date()
    },
    more(){
      // //서버로 데어터 전달하는 법
      // axios.post('URL', {name : 'kim'})
      // //서버통신 성공
      // .then()
      // //서버통신 실패
      // .catch((err)=>{
      //   err
      // })

      //서버에서 데이터 가져오는법
      axios.get(`https://codingapple1.github.io/vue/more${this.button}.json`)
      .then((result)=>{
        // 요청 성공시 실행할 코드
        console.log(result.data);
        this.contents.push(result.data);
        this.button++;
      })
    },
    upload(e){
      let file = e.target.files;
      console.log(file);
      //이미지의 가상 url 생성해줌
      let url = URL.createObjectURL(file[0]);
      console.log(url);
      this.image = url;
      //업로드 후 다음페이지로 이동
      this.step++;
    },
    publish(){
      var mypost = {
                      name: "Kim Hyun",
                      userImage: "https://placeimg.com/100/100/arch",
                      postImage: this.image,
                      likes: 36,
                      date: "May 15",
                      liked: false,
                      content: this.postcontent,
                      filter: this.selectfilter
                  };
      this.contents.unshift(mypost);  //unshift는 array에 데이터 추가하는 js문법
      this.step = 0;
    },
  },
}
</script>

<style>
body {
  margin: 0;
  background-color: #E0C3F9;
}
ul {
  padding: 5px;
  list-style-type: none;
}
.logo {
  width: 22px;
  margin: auto;
  display: block;
  position: absolute;
  left: 0;
  right: 0;
  top: 13px;
}
.header {
  width: 100%;
  height: 40px;
  background-color: #FF9CA3;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: rgb(255, 255, 255);
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: rgb(255, 255, 255);
  float: right;
  width: 50px;
  cursor: pointer;
  margin-top: 10px;
}
.footer {
  width: 100%;
  position: sticky;
  bottom: 0;
  padding-bottom: 10px;
  background-color: #FBF7B0;
}
.footer-button-plus {
  width: 80px;
  margin: auto;
  text-align: center;
  cursor: pointer;
  font-size: 24px;
  padding-top: 12px;
}
.sample-box {
  width: 100%;
  height: 600px;
  background-color: bisque;
}
.inputfile {
  display: none;
}
.input-plus {
  cursor: pointer;
  font-size: 1rem;
}
#app {
  box-sizing: border-box;
  font-family: "consolas";
  margin-top: 60px;
  width: 100%;
  max-width: 460px;
  margin: auto;
  position: relative;
  border-right: 1px solid #eee;
  border-left: 1px solid #eee;
}
</style>

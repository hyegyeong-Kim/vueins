<template>
  <div class="header">
    <ul class="header-button-left">
      <li>Cancel</li>
    </ul>
    <ul class="header-button-right">
      <li v-if="step == 1" @click="step++">Next</li>
      <li v-if="step == 2" @click="publish()">발행</li>
    </ul>
    <img src="./assets/logo.png" class="logo" />
  </div>

  <Container :데이터들="데이터들" :step="step" :이미지="이미지" @write="작성한글 = $event"></Container>
  <button @click="more" v-if="step == 0">더보기</button>


  <div class="footer">
    <ul class="footer-button-plus">
      <input @change="upload" type="file" id="file" class="inputfile" /> 
      <label for="file" class="input-plus" v-if="step == 0">+</label>
    </ul>
 </div>
</template>

<script>
import Container from './components/Container.vue'
import Data from './data.js'
import axios from 'axios'
// axios.get()

export default {
  name: 'App',
  components: {
    Container,
  },
  data(){
    return {
      step : 0,
      데이터들 : Data,
      더보기 : 0,
      이미지 : '',
      작성한글 : '',
    }
  },
  methods : {
    more(){
      axios.get('https://codingapple1.github.io/vue/more'+ this.더보기 +'.json')
      .then((결과)=>{
        this.데이터들.push(결과.data); 
        this.더보기++;//이데이터를 위에 data에 pusu
      })
    },
    upload(e){
      let 파일 = e.target.files; //업로드한 파일
      let url = URL.createObjectURL(파일[0]) //해당 파일로 url 만들기
      console.log(url)
      this.이미지 = url
      this.step = 1
    },
    publish(){
      var 내게시물 = {
          name: "Kim Hyun",
          userImage: "https://picsum.photos/100?random=1",
          postImage: this.이미지,
          likes: 36,
          date: "May 15",
          liked: false,
          content: this.작성한글,
          filter: "perpetua"
        };
        this.데이터들.unshift(내게시물);
        this.step = 0;
      }, 
  },

}
</script>

<style>

body {
  margin: 0;
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
  background-color: white;
  padding-bottom: 8px;
  position: sticky;
  top: 0;
}
.header-button-left {
  color: skyblue;
  float: left;
  width: 50px;
  padding-left: 20px;
  cursor: pointer;
  margin-top: 10px;
}
.header-button-right {
  color: skyblue;
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
  background-color: white;
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

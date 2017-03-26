<template>
  <div id="app">
    <div class="left">
      <img :src=obj.data.songs[0].artists[0].picUrl alt="" class="photo" />
    </div>
    <div class="right">
      <button @click=toggle() ><div :class="{stop:played}"></div></button>
      <audio :src=mp3  autoplay="autoplay"></audio>
    </div>
  <div class="content">
      <div class="artist"><p>{{ obj.data.songs[0].name }}</p><p><em>{{obj.data.songs[0].artists[0].name}}</em></p></div>
  </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      played:false,
      obj:{},
      mp3:""
    }
  },
  mounted(){
    var that=this;
    var url='https://bird.ioliu.cn/netease?id='+this.random(100000,400000);
    axios.get(url)
          .then(function (response) {

            that.obj=response;

          })
          .catch(function (error) {
            console.log(error);
          });
  },
  methods:{
    toggle(){
      if (!this.played) {
        this.play()
      }else{
        this.stop()
      }
       this.played=!this.played;
    },
    play(){
        this.mp3=this.obj.data.songs[0].mp3Url;
    },
    stop(){
      this.mp3=''
    },
    random(m,n){
      return Math.round(Math.random()*(n-m))+m;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 480px;
  height: 120px;
  margin:0 auto;
}
p,span{padding:5px;}
.left{float:left;}.right{float:right;}
.left .photo,.right{width: 100px;height: 100px;padding: 5px;}
.content{
  margin-left:120px;
  margin-right:120px;
  height: 120px;
  vertical-align:middle;
}
.artist{
  height: 100px;
  padding: 5px;
}

button{
  border:none;
  outline: none;
  display:inline-block;
  border-radius:50%;
  position: relative;
  height: 60px;
  width: 60px;
  padding: 10px;
  margin:10px
}
button div{
    width: 0;
    height: 0;
    border-top: 15px solid transparent;
    border-left: 30px solid #C3C1C1;
    position: absolute;
    top: 15px;
    left: 20px;
    border-bottom: 15px solid transparent;
}
.stop{
    top: 15px;
    left: 15px;
    background: #C3C1C1
}
</style>

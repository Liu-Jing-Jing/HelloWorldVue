<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="安装成功 Vue.js App"/>
    
    <ul>
      <li v-for='(song, index) in lists' :key = 'index' @click="liCLick(song.id)" ><button>{{song.name}}</button></li>
    </ul>

    <audio :src="songUrl" controls='controls'  ref="player"></audio>
  </div>
  

  
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from 'axios'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {num:123,
      lists:[],
      songUrl:''

    }
  },
  created(){
    axios({
        url: "http://183.237.67.218:3000/search?keywords=知足"
    }).then(res => {
        console.log(res);
        // http://183.237.67.218:3000/song/url?id=310574
        var lists = res.data.result.songs;
        this.lists = lists;

    })
  },
  methods:{
    liCLick(id){
    axios({
            url: "http://183.237.67.218:3000/song/url?id="+ id
        }).then(songData => {
            window.console.log(songData.data);
            window.console.log(this.$refs.player.src);

            this.songUrl = songData.data.data[0].url;
            // http://183.237.67.218:3000/song/url?id=310574
            
            

        })
    }
  }
}
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: skyblue;
}

/* CSS导入外部文件的关键字使用的是@import url(path) */

</style>

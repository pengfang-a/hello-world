<template>
  <div class="gallery">
    <div id="container">
        <div class="photo-box" :id="item.id" v-for="(item,index) in photoArr" :class="{'center':item.id==centerId}" @click="clickHandler(item)" :style="{left: item.left+'px',
    top: item.top+'px', transform: 'rotate('+item.rotate+'deg)'
  }">
            <div class="overturn">
                <div class="front" :style="{transform:'rotateY('+item.frontRotateY+'deg)'}">
                  <img :src="item.src"><p>{{item.name}}</p>
                </div>

                <div class="back" :style="{transform:'rotateY('+item.backRotateY+'deg)'}">
                  <div class="des">
                    <p>{{item.description}}</p>
                  </div>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import AXIOS from '../axios/axios';
const Axios = new AXIOS();

export default {
  name: 'gallery',
  data () {
    return {
      photoArr:[
            {
                "id":0,
                "name":"无处安放的头发",
                "description":"拿什么跟你作比较才算特别，对你的感觉，强烈却又不太了解 只凭直觉",
                "src":"./static/image/0.jpg"
            },
            {
                "id":1,
                "name":"夏天",
                "description":"如果夏天有颜色一定是你的五彩缤纷",
                "src":"./static/image/1.jpg"
            },
             {
                "id":2,
                "name":"小破车",
                "description":"金车银车，最喜欢自己的小破车",
                "src":"./static/image/2.jpg"
            },
            {
                "id":3,
                "name":"满天星",
                "description":"我就知道你会踩我雷区，所以我提前把炸弹都换成了满天星。",
                "src":"./static/image/3.jpg"
            },
            {
                "id":4,
                "name":"我们",
                "description":"第一次看到宇宙，是和你四目相对的时候。",
                "src":"./static/image/4.jpg"
            },
            {
                "id":5,
                "name":"你",
                "description":"只有对你，我才能静下心来，仔细地去和一个人交谈，同时，也变得温柔。",
                "src":"./static/image/5.jpg"
            },
             {
                "id":6,
                "name":"玉子",
                "description":"你好呀，我是玉子。玉子的玉，玉子的子",
                "src":"./static/image/6.jpg"
            },
            {
                "id":7,
                "name":"油腻子",
                "description":"悲惨人生中的两个避难所，一是你，二是猫",
                "src":"./static/image/7.jpg"
            },
            {
                "id":8,
                "name":"看什么看",
                "description":"没错，万年不变的玉子，只能换个花样玩。",
                "src":"./static/image/8.jpg"
            },
             {
                "id":9,
                "name":"你和我",
                "description":"有美一人，婉如清扬",
                "src":"./static/image/9.jpg"
            },
            {
                "id":10,
                "name":"煮猫啦",
                "description":"救救我，铲屎的要煮了我",
                "src":"./static/image/10.jpg"
            }
        ],
      centerId:0
    }
  },
  mounted(){
    this.getPhotoArr(()=>{
          
          this.photoArr.forEach((item,index)=>{
            this.randomPos(item);
          });
        });
        
   },
  methods:{
    getPhotoArr(cal){
       let params = {
        // api: './static/photo.json',
        param: ''
      };
      
            this.photoArr= this.photoArr
            // console.log(this.photoArr)
            cal();
       
    },
    clickHandler(item){
      // console.log(this.photoArr)
      var curId=item.id;
      if(curId==this.centerId){
          this.overturn(item);
      }
      else{
          this.centerId=curId;
          this.photoArr.forEach((item,index)=>{
            if(item.id!=this.centerId){
              this.randomPos(item);
            if(item.frontRotateY==180)
              this.overturn(item);
            }
          });
      }
    },
    overturn(item){
      if(item.frontRotateY){
        if(item.frontRotateY==180){
          item.frontRotateY=0;
          item.backRotateY=180;
        }else{
          item.frontRotateY=180;
          item.backRotateY=0;
        }
      }else{
          this.$set(item,"frontRotateY",180);
          this.$set(item,"backRotateY",0);  
      }
    },
    random(j,k){                       
      return Math.floor(Math.random()*k)+j;
    },
    randomPos(item){ 
      if( typeof item.left == 'undefined' ){
          //Vue.set(product,"checked",true);  全局注册
          this.$set(item,"left",this.random(-130,document.body.offsetWidth-130)); //局部注册
          this.$set(item,"top",this.random(-170,document.body.offsetHeight-170)); 
          this.$set(item,"rotate",this.random(-90,90));
        }else{ 
          item.left=this.random(-130,document.body.offsetWidth-130);
          item.top=this.random(-170,document.body.offsetHeight-170);
          item.rotate=this.random(-90,90);
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

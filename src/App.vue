<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import wx from "weixin-js-sdk";
  export default {
    name: 'App',
    data(){
      return {
      
      }
    },
    mounted(){
     if(this.isWeixin()){ // 微信环境下禁用分享
        document.addEventListener('WeixinJSBridgeReady', function onBridgeReady() {
          // 通过下面这个API隐藏右上角按钮
          WeixinJSBridge.call('hideOptionMenu');
        });
      }
    },
    methods:{
      isWeixin() {
        var ua = navigator.userAgent.toLowerCase();
        if (ua.match(/MicroMessenger/i) == "micromessenger") {
            return true;
        } else {
            return false;
        }
      }
    },
  }
</script>

<style>
html,body{
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #303030;
  width: 100%;
  height: 100%;
  background-size: 100% 100%;
  background: #fbfdfc;
  margin: 0;
  padding: 0;
  -webkit-overflow-scrolling: touch;
}
body,h1,h2,h3,h4,h5,h6,div,dd,dt,dl,form,kbd,table,ul,li,marquee,hr,blockquote,ol,pre,fieldset,legend,button,input,textarea,th,td,p{font-size:12px; margin:0; padding:0; font-family: "微软雅黑",Arial, "宋体", Tahoma, Verdana,  Helvetica, sans-serif;}
address,cite,dfn,em,var{font-style:normal;}
button,input,select,textarea{font-size:100%; cursor:pointer}
input{ cursor:pointer}
table{border-collapse:collapse;border-spacing:0;}
ul,ol{list-style:none;}
img{border:0;width: 100%;}
ul{list-style:none;}
.clear{ clear:both;}
a{text-decoration: none; color: #666666; }
a:hover{ color:#000; text-decoration:none}
input[type="submit"],input[type="reset"],input[type="button"],input[type="text"], button { -webkit-appearance: none;border-radius: 0; } 

.clearfix:after { visibility: hidden; display: block; font-size: 0; content: " "; clear: both; height: 0; }
::-webkit-scrollbar {
  display: none; /* Chrome Safari */
  -ms-overflow-style: none; /* IE 10+ */
  scrollbar-width: none; /* Firefox */  
}
input::-webkit-input-placeholder { 
/* WebKit browsers */ 
  color: #adadad; 
} 
input:-moz-placeholder { 
/* Mozilla Firefox 4 to 18 */ 
  color: #adadad; 
} 
input::-moz-placeholder { 
/* Mozilla Firefox 19+ */ 
  color: #adadad; 
} 
input:-ms-input-placeholder { 
/* Internet Explorer 10+ */ 
  color: #adadad; 
}

</style>

<template>
  <div class="header">
    <div class="mainInf">
      <div class="avatar">
        <!-- 图片链接 v-bind 简写为: -->
          <img :src="seller.avatar" alt="">
      </div>
      <div class="content">
        <span class="title"></span>
        <!-- <span>{{goods.name[0]}}</span> -->
        <span class="name">{{seller.name}}</span>
        <div class="delivery">{{seller.description}}/{{seller.deliveryTime}}分钟饭就到啦</div>
        <!-- 要先用v-if判断是否存在 -->
        <div class="support" v-if='seller.supports'>
          <span class="icon"></span>
          <span>{{seller.supports[0].description}}</span>
        </div>
      </div>
      <div class="supportCount" v-if="seller.supports" @click="detailShow">
        <span class="count">{{seller.supports.length}}个&nbsp;&gt;</span>
      </div>
    </div>
    <div class="bulletin" @click="detailShow()">
      <span class="notice"></span><span class="butt_inf">{{seller.bulletin}}</span><span class="go_right">&gt;</span>
    </div>
    <div class="background">
      <img :src="seller.avatar" alt="">
    </div>
    <div v-if="showDetail" class="details" >
      <div class="datail-wrapper">
        <h1 class="name">{{seller.name}}</h1>
        <!-- 未解决 -->
        <!-- <star></star> -->
        <div class="spc_star">
          <span></span>
          <span></span>
          <span></span>
          <span></span>
        </div>
        <div class="spc_inf">
          <div class="line"></div>
          <div class="spc_text">优惠信息</div>
          <div class="line"></div>
        </div>
        <ul v-if="seller.supports" class="spc_spt">
          <li class="support-item" v-for="item in seller.supports">
            <span class="icon"></span>
            <span class="text">{{seller.supports[0].description}}</span>
          </li>

        </ul>
        <div class="spc_inf">
          <div class="line"></div>
          <div class="spc_text">商家公告</div>
          <div class="line"></div>
        </div>
        <div class="spc_bulletin">
          <p class="content">{{seller.bulletin}}</p>
        </div>

      </div>
      <div class="closeDetail" @click="hideDetail">X</div>
    </div>

  </div>

</template>

<script>
// import star from 'components/star/star'
  export default{
    // props 可以是数组或对象，用于接收来自父组件的数据。
    props: [
      'seller',
      'goods'
    ],
    data () {
      return {
        showDetail: false
      }
    },
    methods: {
      detailShow: function () {
        this.showDetail = true
      },
      hideDetail: function () {
        this.showDetail = false
      }
    },
    created: function () {
    }
  }

</script>

<style>
.clearfix {
  display: inline-block;
  *zoom:1;
}
.clearfix:after {
  content:".";
  display:block;
  height:0;
  visibility:hidden;
  clear:both;
}
.header{
  font-size: 0;
  width: 100%;
  height: 134px;
  color: rgb(255, 255, 255);
  background-color: rgba(7, 17, 27, 0.5);
  /*overflow: hidden;*/
}
.header .mainInf{
  height: 64px;
  width: 100%;
  padding:24px 12px 18px 24px;
  background-color: rgba(7, 17, 27, 0.5);
  position: relative;
}
.header .avatar{
  vertical-align: top;
}
.header .avatar, .avatar img{
  width: 64px;
  height: 64px;
  border-radius: 2px;
  display: inline-block;
}
.mainInf .content{
  display: inline-block;
  margin-left: 16px;
}
.mainInf .content .title{
  display: inline-block;
  width: 30px;
  height: 18px;
  background-size: 30px 18px;
  background-image: url('./img/brand@2x.png');
  background-repeat: no-repeat;
  vertical-align: top;
  margin-right: 6px;
}
.mainInf .content .name{
  font-size: 16px;
  line-height: 18px;
  font-weight: bold;
}
.mainInf .content .delivery{
  font-size: 12px;
  line-height: 12px;
  font-weight: 200;
  padding: 8px 0 10px 0;
}
.mainInf .support{
  font-size: 10px;
  line-height: 12px;
  font-weight: 200;
}
.support .icon{
  display: inline-block;
  width:12px;
  height: 12px;
  background-size: 12px 12px;
  background-image: url('./img/decrease_1@2x.png');
  background-repeat: no-repeat;
  vertical-align: top;
}
.supportCount{
  width: 42px;
  height: 24px;
  border-radius: 8px;
  position: absolute;
  left:310px;
  top: 60px;
  background-color: rgba(0, 0, 0, 0.2);
  font-size: 10px;
  line-height: 24px;
  text-align: center;
  /*display: inline-block;
  margin-right: 24px;
  margin-bottom: 60px;*/
}
.count{
  display: inline-block;
}
.header .bulletin{
  height: 28px;
  background-color: rgba(7, 17, 27, 0.2);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: 10px;
  line-height: 28px;
  font-weight: 200;
  padding: 0 22px 0 12px;
  position: relative;

}
.bulletin .notice{
  display: inline-block;
  width: 22px;
  height: 12px;
  background-image: url('./img/bulletin@2x.png');
  background-size: 22px 12px;
  background-repeat: no-repeat;
  vertical-align:top;
  margin-top: 8px;
}
.header .bulletin .butt_inf{
  margin: 0 4px;
  vertical-align: top;
}
.bulletin .go_right{
  position: absolute;
  display: inline-block;
  right: 12px;
}
.background{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height:134px;
  z-index: -1;
  filter: blur(10px);
}
.background img{
  width: 100%;
  height: 100%;
}
.details{
  width: 100%;
  /* sticky footer body设置最低高度为设备高度，同时设置flex,将main部分flex设置大于0，通常为1，将closeDetail部分设置高度，即可用内容撑起flex和整个页面/
  */
  min-height: 100%;
  overflow: auto;
  display: flex;
  flex-flow: column;
  background-color: rgba(7, 17, 27, 0.8);
  z-index: 100;
  position: absolute;
  top: 0;
  left: 0;
  /*只在ios上生效*/
  backdrop-filter:blur(10px);
  transition: all 0.5s;
}

/*.fade-transition{
  opacity: 1;
  background-color: rgba(7, 17, 27, 0.8);
}
.fade-enter, .fade-leave{
  opacity: 0;
  background-color: rgba(7, 17, 27, 0);
}*/

.datail-wrapper{
  flex: 1;
  margin-top: 64px;
}
.datail-wrapper h1{
  width: 100%;
  text-align: center;
  font-size: 16px;
  line-height: 16px;
  font-weight: 700;
}
.spc_star{
  width: 100%;
  text-align: center;
  height: 24px;
  margin: 16px auto 28px auto;
}
.spc_star span{
  display: inline-block;
  width: 15px;
  height: 15px;
  background-image: url("../star/img/star36_on@2x.png");
  background-repeat: no-repeat;
  background-size: 15px 15px;
  margin-right: 10px;
}
.spc_inf{
  width: 80%;
  margin: 30px auto;
  text-align: center;
  display: flex;
}
.spc_inf .line{
  /*background: blue;*/
  display: inline-block;
  flex: 1;
  vertical-align: top;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  position: relative;
  top: -6px;

}
.spc_inf .spc_text{
  font-size: 14px;
  line-height: 16px;
  font-weight: 700;
  padding: 0 12px;
}

/*  <ul v-if="seller.supports" class="spc_spt">
    <li class="support-item">
      <span class="icon"></span>
      <span class="text">{{seller.supports[0].description}}</span>
    </li>

  </ul>*/
.spc_spt {
  width: 80%;
  margin: 0 auto;
}
.spc_spt .support-item{
  padding: 0 12px;
  margin-bottom: 12px;
}
.spc_spt .support-item:last-child{
  margin-bottom: 0;
}
.spc_spt .support-item .icon{
  display: inline-block;
  width: 16px;
  height: 16px;
  vertical-align: top;
  background-size: 16px 16px;
  background-image: url("img/decrease_1@3x.png");
  background-repeat: no-repeat;
  margin-right: 6px;
}

.spc_spt .support-item .text{
  font-size: 12px;
  line-height: 12px;
  font-weight: 200;
}

.spc_bulletin {
  width: 80%;
  margin: 0 auto;
}
.spc_bulletin .content{
  padding: 24px 12px 0 12px;
  font-size: 12px;
  line-height: 24px;
  font-weight: 200;
}

.closeDetail{
  width: 100%;
  height: 6em;
  line-height: 6em;
  font-size: 32px;
  color: rgba(255, 255, 255, 0.5);
  text-align: center;
  /*background: red;*/
}
</style>

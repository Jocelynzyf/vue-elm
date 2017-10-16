<template>
  <div class="goods">
    <div class="menuWrapper" ref="menuWrapper">
      <ul>
        <li class="menu-item border-bottom-1px" v-for="item in goods">
             <span class="text">{{item.name}}</span>
         </li>
      </ul>
    </div>
    <div class="foodsWrapper" ref="foodsWrapper">
      <ul>
        <li class="food-list" v-for="item in goods">
          <h1 class="title">{{item.name}}</h1>
          <ul class="test">
            <li class="food-item border-bottom-1px" v-for="food in item.foods">
              <div class="food-icon">
                <img :src="food.icon" >
              </div>
              <div class="food-content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span class="count">月售{{food.sellCount}}份</span>
                  <span class="rate">好评{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span class="now">￥{{food.price}}</span>
                  <span class="old" v-if="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>

    </div>
  </div>
</template>

<script>
  import BScroll from 'better-scroll'
  export default{
    // define Errok = 0
    data () {
      return {
        goods: {},
        url: 'http://127.0.0.1:8888/goods.php?callback=getdata'
      }
    },
    created () {
      this.fetchData()
    },
    methods: {
      fetchData () {
        this.$http.jsonp(this.url).then(function (data) {
          this.goods = data.body
          this.$nextTick(() => {
            this._initScroll()
          })
          console.log(data)
        }, function (response) {
        })
      },
      _initScroll () {
        this.menuScroll = new BScroll(this.$refs.menuWrapper, {})
        this.foodsScroll = new BScroll(this.$refs.foodsWrapper, {})
      }
    }
  }
</script>

<style>
.border-1px{
    height:1px;
    background:#ccc;
    -webkit-transform: scaleY(0.5);
    -webkit-transform-origin:0 0;
    overflow: hidden;
}
.goods{
  display: flex;
  position: absolute;
  top:175px;
  bottom: 46px;
  width: 100%;
  overflow: hidden;
}
.menuWrapper{
  /*兼容*/
  flex: 0 0 80px;
  width: 80px;
  background: #faf5f7;
}

.menuWrapper .menu-item{
  display: table;
  height: 54px;
  width: 56px;
  line-height: 14px;
  font-size: 12px;
  padding: 0 12px;
}

.menuWrapper .icon{
  display: inline-block;
  width:12px;
  height: 12px;
  background-size: 12px 12px;
  background-image: url('./img/decrease_3@2x.png');
  background-repeat: no-repeat;
  vertical-align: top;
}
.menuWrapper .text{
  display: table-cell;
  width: 56px;
  height: 54px;
  vertical-align: middle;
  /*border: 1px rgba(7, 17, 27, 0.1);*/
  font-size: 12px;
}


.foodsWrapper{
  flex:1;
}
.foodsWrapper .title{
  display: inline-block;
  height: 26px;
  width: 100%;
  background: #f3f5f7;
  border-left: 2px solid #d9dde1;
  padding-left: 14px;
  font-size: 12px;
  line-height: 26px;
  color: rgb(147, 153, 159);
}
.foodsWrapper .food-item{
  display: flex;
  margin: 18px;
  padding-bottom: 18px;
}
/*如何去掉border问题：无法选取到last-child实验first-child可用*/
/*.border-bottom-1px:first-child::after{
  display: none;
}*/
.test .border-bottom-1px:last-child::after{
  display: none;
  margin-bottom: 0;
}
.food-item .food-icon{
  flex:0 0 57px;
  width: 57px;
  height: 57px;
}
.food-icon img{
  width: 57px;
  height: 57px;
}
.food-content{
  flex:1;
  margin-left: 10px;
}
.food-content .name{
  margin: 2px 0 8px 0;
  height: 14px;
  line-height: 14px;
  color: rgb(7, 17, 27);
}
.food-content .desc, .extra{
  font-size: 10px;
  line-height: 10px;
  color: rgb(143, 153, 159);
}
.food-content .desc{
  margin-bottom: 8px;
}
.extra .count{
  margin-right: 12px;
}
.price{
  font-weight: 700;
  line-height: 24px;
}
.price .now{
  margin-right: 8px;
  font-size: 14px;
  color: rgb(240, 20, 20);
}
.price .old{
  text-decoration: line-through;
  font-size: 10px;
  color: rgb(147, 153, 159);
}
</style>

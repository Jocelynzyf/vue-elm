<template lang="html">
<div class="shopcart">
  <div class="content">
    <div class="contentLeft">
      <div class="logoWrapper">
        <div class="logo">
          <img src="./img/cart10.png" alt="">
        </div>
        <div class="num">{{totalCount}}
        </div>
      </div>
      <div class="priceWrapper border-right-1px">
        <span class="price">￥{{totalPrice}}元</span>
      </div>
      <div class="del">
        还需配送费{{deliveryPrice}}元
      </div>
    </div>
    <div class="contentRight" :class="payClass">
      <div class="pay">
        {{payDesc}}
      </div>
    </div>
  </div>


</div>
</template>

<script>
export default {
  // 组件之间调用需要引用父组件的数据时候需要在父组件的router-view里调用，同时props调用之后才能输出
  // 其他组件输出的数据在此组件需要引用
  props: {
    selectFood: {
      // props是Array或者function时候default是一个函数
      type: Array,
      default () {
        return [
          {
            price: 10,
            count: 1
          }
        ]
      }
    },
    deliveryPrice: {
      type: Number,
      default: 0
    },
    minPrice: {
      type: Number,
      default: 0
    }
  },
  computed: {
    totalPrice () {
      let total = 0
      this.selectFood.forEach((food) => {
        total += food.price * food.count
      })
      return total
    },
    totalCount () {
      let count = 0
      this.selectFood.forEach((food) => {
        count += food.count
      })
      return count
    },
    payDesc () {
      let minPrice = this.minPrice
      if (this.totalPrice === 0) {
        return minPrice + '元起送'
        // return '还未开始购物'
      } else if (this.totalPrice < this.minPrice) {
        let diff = this.minPrice - this.totalPrice
        return '还差' + diff + '元起送'
      } else {
        return '去结算'
      }
    },
    payClass () {
      if (this.totalPrice < this.minPrice) {
        return 'not-enough'
      } else {
        return 'enough'
      }
    }
  }
}
</script>
<style lang="css">
.shopcart{
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 58px;
  font-size: 0;

}
.shopcart .content{
    display: flex;
    background-color: #141d27;
}
.contentLeft{
  flex: 1;
}
.logoWrapper, .priceWrapper, .del{
  display: inline-block;
}
.logoWrapper{
  width: 54px;
  height: 54px;
  margin: 0 18px;
  padding: 6px;
  background: #141d27;
  vertical-align: top;
  box-sizing: border-box;
  border-radius: 50%;
  position: relative;
  top: -10px;
}
.num{
  position: absolute;
  top:0;
  right: 0;
  width: 24px;
  height: 16px;
  line-height: 16px;
  text-align: center;
  border-radius: 10px;
  background: red;
  font-size: 9px;
  font-weight: 700;
  color: #fff;
  background: rgb(240, 20, 20);
  box-shadow: 0 4px 8px 0px rgba(0, 0, 0, 0.4);
}
.logo{
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  border-radius: 50%;
  background: #ccc;
  font-size: 24px;
  line-height: 24px;
  text-align: center;
}
.logo img{
  width: 80%;
  height: 80%;
}
.shopcart .priceWrapper{
  height: 100%;
  text-align: center;
  line-height: 58px;
}
.shopcart .priceWrapper .price{
  display: inline-block;
  font-size: 16px;
  color: rgba(255, 255, 255, 0.4);
  line-height: 24px;
  font-weight: 700;
  padding-right: 10px;
  /*vertical-align: top;*/
}
/*right-border 1px*/
.shopcart .border-right-1px::after{
  content:"";
  position: absolute;
  right: 0;
  bottom: 10%;
  width: 1px;
  height: 80%;
  transform-origin: 0 0;
  webkit-transform: scaleY(0.5);
  -webkit-transform-origin:0 0;
  overflow: hidden;
}
.shopcart .del{
  /*vertical-align: top;*/
  text-align: center;
  font-size: 10px;
  line-height: 24px;
  font-weight: 700;
  color: rgba(255,255,255,0.4);
  padding-left: 6px;
}
.contentRight{
  flex: 0 0 100px;
  width: 100px;
}
.contentRight .pay{
  height: 48px;
  line-height: 48px;
  text-align: center;
  font-size: 12px;
  font-weight: 700;
}
.not-enough{
  background: #2b333b;
  color: rgba(255, 255, 255, 0.4);
}
.enough{
  background: #00b43c;
  color: #fff;
}
</style>

<template>
  <div id="app">
    <vheader :seller='seller'></vheader>
    <div class="tab">
      <router-link to="/goods">商品</router-link>
      <router-link to="/seller">商家</router-link>
      <router-link to="/ratings">评分</router-link>
    </div>
    <div class="border-btm"></div>
    <router-view></router-view>
  </div>
</template>

<script>
import Header from '@/components/header/header'

export default {
  name: 'app',
  data () {
    return {
      seller: {},
      url: 'http://127.0.0.1:8888/seller.php?callback=getdata'
    }
  },

  created () {
    this.fetchData()
  },
  methods: {
    fetchData () {
      this.$http.jsonp(this.url).then(function (data) {
        this.seller = data.body
        // this.goods = data.body.goods
        // console.log(data)
        // console.log(this.seller)
      }, function (response) {
        // console.log(response)
      })
    }
  },
  components: {
    vheader: Header
  }
}

</script>

<style>
/**
 * Eric Meyer's Reset CSS v2.0 (http://meyerweb.com/eric/tools/css/reset/)
 * http://cssreset.com
 */
html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var,
b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, menu, nav, output, ruby, section, summary,
time, mark, audio, video, input {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font-weight: normal;
    vertical-align: baseline;
}

/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, menu, nav, section {
    display: block;
}
body {
    line-height: 1;
}
blockquote, q {
    quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
    content: none;
}
table {
    border-collapse: collapse;
    border-spacing: 0;
}
/* custom */
a {
    color: #7e8c8d;
    text-decoration: none;
    -webkit-backface-visibility: hidden;
}
li {
    list-style: none;
}
::-webkit-scrollbar {
    width: 5px;
    height: 5px;
}
::-webkit-scrollbar-track-piece {
    background-color: rgba(0, 0, 0, 0.2);
    -webkit-border-radius: 6px;
}
::-webkit-scrollbar-thumb:vertical {
    height: 5px;
    background-color: rgba(125, 125, 125, 0.7);
    -webkit-border-radius: 6px;
}
::-webkit-scrollbar-thumb:horizontal {
    width: 5px;
    background-color: rgba(125, 125, 125, 0.7);
    -webkit-border-radius: 6px;
}
html, body {
    width: 100%;
}
body {
    -webkit-text-size-adjust: none;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  font-size: 14px;
}
.tab{
  height: 100%;
  height: 40px;
  line-height: 40px;
  display: flex;
}
.tab a{
  flex: 1;
  text-align: center;
}
.router-link-exact-active, .router-link-active{
  color: rgb(240, 20, 20);
}
/*1px边框*/
.border-btm{
    height:1px;
    background:#ccc;
    -webkit-transform: scaleY(0.5);
    -webkit-transform-origin:0 0;
    overflow: hidden;
}
.border-1px, .border-bottom-1px, .border-top-1px, .border-left-1px, .border-right-1px {
   position: relative;
 }
/*线条颜色 黑色*/
.border-1px::after, .border-bottom-1px::after, .border-top-1px::after, .border-left-1px::after, .border-right-1px::after {
     background-color: #ccc;
}
 /*底边边框一像素*/
.border-bottom-1px::after {
     content:"";
     position: absolute;
     left: 0;
     bottom: 0;
     width: 100%;
     height: 1px;
     transform-origin: 0 0;
     -webkit-transform: scaleY(0.5);
     -webkit-transform-origin:0 0;
     overflow: hidden;
 }
</style>

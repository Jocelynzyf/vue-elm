<template lang="html">
  <div class="catControl">
    <div class="cat-dec" v-if="">
      -
    </div>
    <div class="cat-count">1
    </div>
    <div class="cat-add" @click="catAdd">
      <span>+</span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    food: {
      type: Object
    }
  }
}
</script>

<style lang="css">
.catControl{
  font-size: 0;
}
.cat-dec, .cat-count, .cat-add{
  display: inline-block;
}
.cat-dec, .cat-add{
  width: 16px;
  height: 16px;
  background: rgb(0, 160, 220);
  text-align: center;
  color: #fff;
  padding: 4px;
  border-radius: 50%;
  font-size: 14px;
  line-height: 16px;
  font-weight: 700;
}
.cat-count{
  font-size: 10px;
  line-height: 24px;
  color: rgb(147, 153, 159);
  width: 24px;
  text-align: center;
}
</style>

<template>
  <div>
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
  import Header from '@/components/header/Header';

  const ERR_OK = 0;

  export default {
    data () {
      return {
        seller: {}
      };
    },
    created () {
      this.$http.get('/api/seller').then((response) => {
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
        };
      });
    },
    components: {
      'v-header': Header
    }
  };
</script>

<style lang="sass" rel="stylesheet/sass">
  @import "./common/sass/mixin.sass"

  .tab
    display: flex
    width: 100%
    height: 40px
    .tab-item
      flex: 1
      text-align: center
      line-height: 40px
      @include border-1px(rgba(7, 17, 27, 0.1))
      a
        display: block
        font-size: 14px
        color: rgb(77, 85, 93)
        line-height: 40px
      .active
        color: rgb(240, 20, 20)
</style>

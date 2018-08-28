<template>
    <div>

 <div class="swipe-wrapper">
        <mt-swipe :auto="4000"  >
            <mt-swipe-item  v-for="item in recommends" :key="item.id">
              <a :href="item.linkUrl">
                <img class="swipe-img" :src="item.picUrl" alt="">
                </a>
              </mt-swipe-item>
        </mt-swipe>
  </div>        

  <div  class="recommend-list" v-for="item in tuijiangedan" :key="item.id">
    <div class="recommend-list-img"> <img v-lazy="item.imgurl"  ></div>
    <div class="recommend-list-content">
      <span>{{item.creator.name}}</span>
      <p>{{item.dissname}}   </p>
    </div>
  </div>
  
<button @click="loadMore()">加载更多</button>

    </div>  
</template>


<script>
import { getRecommend, getDiscList } from "@/api/recommend.js";
import { ERR_OK } from "@/api/config.js";
import { Toast } from "mint-ui";
import { Indicator } from "mint-ui";
import { MessageBox } from "mint-ui";
export default {
  data() {
    return {
      recommends: [],
      discList: [],
      tuijiangedan: [],
      indexPage: 1
    };
  },
  created() {
    this._getRecommend()
    this._getDiscList();
  },
  methods: {
    _getRecommend() {
      getRecommend().then(res => {
        // res对应的就是json对象，之前已经import该方法了
        if (res.code === ERR_OK) {
          // console.log(res.data.slider)

          this.recommends = res.data.slider;
        }
        console.log(this.recommends);
      });
    },
    _getDiscList() {
      getDiscList().then(res => {
        if (res.code === ERR_OK) {
          this.discList = res.data.list;
          this.tuijiangedan = this.discList.slice(0, 10 * this.indexPage);
        }
        console.log(this.tuijiangedan);
        if (this.tuijiangedan.length > 29) {
          Toast("已全部加载完毕");
        }
        Indicator.close();
      });
    },
    loadMore() {
      Indicator.open({
        text: "加载中...",
        spinnerType: "triple-bounce"
      });
      this.indexPage++;
      this._getDiscList(this.indexPage);
      console.log(this.indexPage);
    }
  }
}
</script>


 <style lang="stylus">
 .swipe-wrapper {
   width: 100%;
   height: 158px;
 }

 .swipe-img {
   width: 100%;
 }

 .mint-swipe-item {
   height: 11em;
 }

 .recommend-list {
   display: flex;
   justify-content: space-around;
   margin: 5%;
 }

 .recommend-list-img {
   width: 20%;
 }

 .recommend-list-img img {
   width: 100%;
 }

 .recommend-list-content {
   width: 70%;
   display: flex;
   flex-direction: column;
   text-align: left;
 }
</style>


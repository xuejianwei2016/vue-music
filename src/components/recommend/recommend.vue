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


    </div>  
</template>


<script>
import { getRecommend,getDiscList } from "@/api/recommend.js";
import { ERR_OK } from "@/api/config.js";
export default {
  data() {
    return {
      recommends: [],
      aa :[]
    };
  },
  created() {
    this._getRecommend(),
    this._getDiscList()
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
      })
    },
    _getDiscList(){
      getDiscList().then((res)=>{
        if(res.code === ERR_OK){
         this.aa = res.data;
        }
        console.log(this.aa)
      })
    }
  }
}
</script>


 <style lang="stylus">

 .swipe-wrapper 
   width: 100%
   height: 158px  
  .swipe-img
    width  : 100%


.mint-swipe-item{
  height 11em
}

    


</style>


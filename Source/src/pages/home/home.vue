<style>
/* body{
  background: white !important;
} */
.pic {
  position: absolute;
  z-index: -1;
  width: 100%;
  height: 100%;
  top: 0;
}
.top {
  position: fixed;
  z-index: 1;
  top: 0px;
  width: 100%;
}
</style>

<template>
  <div style="background-color:#eeeeee;">
    <!-- <mt-header  fixed title="首页" style="background-color:#FF4081"></mt-header> -->
    <!-- <div class="height-40"></div> -->

    <div style class="top">
      <div class style="position:relative;">
        <img :src="uploadpath+'resource/'+res.membertopbg" class="pic">

        <div class="padding-5 flex-row flex-center" @click="push('/mybaby',true)">
          <img :src="uploadpath+'resource/'+res.mybaby" class="icon-15">
          <div class="txt-bold">我的宝贝</div>
        </div>

        <div class="padding-5 txt-bold margin-left-20 h7">宝贝状态：</div>

        <div class="padding-5 txt-red flex-row flex-center">
          <div class="flex-1"></div>
          <div class="flex-4 h7-5 txt-bold">{{mybaby[0]!=null?mybaby[0].baby_name:"请立即添加您的宝贝"}}</div>
        </div>

        <div class="txt-red flex-row flex-center">
          <div class="flex-2"></div>
          <div class="flex-1">
            <img
              :src="uploadpath+  (mybaby[0]!=null?'baby/':'resource/')  + (mybaby[0]!=null? mybaby[0].baby_img:res.babyface)"
              class="icon-30 bg-white"
              style="border:2px solid white;border-radius:50%"
            >
          </div>
        </div>

        <div class="padding flex-row flex-center">
          <img :src="uploadpath+'resource/'+res.share" class="icon-10">
          <div class="txt-bold txt-white margin-left-10">跟宝妈奶爸一同分享好心情吧。</div>
        </div>
      </div>

      <div class="padding-10 bg-white" style="border-bottom:1px solid #eeeeee">
        <div class="txt-bold h7-5">宝贝心情周报：</div>
      </div>

      <div class="padding-5 flex-row flex-center bg-white" style>
        <div class="flex-row flex-column flex-1">
          <div>周日</div>
          <div class="margin-top-5">14</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周一</div>
          <div class="margin-top-5">15</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周二</div>
          <div class="margin-top-5">16</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周三</div>
          <div class="margin-top-5">17</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周四</div>
          <div class="margin-top-5">18</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周五</div>
          <div class="margin-top-5">19</div>
        </div>

        <div class="flex-row flex-column flex-1">
          <div>周六</div>
          <div class="margin-top-5">20</div>
        </div>
      </div>

      <div class="padding-left-20 padding-top-20">用片数量：0</div>

      <div class="padding-left-20 padding-top-10 flex-row flex-center">
        <div>当日评分：</div>
        <div class="flex-row flex-center">
          <img :src="uploadpath+'resource/'+res.star_yellow" class="icon-10">
          <img :src="uploadpath+'resource/'+res.star_gray" class="icon-10">
          <img :src="uploadpath+'resource/'+res.star_gray" class="icon-10">
          <img :src="uploadpath+'resource/'+res.star_gray" class="icon-10">
          <img :src="uploadpath+'resource/'+res.star_gray" class="icon-10">
        </div>
        <div class="margin-left-5">0分</div>
      </div>

      <div class="height-50"></div>

      <div class="text-center flex-row flex-column">
        <img :src="uploadpath+'resource/'+res.home_1" class="icon-50">
        <div class="margin-top-20 txt-bold">宝宝好给力会自己换尿布了</div>
        <div class="height-30"></div>
        <mt-button class="h8" @click="chakan" style="width:50%;height:30px" type="primary">查看宝宝实时情况</mt-button>
      </div>
      
    </div>

    
  </div>
</template>

<script>
import { AppBase } from "../../app/AppBase";

class Content extends AppBase {
  constructor() {
    super();
  }

  // takeP(){
  //   this.takePhoto((src)=>{
  //     this.photo=src;
  //   });
  // }

  // getPhoto(){
  //   this.choosePhoto((src)=>{
  //     this.photo=src;
  //   });
  // }

  setData(data) {
    data.mybaby = "";

    return data;
  }
  chakan() {
    console.log(this.mybaby[0]);
    if (
      this.mybaby[0] == "" ||
      this.mybaby[0] == undefined
    ) {
      this.info("请选择宝贝");
    } else {
      this.mybaby[0] == undefined
       if(this.mybaby[0].baby_equipment ==''||this.mybaby[0].baby_equipment =='')
       {
this.info("请绑定设备");

       }
       else{this.pushParam("realtimedata", { id: this.mybaby[0].id,xh:this.mybaby[0].nbxh});}

      
    }
  }
  onMyLoad() {}

  onMyShow() {
    this.post("news", "thisbaby", { member_id: this.MemberInfo.id }).then(
      ret => {
        this.mybaby = ret;
      }
    );
  }

  // upload(){
  //   this.uploadFile(this.photo,"member",(filename)=>{
  //     this.afphoto=filename;
  //   })
  // }
}

var content = new Content();
var body = content.generateBodyJson();
body.methods.chakan = content.chakan;
// body.methods.takeP=content.takeP;
// body.methods.upload=content.upload;

export default body;
</script>

<template>
<div class="reviewList">
  <div class="grey"></div>
  <div v-for="(items, index) in reviewList" :key="index" class="items">
    <div class="content">
      <div class="content_top">
        <div class="top_left">
          <div class="left_btn1">审批假条</div>
          <div class="left_btn2">外出考试</div>
        </div>
        <div class="top_right">
          详情>
        </div>
      </div>
      <div class="content_flex">
        <div class="content_left">
          <p>有效时间：{{GetNumberOfDays(items.beginTime,items.endTime)}}天</p>
          <p>创建时间：{{items.dataTime}}</p>
          <p>申请人：{{items.applicant}}</p>
          <p>审核人：{{items.reviewed}}</p>
          <p>学院：{{items.college}}</p>
          <p>班级：{{items.className}}</p>
        </div>
        <div class="content_right">
          <img v-if="items.status" class="greenImg" src="../assets/agree.png" alt="">
          <img v-else class="greenImg" src="../assets/backAgree.png" alt="">
          <div class="buttonArea">
            <div v-if="items.status" class="btn green-btn" @click="changeStatus(index)">确认离校</div>
            <div v-else class="btn orange-btn">确认返校</div>
          </div>
        </div>
      </div>
      </div>

    <div class="grey" style="height: 30px"></div>
  </div>
  <button @click="backForm">回到修改页面</button>
</div>
</template>

<script>
export default {
  name: "reviewList",
  emits: ['showFormArea'],
  data(){
    return{
      reviewList:{},
      status: true
    }
  },
  mounted() {
    this.reviewList = this.$parent.list
    console.log('reviewList',this.reviewList)
  },
  methods:{
    backForm(){
      this.$emit('showFormArea')
    },
    showData(){
      console.log('$parent',this.$parent.list)
    },
    GetNumberOfDays(date1,date2){//获得天数
    //date1：开始日期，date2结束日期
    let a1 = Date.parse(new Date(date1));
    let a2 = Date.parse(new Date(date2));
    return parseInt((a2-a1)/ (1000 * 60 * 60 * 24));//核心：时间戳相减，然后除以天数
    },
    changeStatus(index){
      // 切换图片状态
      this.reviewList[index].status = false
      this.$parent.list[index].status = false
    }
  }
}
</script>

<style scoped>
.grey{
  background: #f3f1f4;
  width: 100%;
  height: 15px;
}
.reviewList{
  position: fixed;
  width: 100%;
  height: 100%;
  background: rgb(243, 241, 244);
}
.items{
  box-sizing: border-box;
  padding: 0 15px;
}
.content{
  background: #fff;
  border-radius: 8px;
  padding: 15px;
}
.content_flex{
  display: flex;
  justify-content: space-between;
}
.content_top{
  display: flex;
  height: 35px;
  justify-content: space-between;
  border-bottom: 1px solid #F0F1F3;
}
.top_left{
  width: 155px;
  display: flex;
  justify-content: space-between;
}
.left_btn1{
  width: 70px;
  height: 25px;
  font-size: 14px;
  color: white;
  background: #56BF6A;
  border-radius: 2px;
}
.left_btn2{
    width: 70px;
    height: 25px;
    font-size: 14px;
    background: white;
    color: #7EC14F;
    border: 1px solid #7EC14F;
    border-radius: 3px;
}
.content_left{
  text-align: left;
}
.content_left p{
  font-size: 14px;
  margin: 8px 0;
}
.greenImg{
  right: -8px;
  top: 0;
  width: 130px;
  height: 130px;
}
.buttonArea{
  padding-left: 40px;
}
.btn{
  text-align: center;
  color: #fcfcfc;
  width: 65px;
  height: 30px;
  line-height: 30px;
  font-size: 13px;
  border-radius: 5px;
  border: 0;
}
.back-btn {
  background: #8e929b;
}
.lightblue-btn {
  background: #a2cefd;
}
.green-btn{
  background: #7EC14F;
}
.orange-btn{
  background: #E6A142;
}
</style>
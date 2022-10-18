<template>
  <div class="grey"></div>
  <div class="formData">
    <div class="items">
      创建假条日期:<input class="ml20" type="date" v-model="formData.dataTime" />
    </div>
    <div class="items">
      申请人:<input class="ml20" type="text" v-model="formData.applicant" />
    </div>
    <div class="items">
      审核人:<input class="ml20" type="text" v-model="formData.reviewed" />
    </div>
    <div class="items">
      所属学院:<input class="ml20" type="text" v-model="formData.college" />
    </div>
    <div class="items">
      班级:<input class="ml20" type="text" v-model="formData.className" />
    </div>
    <div class="items">
      有效日期:<input class="ml20" type="date" v-model="formData.beginTime" />-<input type="date" v-model="formData.endTime" />
    </div>
    <div class="buttonArea">
      <div class="btn" @click="submitForm">提交</div>
      <div class="btn" @click="jumpToReview">查看假条</div>
      <div class="btn" @click="clearList">清除记录</div>
    </div>
  </div>
  <div class="grey"></div>
  <div class="tips">
    <p>左上角的返回键才能保存记录</p>
    <p>本工具仅限学习交流使用，切勿用于违反校方规定行径，所产生的不良后果与本人无关，在使用此工具的时候视为默认您同意此条例</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      formData:{
        dataTime:'',
        applicant:'张三',
        reviewed:'李四',
        college:'信息工程学院',
        className:'xx年xx班',
        beginTime:'',
        endTime:'',
        status:true
      }
    }
  },
  emits: ['showList'],
  methods:{
    submitForm(){
      this.$parent.list = [...this.$parent.list,JSON.parse(JSON.stringify(this.formData))]
      console.log(this.formData,'list',this.$parent.list)
      this.jumpToReview()
    },
    jumpToReview(){
      this.$emit('showList')
    },
    clearList(){
      this.$parent.list = []
      console.log('清除后的list',this.$parent.list)
    }
  }
}
</script>
<style scoped>
.formData{
  padding: 15px 1.25rem;
  position: relative;
}
.items{
  margin: 15px 0;
  display: flex;
  justify-content: left;
}
.ml20{
  margin-left: 20px;
}
.buttonArea{
  display: flex;
  justify-content: space-around;
}
.btn{
  background: #4ea4ff;
  color: #fcfcfc;
  width: 100px;
  height: 40px;
  line-height: 40px;
  border-radius: 5px;
  border: 0;
}
.grey{
  background: #f3f1f4;
  width: 100%;
  height: 15px;
}
.tips{
  text-align: left;
}
</style>

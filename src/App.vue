<template>
  <div>
    <div class="title">
      <a href="#/"><img class="backImg" @click="showVisible" src="./assets/arrow_left.png" alt=""></a>
      <div class="titleName">online-leave</div>
    </div>
    <HelloWorld v-if="showForm" @showList="showVisible"/>
    <ReviewList v-else @showFormArea="showVisible"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ReviewList from "./components/reviewList.vue";
export default {
  name: 'App',
  data(){
    return{
      showForm: true,
      list:[]
    }
  },
  components: {
    HelloWorld,
    ReviewList
  },
  methods:{
    showVisible(){
      this.showForm = !this.showForm
    }
  }
}
</script>
<style scoped>
*{
  margin: 0;
  box-sizing: border-box;
}
.title{
  box-sizing: border-box;
  position: relative;
  padding: 15px 0.5rem;
  width: 100%;
  text-align: center;
  display: flex;
  background: #6CB1F4;
  justify-content: flex-start;
}
.backImg{
  width: 20px;
  height: 25px;
}
.titleName{
  display: inline-block;
  color: white;
  font-family: -apple-system,BlinkMacSystemFont,Segoe UI,Roboto,Oxygen,Ubuntu,Cantarell,Open Sans,Helvetica Neue,sans-serif;
  font-weight: 500;
  margin: 0;
}
</style>

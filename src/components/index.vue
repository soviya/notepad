<template>
    <div>
      <div class="title">记事本</div>
      <div class="main">
        <input class="input" type="text" v-model.trim="inputValue" @keyup.enter="add" placeholder="请按回车添加待办事项">
        <ul class="list">
          <li v-for="(item,index) in list" :key="index">
            <div class="index">{{index+1}}、</div>
            <div class="msg">{{item}}</div>
            <div class="delete" @click="deleteFn(index)"><img :src="deleteImg" alt=""></div>
          </li>
        </ul>
        <div class="bottom" v-if="this.list.length!=0">
          <div class="num">{{list.length}} 个待办项目</div>
          <div class="clear" @click="clear">clear</div>
        </div>
        <div class="prompt" v-if="repeat">
          <div class=prompt-title>提示</div>
            {{this.promptTxt}}
            <div class="close" @click="close">关闭</div>
        </div>
      </div>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      list:[
      ],
      inputValue:"",
      deleteImg:require('../assets/images/delete.png'),
      repeat:false,
      promptTxt:''
    }
  },
  methods: {
    add:function(){
      if(this.list.indexOf(this.inputValue)===-1&&!!this.inputValue){
        this.list.push(this.inputValue);
        this.inputValue="";
      }else{
        if(this.list.indexOf(this.inputValue)!==-1){
          this.promptTxt="请勿输入重复待办事项，请重新输入"
          this.repeat=true;
        }
        if(!this.inputValue){
          this.promptTxt="待办事项不能空，请重新输入"
          this.repeat=true;
        }
        
      }
      
    },
    deleteFn:function(index){
      this.list.splice(index,1)
    },
    clear:function(){
      this.list.splice(0,this.list.length);
    },
    close:function(){
      this.repeat=false;
    }
  }
}
</script>
<style scoped>
*{
  margin:0px;padding:0px;
}
@font-face {
  font-family: 'title';
  src: url('../assets/font/潮字社风云简.ttf');
}
@font-face {
  font-family: 'index';
  src: url('../assets/font/BassetBold.ttf');
}
@font-face {
  font-family: 'msg';
  src: url('../assets/font/字在如风.ttf');
}
.title{
  font-family: 'title';
  font-size:60px;
}
.input{
  width:400px;
  height: 50px;
  line-height: 50px;
  padding:0 10px;
  box-sizing:border-box;
  border-radius: 6px;
  border:1px solid #dedede;
  outline: none;
  margin: 20px 0px;
}
.index{
  font-family: 'index';
  font-size:22px;
}
.list,
.bottom{
  width:400px;
  margin:0 auto;
}
.list li{
  display: flex;
  padding:10px 0px;
  border-bottom:dashed 1px #dedede;
  align-items: center;
}
.msg{
  font-family: 'list';
  font-size:22px;
  flex:1 0 100px;
}
.delete,
.delete img{
  width:16px;
  height:16px;
}
.clear,
.delete,
.close{
  cursor: pointer;
}
.bottom{
  display: flex;
  justify-content:space-between;
  padding-top: 10px;
}
.prompt{
  width:250px;
  height:120px;
  border-radius: 10px;
  left:50%;
  top:150px;
  position: absolute;
  margin-left:-125px;
  text-align: center;
  background:#f2f2f2;
  color:#333;
  font-size:13px;
}
.prompt-title{
  height:30px;
  width:100%;
  line-height: 30px;
  background:#dedede;
  border-radius:10px 10px 0 0 ;
  margin-bottom: 20px;
  font-size:15px;
}
.close{
  float:right;
  margin-top:30px;
  margin-right: 20px;
  font-size:12px;
  background:#dedede;
  padding:2px 5px;
  border-radius: 2px;
}
</style>

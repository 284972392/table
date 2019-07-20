<template>
    <div class="test">
      <div>
        <input type="text" v-model="searchData" class="input" placeholder="搜索">
        <button @click="search"> 搜索</button>
      </div>
      
      <table border="1" width='500' ref="selection">
         <tr>
           <td>
            <input type="checkbox" name="Checkbox" class="check"  style="float:none;height:auto;" v-model="checked" @click="checkedAll">
           </td>
          <td v-for="(item,index) in topList" :key="item.key">
            <span class="caret-wrapper"><i class="sort-caret ascending"></i><i class="sort-caret descending"></i></span>
            {{item.title}}
          </td>
       </tr>
        <tr v-for="(data,index) in tableData" :key="index">
          <td>
             <input type="checkbox" name="Checkbox" class="check"  style="float:none;height:auto;" v-model="checkList" :value="data.id">
          </td>
          
            <td v-for="(value,key,index) in data" v-if="data[keys[index]]" :key="index+'nn'">
             {{data[keys[index]]}}
            </td>
        </tr>
         <tr>

        </tr>

  

      </table>

       <div class="footer">
          <span>共：{{total}}条数据</span>
          <span>当前第{{pageNum}}
            <select @change="setPage" v-model="setPageNum">
              <option v-for="data in dateOption" :value='data'>{{data}}</option>
            </select>
            页
          </span>
          <button type="button"  class="btn-prev" @click="lastPage"><i class="el-icon el-icon-arrow-left"></i></button>
          <button type="button"  class="btn-next" @click="nextPage"><i class="el-icon el-icon-arrow-right"></i></button>
          <p>前往</p>
          <input type="text" v-model="goPageNum" @keyup.enter='goPage' >
          页  
        </div>
     

    </div>
</template>

<script>

export default {
  props: {
    tableData: {
      type: Array,
      default: ()=>[]
    },
    headLabel:{
      type: Array,
      default: ()=>[]
    },
    total:{
      // 总共几条数据
      type:Number,
      default:0
    },
    pageSize:{
      type:Number,
      default:1
    }
 
  },
  name: 'table',
  data() {
    return {
        checked:false,//全选按钮
        checkList:[],//勾选列表
        goPageNum:null,
        pageNum:1,//当前页数
        searchData:null,
        list:this.tableData,//表数据
        totals:this.total,//总数据量
        topList:this.headLabel,//头部展示信息
        keys:[],
        dateOption:[],
        setPageNum:1,//选择的页码
    }
  },
  
  methods: {
      lastPage(){
        this.$emit('lastPage')
      },
      nextPage(){
        this.$emit('nextPage')
      },
      search(){
       
      },
      goPage(){
        if(this.goPageNum){
          this.$emit('goPage',this.goPageNum)
        }  
      },
      checkedAll() {
        // 全选
          if (this.checked) {
            this.checkList = [];
          } else {
            this.checkList = [];
            this.list.map((item, index)=>{
            
            this.checkList.push(item.id);
            
            });
          }
    },
    setPage(){
      this.$emit('goPage',this.setPageNum)
    }
   
  },
  watch:{
     'checkList': {
      handler: function(val, oldVal) {
        if (val.length === this.list.length) {
          this.checked = true;
        } else {
          this.checked = false;
        }
      },
      deep: true
    },
    
  },
  created() {
   
  },
  beforeMount() {
    for(var a in this.topList){
      this.keys.push(this.topList[a].key)
    }
    this.dateOption = []
    let onum = Math.ceil(this.total/this.pageSize);
    for(let i=1;i <= onum;i++){
      this.dateOption.push(i)
    }


  },
  mounted(){
   

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less" scoped>
    .test{
      margin-top: 100px;
      height: 500px;
      width: 80%;
    }
    .input{
      margin: 20px;
    }
    .footer{
      width: 70%;
      display: flex;
      align-items: center;
     
      margin-top: 20px;
      span{
        margin-right: 50px;
      }
      button{
        margin: 0 5px;
      }
      input{
        width: 60px;
        margin: 0 5px;
      }
      p{
        margin-left: 10px;
      }
    }
</style>

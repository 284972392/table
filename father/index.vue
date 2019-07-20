<template>
    <div>
		<tabletest :tableData='tableData' :total='total' :pageSize='pageSize' :headLabel='headLabel' @lastPage='lastPage' @nextPage='nextPage' @goPage='goPage($event)'></tabletest>
    </div>
</template>

<script>
	import tabletest from '../tabletest'
    export default {
		components:{
			tabletest
		},
        name:'inform',
        data(){
        	return{
				pageSize:4,
				total:9,
				 headLabel:[
					 {title:'时间',key:'date'},
					 {title:'地址',key:'address'},
					 {title:'名字',key:'name'}
				 ],
				 tableData: [{
						date: '2016-05-02',
						name: '王小虎',
						address: '上海市普陀区金沙江路 1518 弄',
						id:'121'
					}, {
						date: '2016-05-04',
						name: '王小虎',
						address: '上海市普陀区金沙江路 1517 弄',
						id:'32132'
					}, {
						date: '2016-05-01',
						name: '王小虎',
						address: '上海市普陀区金沙江路 1519 弄',
						id:'32121'
					}, {
						date: '2016-05-03',
						name: '王小虎',
						address: '上海市普陀区金沙江路 1516 弄',
						id:'3224'
       		   }],
        	}
        },
        methods:{
			lastPage(){
				console.log('lastPage')
			},
			nextPage(){
				console.log('nextPage')
			},
			goPage(num){
				console.log(num)	
			},
    },
       mounted(){
      
       }
     }
</script>

<style scoped lang="scss">

</style>
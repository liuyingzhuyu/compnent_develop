<template>
    <div>
      <button type="primary" @click="handleClick">改变所选</button>
      <button type="primary" @click="handleClick2">获取所选</button>
      <button type="primary" @click="disabled = !disabled">是否可用</button>
      <checkbox :selectArr="selectArr" @change="change" :list='list' :disabled="disabled"></checkbox>
    </div>
</template>
<script>
import  checkbox from './checkbox'
export default {
    layout: 'prient',
  components: {
    checkbox
  },
  computed: {

  },
  data() {
    return{
      disabled:true,
      selectArr: ['1','3'],
      list : [
        {
          label: '反馈感觉',
          value: '1',
        },
         {
          label: '环境规划法规',
          value: '2',
        },
         {
          label: '发鬼地方',
          value: '3',
        },
         {
          label: '和根据钢结构',
          value: '4',
        },
         {
          label: '个任务而无法',
          value: '5',
        }
      ]
    }
  },
  methods:{
    handleClick2(){
        console.log(this.selectArr,'获取数据')
    },
    handleClick(){
      this.selectArr  = ['1','3']
      // 随机选中
      // this.selectArr = []
      // this.list.map(i=>{
      //   if(Math.random()>0.5 ){
      //     this.selectArr.push(i.value)
      //   }
      // })
      console.log(this.selectArr,'按钮改变')
    },
  	change(val){
  		this.selectArr = val
  	}
  }
}
</script>
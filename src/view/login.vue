<template>
  <div>
    测试111
  </div>
</template>
<script>
import { List } from 'vant'
export default {
  data(){
    return{
      
    }
  },
  mounted(){
    this.getInfo()
  },
  methods:{
    async getInfo(){
      let b=  await this.menList();
      console.log(b);
      let a =  await this.list();
      console.log(a)
      console.log(123)
    },
    
    list(){
        return new Promise ((resolve,reject)=>{
          this.$axios.get('https://meituan.thexxdd.cn/api/forshop/getprefer').then((result) => {
            resolve(result.data)
          })
        })
    },

    menList(){
      return new Promise((resolve,reject)=>{
        setTimeout(() => {
          resolve('哈哈哈哈哈')
        }, 3000);
      })
    }
  }
}
</script>
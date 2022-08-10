<template>
  <div id="app">
    <div class="container">
      <div class="header">
        <input type="text" v-model="keyword">
        <div class="match-num">{{ currentIdx }} / {{ matchCount }}</div>
        <button @click.stop="searchLast">上一个</button>
        <button @click.stop="searchNext">下一个</button>
      </div>
      <search-highlight
        class="search-highlight"
        ref="search"
        @current-change="currentChange"
        @match-count-change="matchCountChange"
        :content="content"
        regExp
        :keyword="keyword">
      </search-highlight>
    </div>
  </div>
</template>
 
<script>
import SearchHighlight from '@/components/SearchHighlight.vue'
 
export default {
  name: 'app',
  components: {
    SearchHighlight
  },
  data () {
    return {
      keyword: '明月',
      currentIdx: 0,
      matchCount: 0,
      content:'',
      list1:'<div class="title">流行病学</div><p>肾细胞癌(Renal cell carcinoma，RCC) 简称肾癌，是源于肾小管上皮的恶性肿瘤，占肾脏恶性肿瘤的80%～90%。在世界范围内，RCC的发病率占成人恶性肿瘤的2%～3%，分布有明显地域差异，北美、西欧等国发病率最高。发病可见于各年龄段，高发在50～70岁，男女比例约为2:1。据GLOBOCAN 2020统计，全球RCC发病率居恶性肿瘤第14位，死亡率居第15位。年龄标化发病率男性6.1/10万，女性3.2/10万。年龄标化死亡率男性4.6/10万，女性1.8/10万。据2019中国肿瘤登记数据显示，2016年肿瘤登记地区肾及泌尿系统不明癌居全部癌症发病第17位，最常见为RCC，占77.38%。肿瘤登记地区RCC发病率为4.02/10万，男性（5.15/10万）高于女性（2.86/10万），城市（5.17/10万）高于农村（2.86/10万）。肾及泌尿系统不明癌居全部癌症死亡第18位。登记地区RCC死亡率为1.37/10万，男性（1.79/10万）高于女性（0.94/10万），城市（1.77/10万）高于农村（0.96/10万）。</p>'
    }
  },
  mounted () {
    let keywords = [];
    this.content = this.list1;
    const map = [...'\\[](){}?.+*^$:|'].reduce((r, c) => (r[c] = true, r), {})
    keywords = keywords.filter(word => word).map(word => {
      return word.split('').map(s => map[s] ? `\\${s}` : s).join('')
    })
    this.keyword = keywords.join('|')
  },
  methods: {
    searchLast () {
      this.$refs.search.searchLast()
    },
    searchNext () {
      this.$refs.search.searchNext()
    },
    matchCountChange (count) {
      this.matchCount = count
    },
    currentChange (idx) {
      this.currentIdx = idx
    },
  }
}
</script>
 
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
}
body {
  margin: 0;
}
 
</style>
 
<style>
 
.container {
  width: 100%;
  box-sizing: border-box;
  margin: 0 auto;
}
 
.header {
  width: 100%;
  text-align: center;
  display: flex;
  height: 40px;
  align-items: center;
  flex-shrink: 0;
  flex-wrap: wrap;
  text-align: center;
  margin-top: 30px;
}
.header input{
    margin-left: 14vw;
    border: 1px solid #555;
    border-radius: 10px;
    height: 40px;
    margin-right: 10px;
} 
button {
  margin: 0 2px;
  flex-shrink: 0;
  background: gold;
  color: #fff;

}
.search-highlight {
  width: 90%;
  margin: 0 auto;
  white-space: pre-line;
  overflow: auto;
  line-height: 2;
  text-align: left;
}
.title{
    color: orange;
    font-size: 18px;
    text-align: center;
    margin-top: 30px;
}
</style>
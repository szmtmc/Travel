<template>
  <div>
    <detail-header :title="title"></detail-header>
    <Detail-Main :mainList="mainList"></Detail-Main>
  </div>
</template>
<script>
import DetailHeader from './components/Header'
import DetailMain from './components/Main'

import axios from 'axios'
import url from '../../common/api'
export default {
  name: 'wDetail',
  data () {
    return {
      title: '',
      mainList: []
    }
  },
  components: {
    DetailHeader, DetailMain
  },
  mounted () {
    this.getTitle()
    this.getMain()
  },
  methods: {
    getTitle () {
      var formData = new FormData()
      formData.append('id', this.$route.params.id)
      axios.post(url.weenkendTitle, formData).then(res => {
        this.title = res.data[0].title
      })
    },
    getMain () {
      if (localStorage.cityId === '270') {
        axios.post(url.weekendDetailgz).then(res => {
          this.mainList = this.randArr(res.data)
        })
      }
      if (localStorage.cityId === '264') {
        axios.post(url.weekendDetailcs).then(res => {
          this.mainList = this.randArr(res.data)
        })
      }
    },
    randArr (arr) {
      return arr.sort(() => {
        return (Math.random() - 0.5)
      })
    }
  },
  watch: {
    // 利用watch方法检测路由变化：
    '$route': function (to, from) {
      // 拿到目标参数 to.query.id 去再次请求数据接口
      if (to.name === 'wDetail') {
        this.getTitle()
        this.getMain()
      }
    }
  }
}
</script>
<style lang="stylus" scoped></style>

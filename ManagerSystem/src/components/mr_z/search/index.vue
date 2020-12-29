<!--查询组件、自定义查询名称以及数组功能，也有重置和导出Excel功能-->
<template>
  <div>
    <el-form :model="filterThings.value">
      <span v-for="(item,index) in filterThings" :key="index">{{ item.type }}<el-input v-model="item.input" autocomplete="off" /></span>

      <el-button type="primary" @click="search">查询</el-button>
      <el-button type="plain" @click="comeback">重置</el-button>
      <el-button type="success" @click="getExcel(doneFilters)">导出EXCEL</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  name: 'Index',
  props: {
    tableData: {
      type: Array,
      default: () => {
        return [{
          date: '2016-05-02',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
          login: '2020-11-26 16:09:28',
          charge: ['王大帅', '赵天才'],
          tag: '家'
        }, {
          date: '2016-05-04',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄',
          login: '2020-11-24 17:04:28',
          charge: ['王大帅', '赵天才'],
          tag: '公司'
        }, {
          date: '2016-05-01',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄',
          login: '2020-11-20 14:48:39',
          charge: ['王大帅', '赵天才'],
          tag: '家'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄',
          login: '2020-11-20 14:48:39',
          charge: ['王大帅', '赵天才'],
          tag: '公司'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄',
          login: '2020-11-20 14:48:39',
          charge: ['王大帅', '赵天才'],
          tag: '公司'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄',
          login: '2020-11-20 14:48:39',
          charge: ['王大帅', '赵天才'],
          tag: '公司'
        }, {
          date: '2016-05-03',
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄',
          login: '2020-11-20 14:48:39',
          charge: ['王大帅', '赵天才'],
          tag: '公司'
        }]
      }
    }
  },
  data() {
    return {
      formLabelWidth: '60px',
      filterThings: [
        { type: 'date', input: '' },
        { type: 'name', input: '' },
        { type: 'address', input: '' },
        { type: 'tag', input: '' },
        { type: 'startTime', input: '' },
        { type: 'endTime', input: '' }
      ],
      doneFilters: this.tableData
    }
  },
  methods: {
    search() {
      // console.log('hahahah')
      const realthings = this.filterThings.filter(item => {
        return item.input.length !== 0
      })
      this.doneFilters = this.tableData.filter((item, check) => {
        return realthings.every(function(value) {
          if (value.type === 'startTime' || value.type === 'endTime') {
            const checkTime = (new Date(item.login).getTime() >= new Date(realthings[0].input).getTime()) || (item.login <= new Date(realthings[1].input).getTime())
            return checkTime
          } else {
            return (item[value.type].indexOf(value.input) !== -1)
          }
        })
      })
      // console.log(ha)
      this.$emit('searchDone', this.doneFilters)
      // this.tableData = doneFilters
      // this.pageCUt()
    },
    comeback() {
      this.doneFilters = this.tableData
      this.$emit('searchReborn')
    },
    getExcel(res) {
      require.ensure([], () => {
        const { export_json_to_excel } = require('../../../utils/Export2Excel.js')
        const tHeader = ['登录账号', '真实姓名', '联系方式', '登录时间', '状态']
        const filterVal = ['date', 'name', 'address', 'login', 'tag']
        const list = res
        const data = this.formatJson(filterVal, list)
        export_json_to_excel(tHeader, data, '用户管理情况表')
      })
    },

    formatJson(filterVal, jsonData) {
      return jsonData.map(v => filterVal.map(j => v[j]))
    }
  }
}
</script>

<style scoped>
.el-input {
  margin-top: 5px;
  width: 120px;
}
</style>

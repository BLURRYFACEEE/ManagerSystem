<template>
  <div class="birthHold">
    <div class="cloth">
      <header>
        <el-row :gutter="48">
          <el-col :span="6">
            <el-card shadow="hover" style="position: relative">
              <img src="http://chuantu.xyz/t6/741/1608631167x1033348159.png">
              <div class="typeAclass" />
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card shadow="hover" style="position: relative">
              <img src="http://chuantu.xyz/t6/741/1608631167x1033348159.png">
              <div class="typeAclass" />
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card shadow="hover" style="position: relative">
              <img src="http://chuantu.xyz/t6/741/1608631167x1033348159.png">
              <div class="typeAclass" />
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card shadow="hover" style="position: relative">
              <img src="http://chuantu.xyz/t6/741/1608631167x1033348159.png">
              <div class="typeAclass" />
            </el-card>
          </el-col>
        </el-row>
      </header>
      <section>
        <div class="headerAchartsmove">
          <div id="headerEchart" />
        </div>
        <div class="threeDetailCharts">
          <el-row :gutter="24">
            <el-col :span="8">
              <el-card id="detailCharts1" shadow="hover" style="position: relative" />
            </el-col>
            <el-col :span="8">
              <el-card id="detailCharts2" shadow="hover" style="position: relative" />
            </el-col>
            <el-col :span="8">
              <el-card id="detailCharts3" shadow="hover" style="position: relative" />
            </el-col>
          </el-row>
        </div>
      </section>
      <footer class="orderAtoAtalk">
        <el-row :gutter="8">
          <el-col :span="12">
            <el-card id="detailCharts4" shadow="hover" style="position: relative">
              <el-table
                ref="filterTable"
                :data="tableData"
                style="width: 100%"
              >
                <el-table-column
                  prop="date"
                  label="Order_No"
                  sortable
                  width="180"
                  column-key="date"
                  :filters="[{text: '2016-05-01', value: '2016-05-01'}, {text: '2016-05-02', value: '2016-05-02'}, {text: '2016-05-03', value: '2016-05-03'}, {text: '2016-05-04', value: '2016-05-04'}]"
                />
                <el-table-column
                  prop="name"
                  label="Price"
                  width="180"
                  align="center"
                />
                <el-table-column
                  prop="address"
                  label="Status"
                  align="center"
                />
                <el-table-column
                  prop="tag"
                  label="标签"
                  width="100"
                  :filters="[{ text: 'pending', value: 'pending' }, { text: 'success', value: 'success' }]"
                  filter-placement="bottom-end"
                  align="center"
                >
                  <template slot-scope="scope">
                    <el-tag
                      :type="scope.row.tag === 'pending' ? 'danger' : 'success'"
                      disable-transitions
                    >{{ scope.row.tag }}</el-tag>
                  </template>
                </el-table-column>
              </el-table>
            </el-card>
          </el-col>
          <el-col :span="6">
            <el-card id="detailCharts5" shadow="hover" style="position: relative">
              <el-table
                ref="multipleTable"
                :data="tableData"
                tooltip-effect="dark"
                style="width: 100%"
                @select="qifei"
                @selection-change="handleSelectionChange"
              >
                <el-table-column
                  type="selection"
                  width="55"
                  cell-class-name="p"
                />
                <el-table-column
                  label="日期"
                >
                  <template slot-scope="scope">{{ scope.row.date }}</template>
                </el-table-column>
              </el-table>
              <div style="margin-top: 20px">
                <span>{{}}</span>
                <el-button @click="toggleSelection([tableData[1], tableData[2]])">All</el-button>
                <el-button @click="toggleSelection([tableData[1], tableData[2]])">Active</el-button>
                <el-button @click="toggleSelection()">Complete</el-button>
              </div>
            </el-card></el-col>
          <el-col :span="6">
            <el-card id="detailCharts6" shadow="hover" style="position: relative" />
          </el-col>
        </el-row>
      </footer>
    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
export default {
  name: 'Index',
  data() {
    return {
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄',
        tag: 'pending'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄',
        tag: 'pending'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄',
        tag: 'success'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: 'pending'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: 'success'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: 'pending'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: 'success'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄',
        tag: 'pending'
      }],
      multipleSelection: []
      // leftNum: this.tableData.length
    }
  },
  mounted() {
    this.drawHeaderEcharts()
    this.drawDetailEcharts()
    this.drawDetailEcharts2()
    this.drawDetailEcharts3()
  },
  methods: {
    drawHeaderEcharts() {
      var myChart = echarts.init(document.querySelector('#headerEchart'))

      const option = {

        title: {

          text: '福建省高级人民法院 月报',

          textStyle: {

            fontSize: 30

          }

        },

        tooltip: {

          trigger: 'axis',

          axisPointer: { // 坐标轴指示器，坐标轴触发有效

            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'

          },

          textStyle: {

            fontSize: 16

          }

        },

        toolbox: {

          feature: {

            dataView: { show: true, readOnly: false },

            magicType: { show: true, type: ['line', 'bar'] },

            restore: { show: true },

            saveAsImage: { show: true }

          }

        },

        legend: {

          data: ['庭审案件数量', '庭审次数', '平均庭审次数'],

          textStyle: {

            fontSize: 24

          }

        },

        grid: {

          left: '3%',

          right: '4%',

          bottom: '3%',

          containLabel: true

        },

        xAxis: [

          {

            type: 'category',

            data: ['民事', '刑事', '行政', '执行', '赔偿', '信访']

          }

        ],

        yAxis: [

          {

            type: 'value'

          }

        ],

        series: [

          {

            name: '庭审案件数量',

            type: 'bar',

            data: [30, 28, 8, 7, 3, 2],

            markLine: {

              lineStyle: {

                type: 'dashed'

              },

              data: [

                [{ type: 'min' }, { type: 'max' }]

              ]

            }

          },

          {
            name: '庭审次数',
            type: 'bar',
            data: [26, 22, 5, 3, 2, 1]
          },
          {
            name: '平均庭审次数',

            type: 'bar',

            // barWidth: 5,

            // stack: '搜索引擎',

            data: [0, 0, 1, 1, 1, 1]
          }
        ]
      }
      myChart.setOption(option)
    },
    drawDetailEcharts() {
      var myChart = echarts.init(document.querySelector('#detailCharts1'))

      const option = {

        title: {

          text: '福建省高级人民法院 月报',

          textStyle: {

            fontSize: 30

          }

        },

        tooltip: {

          trigger: 'axis',

          axisPointer: { // 坐标轴指示器，坐标轴触发有效

            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'

          },

          textStyle: {

            fontSize: 16

          }

        },

        toolbox: {

          feature: {

            dataView: { show: true, readOnly: false },

            magicType: { show: true, type: ['line', 'bar'] },

            restore: { show: true },

            saveAsImage: { show: true }

          }

        },

        legend: {

          data: ['庭审案件数量', '庭审次数', '平均庭审次数'],

          textStyle: {

            fontSize: 24

          }

        },

        grid: {

          left: '3%',

          right: '4%',

          bottom: '3%',

          containLabel: true

        },

        xAxis: [

          {

            type: 'category',

            data: ['民事', '刑事', '行政', '执行', '赔偿', '信访']

          }

        ],

        yAxis: [

          {

            type: 'value'

          }

        ],

        series: [

          {

            name: '庭审案件数量',

            type: 'bar',

            data: [30, 28, 8, 7, 3, 2],

            markLine: {

              lineStyle: {

                type: 'dashed'

              },

              data: [

                [{ type: 'min' }, { type: 'max' }]

              ]

            }

          },

          {
            name: '庭审次数',
            type: 'bar',
            data: [26, 22, 5, 3, 2, 1]
          },
          {
            name: '平均庭审次数',

            type: 'bar',

            // barWidth: 5,

            // stack: '搜索引擎',

            data: [0, 0, 1, 1, 1, 1]
          }
        ]
      }
      myChart.setOption(option)
    },
    drawDetailEcharts2() {
      var myChart = echarts.init(document.querySelector('#detailCharts2'))

      const option = {

        title: {

          text: '福建省高级人民法院 月报',

          textStyle: {

            fontSize: 30

          }

        },

        tooltip: {

          trigger: 'axis',

          axisPointer: { // 坐标轴指示器，坐标轴触发有效

            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'

          },

          textStyle: {

            fontSize: 16

          }

        },

        toolbox: {

          feature: {

            dataView: { show: true, readOnly: false },

            magicType: { show: true, type: ['line', 'bar'] },

            restore: { show: true },

            saveAsImage: { show: true }

          }

        },

        legend: {

          data: ['庭审案件数量', '庭审次数', '平均庭审次数'],

          textStyle: {

            fontSize: 24

          }

        },

        grid: {

          left: '3%',

          right: '4%',

          bottom: '3%',

          containLabel: true

        },

        xAxis: [

          {

            type: 'category',

            data: ['民事', '刑事', '行政', '执行', '赔偿', '信访']

          }

        ],

        yAxis: [

          {

            type: 'value'

          }

        ],

        series: [

          {

            name: '庭审案件数量',

            type: 'bar',

            data: [30, 28, 8, 7, 3, 2],

            markLine: {

              lineStyle: {

                type: 'dashed'

              },

              data: [

                [{ type: 'min' }, { type: 'max' }]

              ]

            }

          },

          {
            name: '庭审次数',
            type: 'bar',
            data: [26, 22, 5, 3, 2, 1]
          },
          {
            name: '平均庭审次数',

            type: 'bar',

            // barWidth: 5,

            // stack: '搜索引擎',

            data: [0, 0, 1, 1, 1, 1]
          }
        ]
      }
      myChart.setOption(option)
    },
    drawDetailEcharts3() {
      var myChart = echarts.init(document.querySelector('#detailCharts3'))

      const option = {

        title: {

          text: '福建省高级人民法院 月报',

          textStyle: {

            fontSize: 30

          }

        },

        tooltip: {

          trigger: 'axis',

          axisPointer: { // 坐标轴指示器，坐标轴触发有效

            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'

          },

          textStyle: {

            fontSize: 16

          }

        },

        toolbox: {

          feature: {

            dataView: { show: true, readOnly: false },

            magicType: { show: true, type: ['line', 'bar'] },

            restore: { show: true },

            saveAsImage: { show: true }

          }

        },

        legend: {

          data: ['庭审案件数量', '庭审次数', '平均庭审次数'],

          textStyle: {

            fontSize: 24

          }

        },

        grid: {

          left: '3%',

          right: '4%',

          bottom: '3%',

          containLabel: true

        },

        xAxis: [

          {

            type: 'category',

            data: ['民事', '刑事', '行政', '执行', '赔偿', '信访']

          }

        ],

        yAxis: [

          {

            type: 'value'

          }

        ],

        series: [

          {

            name: '庭审案件数量',

            type: 'bar',

            data: [30, 28, 8, 7, 3, 2],

            markLine: {

              lineStyle: {

                type: 'dashed'

              },

              data: [

                [{ type: 'min' }, { type: 'max' }]

              ]

            }

          },

          {
            name: '庭审次数',
            type: 'bar',
            data: [26, 22, 5, 3, 2, 1]
          },
          {
            name: '平均庭审次数',

            type: 'bar',

            // barWidth: 5,

            // stack: '搜索引擎',

            data: [0, 0, 1, 1, 1, 1]
          }
        ]
      }
      myChart.setOption(option)
    },
    toggleSelection(rows) {
      if (rows) {
        rows.forEach(row => {
          this.$refs.multipleTable.toggleRowSelection(row)
        })
      } else {
        this.$refs.multipleTable.clearSelection()
      }
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    qifei(index) {
      this.leftNum = this.leftNum - index.length
      console.log(this.leftNum)
    }

  }
}
</script>

<style scoped>
  .birthHold {
  background-color: rgba(236, 240, 241,1);
  padding: 30px;
    /*box-sizing: content-box;*/
}
  .cloth {
    margin-top: 15px;
    /*background-color: #fff;*/
    /*height: 110px;*/
  }
  header .el-card {
    height: 110px;
    /*text-align: right;*/
  }
  header .el-card:hover img{
    border: 3px solid #1e6abc;
  }
  header .el-card img {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    width: 60px;
    height: 60px;
    color: #42b983;
  }
  .typeAclass {
    width: 120px;
    height: 70px;
    outline: 2px solid #42b983;
    margin-left: 200px;
  }
  .birthHold section {
    width: 100%;
  }
  .headerAchartsmove {
    margin-top: 30px;
    background-color: #fff;
  }
  #headerEchart {
    height: 300px;
    width: 100%;
  }
  .threeDetailCharts {
    margin-top: 30px;
  }
  .threeDetailCharts .el-card{
    height: 300px;
  }
  .orderAtoAtalk {
    margin-top: 30px;
  }
  .orderAtoAtalk .el-card {
    min-height: 400px;
  }
  .p {
    background-color: red;
  }
</style>

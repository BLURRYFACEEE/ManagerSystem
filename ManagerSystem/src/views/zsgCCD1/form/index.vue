<template>
  <div class="formBaseHold">
    <span>菜单属性</span>
    <div class="formContent">
      <el-form ref="searchForm" :model="currentList" :inline="true" label-width="180px" label-position="right">
        <el-row>
          <el-col :span="12">
            <el-form-item label="父级菜单" prop="parentName">
              <el-input v-model="currentList.parentName" :disabled="true" width="100%" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item
              label="菜单类型"
              prop="type"
            >
              <el-input v-model="currentList.type" placeholder="审批人2" type="input" :disabled="true" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
            <el-form-item
              label="菜单名称"
              prop="name"
              :rules="[
                { required: true, message: '菜单要填写啊！'}
              ]"
            >
              <el-input v-model="currentList.name" placeholder="审批人3" type="input" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="菜单URL" prop="url">
              <el-input v-model="currentList.url" placeholder="审批人4" type="input" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
            <el-form-item label="有效开始日期" prop="startDate">
              <el-date-picker v-model="currentList.startDate" type="date" placeholder="选择日期" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="有效截止日期" prop="endDate">
              <el-date-picker v-model="currentList.endDate" type="date" placeholder="选择日期" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
            <el-form-item label="是否展示" prop="isShow">
              <el-radio-group v-model="currentList.isShow">
                <el-radio label="是" />
                <el-radio label="否" />
              </el-radio-group>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="图标" prop="iconName">
              <el-input v-model="currentList.iconName" placeholder="图标" type="input" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
            <el-form-item label="打开模式" prop="openmode">
              <el-input v-model="currentList.openmode" placeholder="打开模式" type="input" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="是否有效" prop="isWork">
              <el-radio-group v-model="currentList.isWork">
                <el-radio label="是" />
                <el-radio label="否" />
              </el-radio-group>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="12">
            <el-form-item label="排序" prop="sort">
              <el-input v-model="currentList.sort" placeholder="审批人" type="input" />
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="备注" prop="tip">
              <el-input v-model="currentList.tip" type="textarea" style="width: 400px" />
            </el-form-item>
          </el-col>
        </el-row>
        <el-row align="center" style="text-align: center">
          <el-form-item class="board" prop="buttons">
            <el-button type="danger" @click="deleteCookie">删除</el-button>
            <el-button type="primary" @click="onSubmit">保存</el-button>
            <el-input v-model="currentList.keyname" type="textarea" />
            <!--            <el-input v-model="form.name" type="textarea" style="width: 400px" />-->
          </el-form-item>
        </el-row>
      </el-form>
    </div>
  </div>
</template>
<script>
import eventBus from '../../../utils/eventBus.js'
import Cookies from 'js-cookie'
export default {
  name: 'Index',
  data() {
    return {
      form: {
        name: '123123',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      parentName: '',
      labelMessage: '',
      currentList: {
      },
      // currentList: {
      //   parentName: '菜单根节点',
      //   type: '栏目',
      //   name: '工作台',
      //   url: '/dashboard',
      //   startDate: '2020-11-16',
      //   endDate: '2040-11-17',
      //   isShow: true,
      //   iconName: 'icon-gongzuotai',
      //   openmode: '系统内部跳转',
      //   isWork: true,
      //   sort: 1,
      //   tip: ''
      // },
      allList: {
        2: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '工作台',
          keyname: 'workTable',
          url: '/dashboard',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongzuotai',
          openmode: '系统内部跳转',
          isWork: '是',
          sort: 1,
          tip: '哈哈'
        },
        3: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '资源运行情况',
          keyname: 'resourceSituation',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        4: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '工单管理',
          keyname: 'workPaper',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        5: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '资源管理',
          keyname: 'resourceManage',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        6: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '管理',
          keyname: 'systemmanage',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        7: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '智能报表',
          keyname: 'smartEcharts',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        8: {
          parentName: '菜单根节点',
          type: '栏目',
          name: '监控项信息',
          keyname: 'watchInfos',
          url: '/resourceoperation',
          startDate: '2020-11-16',
          endDate: '2040-11-17',
          isShow: '是',
          iconName: 'icon-gongchengyunxingqingkuang',
          openmode: '系统内部跳转',
          isWork: '否',
          sort: 2,
          tip: '这里是资源运行情况WHATSWUP'
        },
        0: {
          parentName: '菜单根节点',
          name: 'newBorn'
        }
      },
      formInline: {
        user: '',
        region: ''
      },
      addId: 0
    }
  },
  mounted() {
    eventBus.$on('add', (id, parentName) => {
      // console.log('myNameIS' + name)
      // if (name === 'newBorn' || !this.allList[name]) {
      //   const newName = 'newBorn'
      //   // console.log('newChild' + this.allList[newName])
      //   this.currentList = this.allList[newName]
      //   // console.log(name)
      // } else {
      //   this.currentList = this.allList[name]
      //   // console.log(this.currentList)
      //   // if (Cookies.get(this.currentList.name).indexOf(this.currentList.name)) {
      //   //   this.currentList = JSON.parse(Cookies.get(this.currentList.name))
      //   // }
      // }
      // console.log('id+' + id)
      // console.log(this.allList)
      this.currentList = JSON.parse(JSON.stringify(this.allList[id]))
      // this.currentList = this.allList[id]
      this.currentList.parentName = parentName
    })
    eventBus.$on('reloadYourself', () => {
    })
    eventBus.$on('newChild', (parentName) => {
      this.$refs.searchForm.resetFields()
      // alert('新的~！')
      // console.log(parentName)
      console.log('提交前的allList')
      console.log(this.allList)
      this.currentList.parentName = parentName
    })
    eventBus.$on('addTreeDone', (id) => {
      // console.log('addTree' + id)
      this.addId = id
      this.allList[id] = {}
      // console.log(this.allList)
    })
  },
  methods: {
    onSubmit() {
      // Cookies.set(this.currentList.name, this.currentList, { expires: 7 })
      // console.log(this.currentList)
      this.allList[this.addId] = this.currentList
      // console.log(this.addId)
      console.log('提交时的allList')
      console.log(this.allList)
      eventBus.$emit('submitCheck', this.currentList)
      alert('已提交！')
    },
    deleteCookie() {
      Cookies.set(this.currentList.name, '', -1)
    }
  }
}
</script>

<style scoped>
.formBaseHold {
  padding: 20px;
}
  .formBaseHold>span {
    font-size: 14px;
  }
  .formContent {
    margin-top: 30px;
    /*text-align: right;*/
  }
  .formContent .el-form{
    margin-right: 20px;
  }
  ::v-deep .board {
    margin-top: 30px;
  }
  .el-form-item .el-input {
    width: 400px;
  }
</style>

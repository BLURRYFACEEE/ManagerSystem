<!--弹出框输内置选择框功能，获取后将返回一个对象，里面是输入的对象名以及相应的值-->
<template>
  <div>
    <el-dialog :title="title" :visible.sync="showDialog">
      <el-form :model="showTHings.value">
        <el-form-item v-for="(item,index) in showTHings" :key="index" :label="item.name" :label-width="formLabelWidth">
          <el-input v-model="item.value" autocomplete="off" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showDialog = false">取 消</el-button>
        <el-button type="primary" @click="newPush">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'Index',
  props: {
    showTHings: {
      type: Array,
      default: () => {
        return [{
          name: '登录账号',
          words: 'date',
          value: '1314520'
        }, {
          name: '角色名称',
          words: 'name',
          value: '王小虎'
        }, {
          name: '状态',
          words: 'address',
          value: '上海市普陀区金沙江路 1516 弄'
        }, {
          name: '是否默认',
          words: 'login',
          value: '2020-11-26 16:09:28'
        }, {
          name: '备注',
          words: 'tag',
          value: '公司'
        }
        ]
      }
    },
    title: {
      type: String,
      default: 'haha'
    }
  },
  data() {
    return {
      formLabelWidth: '120px',
      showDialog: false
    }
  },
  methods: {
    show() {
      this.showDialog = true
    },
    newPush() {
      const processThing = {}
      this.showTHings.forEach(function(item) {
        processThing[item.words] = item.value
      })
      this.showDialog = false
      this.$emit('dialogDataOut', processThing)
    }
  }
}
</script>

<style scoped>

</style>

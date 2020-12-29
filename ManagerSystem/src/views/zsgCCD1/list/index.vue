<template>
  <div v-if="update">
    <header>
      <div><el-button type="primary" icon="el-icon-edit" circle mini @click="newChild" /></div>
      <div><el-button type="primary" icon="el-icon-refresh" circle mini @click="reloadComp" /></div>
    </header>
    <section>
      <el-tree
        :data="data"
        node-key="id"
        default-expand-all
        draggable
        highlight-current
        :allow-drop="allowDrop"
        :allow-drag="allowDrag"
        @node-click="handleNodeClick"
        @node-drag-start="handleDragStart"
        @node-drag-enter="handleDragEnter"
        @node-drag-leave="handleDragLeave"
        @node-drag-over="handleDragOver"
        @node-drag-end="handleDragEnd"
        @node-drop="handleDrop"
      >
        <span slot-scope="{ node, data }" class="custom-tree-node">
          <span @mousedown.stop>{{ node.label }}</span>
          <span>
            <el-button
              type="text"
              size="mini"
              @click="() => append(data)"
            >
              Append
            </el-button>
            <el-button
              type="text"
              size="mini"
              @click="() => remove(node, data)"
            >
              Delete
            </el-button>
          </span>
        </span>
      </el-tree>
      <!--      <el-tree-->
      <!--        :data="data"-->
      <!--        show-checkbox-->
      <!--        node-key="id"-->
      <!--        default-expand-all-->
      <!--        :expand-on-click-node="false"-->
      <!--        :render-content="renderContent"-->
      <!--      />-->
    </section>
  </div>
</template>
<script>
import eventBus from '../../../utils/eventBus.js'
import Cookies from 'js-cookie'
let id = 1000
export default {
  name: 'Index',
  data() {
    return {
      labelName: '菜单根节点',
      data: [{
        id: 1,
        label: '菜单根节点',
        children: [{
          id: 2,
          label: '工作台',
          name: 'workTable'
        }, {
          id: 3,
          name: 'resourceSituation',
          label: '资源运行情况'
        }, {
          id: 4,
          name: 'workPaper',
          label: '工单管理'
        }, {
          id: 5,
          name: 'resourceManage',
          label: '资源管理'
        }, {
          id: 6,
          name: 'systemmanage',
          label: '系统管理'
        }, {
          id: 7,
          name: 'smartEcharts',
          label: '智能报表'
        }, {
          id: 8,
          name: 'watchInfos',
          label: '监控项信息'
        }]
      }],
      data2: {
      },
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      nowClickData: {},
      update: true
    }
  },
  mounted() {
    if (Cookies.get('ha')) {
      this.data = Cookies.get('ha')
      console.log('listCOokies!')
    }
    eventBus.$on('submitCheck', (submitForm) => {
      // console.log(submitForm)
      const newChild = { id: id++, label: submitForm.name, children: [] }
      if (!this.nowClickData.children) {
        this.$set(this.nowClickData, 'children', [])
      }
      this.nowClickData.children.push(newChild)
      // Cookies.set('ha', this.data)
      // var getChange = (this.data[0].children.filter(function(item) {
      //   return item.name === keyname
      // }))
      // console.log('getChange[0].label' + getChange[0].label)
      // getChange[0].label = name
      // console.log('keyname' + keyname)
      // console.log(name)
    })
  },
  methods: {
    reloadComp() {
      location.reload()
      eventBus.$emit('reloadYourself')
    },
    handleDragStart(node, ev) {
      console.log('drag start', node)
    },
    handleDragEnter(draggingNode, dropNode, ev) {
      console.log('tree drag enter: ', dropNode.label)
    },
    handleDragLeave(draggingNode, dropNode, ev) {
      console.log('tree drag leave: ', dropNode.label)
    },
    handleDragOver(draggingNode, dropNode, ev) {
      console.log('tree drag over: ', dropNode.label)
    },
    handleDragEnd(draggingNode, dropNode, dropType, ev) {
      console.log('tree drag end: ', dropNode && dropNode.label, dropType)
    },
    handleDrop(draggingNode, dropNode, dropType, ev) {
      console.log('tree drop: ', dropNode.label, dropType)
    },
    allowDrop(draggingNode, dropNode, type) {
      if (dropNode.data.label === '二级 3-1') {
        return type !== 'inner'
      } else {
        return true
      }
    },
    allowDrag(draggingNode) {
      return draggingNode.data.label.indexOf('三级 3-2-2') === -1
    },
    handleNodeClick(data, data2) {
      // this.labelName = data.label
      this.nowClickData = data
      // console.log(data)
      this.changesize(data.id, data2.parent.data.label)
      // console.log(data2.parent.data.label)
    },
    append(data) {
      const newChild = { id: id++, label: 'new', children: [] }
      if (!data.children) {
        this.$set(data, 'children', [])
      }
      data.children.push(newChild)
    },

    remove(node, data) {
      const parent = node.parent
      const children = parent.data.children || parent.data
      const index = children.findIndex(d => d.id === data.id)
      children.splice(index, 1)
    },
    // renderContent(h, { node, data, store }) {
    //   return (`<span class='custom-tree-node'><span>{${node}.label}</span> <span> <el-button size='mini' type='text' on-click={ () => this.append(${data}) }>Append</el-button> <el-button size='mini' type='text' on-click={ () => this.remove(${node}, ${data}) }>Delete</el-button> </span> </span>
    //   `)
    // },
    newChild() {
      // const newChild = { id: id++, label: 'new', name: 'newBorn', children: [] }
      // if (!this.nowData.children) {
      //   this.$set(this.nowData, 'children', [])
      // }
      // this.nowData.children.push(newChild)
      // eventBus.$emit('newChild', newChild.name)
      eventBus.$emit('addTreeDone', id)
      eventBus.$emit('newChild', this.nowClickData.label)
    },
    changesize(id, parentName) {
      eventBus.$emit('add', id, parentName)
    }
  }
}
</script>

<style scoped>
  header {
    position: relative;
    width: 100%;
    height: 45px;
    background-color: #9dc8db;
    line-height: 45px;
  }
  header div {
    display: inline-block;
    width: 49%;
  }
  header div:nth-child(1) {
    text-align: right;
    padding-right: 10px;
  }
  header div:nth-child(2) {
    padding-left: 10px;
  }
</style>

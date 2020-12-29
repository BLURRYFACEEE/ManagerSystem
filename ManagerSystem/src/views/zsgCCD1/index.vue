<template>
  <div class="basehold">
    <el-row :gutter="12">
      <el-col :span="4">
        <el-card shadow="hover">
          <list />
        </el-card>
      </el-col>
      <el-col :span="20">
        <el-card shadow="hover">
          <inputForm />
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import list from './list/index'
import inputForm from './form/index'
export default {
  name: 'Index',
  components: {
    list, inputForm
  },
  methods: {
    handleOpen(key, keyPath) {
      console.log(key, keyPath)
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath)
    }
  }
}
</script>

<style scoped>
.basehold{
  padding: 15px;
}
::v-deep .el-card__body {
  padding: 0;
}
  .el-card {
    height: 800px;
  }
</style>

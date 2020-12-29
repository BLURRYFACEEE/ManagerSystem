<template>
  <div>
    <div class="page1">
      <div class="resourceUp">
        <el-row :gutter="12">
          <el-col :span="13">
            <el-card shadow="hover" style="position: relative" class="resourceCard">
              <header>
                <img src="http://chuantu.xyz/t6/741/1608704449x1700338588.gif">
                <span>资源概览</span>
              </header>
              <section>
                <div class="cloudService cardCommon">
                  <div class="firstLine"><span>ECS</span><span>729</span></div>
                  <div class="secondLine"><span>云服务器</span></div>
                  <div class="thirdLine"><a>今日告警（次）0</a></div>
                </div>
                <div class="objStorage cardCommon cardThreeCommon">
                  <div class="firstLine"><span>OSS</span><span>42</span></div>
                  <div class="secondLine"><span>云服务器</span></div>
                  <div class="thirdLine"><a>今日告警（次）0</a></div>
                </div>
                <div class="relationDBService cardCommon cardThreeCommon">
                  <div class="firstLine"><span>RDS</span><span>132</span></div>
                  <div class="secondLine"><span>云服务器</span></div>
                  <div class="thirdLine"><a>今日告警（次）0</a></div>
                </div>
                <div class="workSleepWell cardCommon cardThreeCommon">
                  <div class="firstLine"><span>SLB</span><span>2</span></div>
                  <div class="secondLine"><span>云服务器</span></div>
                  <div class="thirdLine"><a>今日告警（次）0</a></div>
                </div>
              </section>
            </el-card>
          </el-col>
          <el-col :span="11">
            <el-card shadow="hover" style="position: relative" class="resourceUpCard2">
              <header>
                <img src="http://chuantu.xyz/t6/741/1608704449x1700338588.gif">
                <span>资源运行快速导航</span>
              </header>
              <section>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
              </section>
            </el-card>
          </el-col>
        </el-row>
      </div>
      <div class="resourceContent">
        <el-row :gutter="12">
          <el-col :span="13">
            <el-card shadow="hover" style="position: relative" class="resourceCard">
              <header>
                <img src="http://chuantu.xyz/t6/741/1608704449x1700338588.gif">
                <span>代办工单</span>
                <div class="more"><a>更多></a></div>
              </header>
              <section>
                <el-timeline :reverse="reverse" >
                  <el-timeline-item
                    v-for="(activity, index) in activities"
                    :key="index"
                    :timestamp="activity.timestamp"
                  >
                    {{ activity.content }}
                  </el-timeline-item>
                </el-timeline>
              </section>
            </el-card>
          </el-col>
          <el-col :span="11">
            <el-card shadow="hover" style="position: relative" class="resourceUpCard2">
              <header>
                <img src="http://chuantu.xyz/t6/741/1608704449x1700338588.gif">
                <span>待维护资源</span>
              </header>
              <section>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
                <div><a>ECS资源快速导航</a></div>
              </section>
            </el-card>
          </el-col>
        </el-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Index',
  data() {
    return {
      reverse: true,
      activities: [{
        content: '活动按期开始',
        timestamp: '2018-04-15'
      }, {
        content: '通过审核',
        timestamp: '2018-04-13'
      }, {
        content: '创建成功',
        timestamp: '2018-04-11'
      },{
        content: '活动按期开始',
        timestamp: '2018-04-15'
      }, {
        content: '通过审核',
        timestamp: '2018-04-13'
      }, {
        content: '创建成功',
        timestamp: '2018-04-11'
      }, {
        content: '创建成功',
        timestamp: '2018-04-11'
      }]
    }
  }
}
</script>

<style scoped>
  .page1{
    padding: 40px;
    background-color: rgba(236, 240, 241,1);
  }
  .resourceUp .el-card {
    /*min-width: 110px;*/
    height: 200px;
  }
  header span {
    font-size: 22px;
  }
  header img {
    /*position: absolute;*/
    /*top: 50%;*/
    /*transform: translateY(-50%);*/
    width: 14px;
    height: 14px;
  }
  .resourceCard section {
    margin-top: 20px;
  }
  .firstLine span:nth-child(1) {
    color: #1e6abc;
    font-size: 20px;
  }
  .firstLine span:nth-child(2) {
    color: #99a9bf;
    font-weight: 700;
    font-size: 36px;
    margin-left: 10px;
  }
  .secondLine {
    margin-top: 5px;
  }
  .thirdLine {
    margin-top: 5px;
  }
  .thirdLine a{
    text-decoration: underline;
    color: #4AB7BD;
  }
  .cardCommon{
    display: inline-block;
    width: 18%;
    height: 110px;
    padding-left: 20px;
    padding-top: 5px;
    /*background-color: #0000ff;*/
  }
  .cardThreeCommon{
    margin-left: 50px;
    border-left: 1px solid #d3dce6;
  }
  .resourceUpCard2 div{
    font-size: 20px;
    display: inline-block;
    width: 49%;
    text-align: center;
    margin-top: 20px;
  }
  .resourceUpCard2 div a{
    background-color: #d3dce6;
    font-weight: normal;
    padding: 5px;
  }
  .resourceContent{
    margin-top: 10px;
  }
  .resourceContent .el-card {
    height: 550px;
  }
  ::v-deep .resourceContent .el-timeline {
    font-size: 16px;
    margin-left: 140px;
  }
  ::v-deep .resourceContent .el-timeline-item__content {
    margin-left: 40px;
    color: #99a9bf;
  }
  ::v-deep .resourceContent .el-timeline-item__timestamp.is-bottom{
    position: relative;
    right: 140px;
    top: -25px;
    font-size: 16px;
  }
  ::v-deep .resourceContent .el-timeline-item__wrapper {
    /*padding-left: 40px;*/
  }
  .more {
    float: right;
    margin-right: 5px;
    color: #4A9FF9;
    font-size: 20px;
  }
</style>

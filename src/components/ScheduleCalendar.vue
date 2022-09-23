<template>
  <div class="schedule-calendar">
    <div class="org-tree">
      <h2>
        <i class="el-icon-notebook-2"></i>
        Staff Book
      </h2>
      <el-tree
        ref="orgTree"
        :data="treeData"
        :props="treeProps"
        node-key="id"
        highlight-current
        @current-change="handleStaffChange"        
      >
      </el-tree>
    </div>
    <div class="staff-info" v-loading="loading">
      <h2>
        <i class="el-icon-date"></i>
        {{ info.title }}
      </h2>
      <p>{{ info.content }}</p>
    </div>
  </div>
</template>

<script>
import { orgTreeData } from '@/constant/data'

export default {
  name: 'ScheduleCalendar',
  props: {
    msg: String,
  },
  data() {
    return {
      // tree
      treeData: [...orgTreeData],
      treeProps: {
        label: 'name',
        children: 'staffList'
      },
      // status
      loading: false,      
      currentStaff: null,
      // info
      info: {
        title: 'Schedule',
        content: 'Select Staff'
      },
    }
  },
  watch: {
    treeData() {
      
    }
  },
  mounted() {

  },
  methods: {
    handleStaffChange(data) {
      // console.log(data)
      if(!data.isStaff) return
      this.currentStaff = {...data}
      this.showCurrentStaffInfo()
    },
    async showCurrentStaffInfo() {
      console.log('fetch staff info', this.currentStaff.id)
      // fake progress for api request staff info
      this.loading = true
      await new Promise(r => setTimeout(r, 400))
      this.loading = false
      this.info.title = `${this.currentStaff.name}'s Schedule`
      this.info.content = `the work plan of ${this.currentStaff.name}.`
    }
  }
  
}
</script>

<style lang="scss">
.schedule-calendar {
  width: 100%;
  height: 100%;
  display: flex;
  .org-tree {
    flex: 0 0 420px;
  }
  .staff-info {
    flex: 1;
    border-left: 2px solid #607d8b;
  }
}

// element ui 
.el-tree--highlight-current .el-tree-node.is-current>.el-tree-node__content {
  background-color: rgb(255 235 59 / 50%);
}

</style>


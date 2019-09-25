<template>
  <div class='task-detail-list-scroll'>
    <p v-for="task in this.chunkInfoList"
      :key=task.index>
      <b>{{ $t('tasks.part') }}{{task.index+1}}:</b>
      <Progress :percent="calcProgress(task)"></Progress>
    </p>
  </div>
</template>
<script>
export default {
  // data
  data() {
    return {
      chunkInfoList:this.taskInfo.chunkInfoList
    }
  },

  props: {
    taskInfo: {
      type: Object,
      required: true
    }
  },
  watch: {
    taskInfo() {
      this.chunkInfoList = this.taskInfo.chunkInfoList
    }
  },
  methods: {
    calcProgress(task) {
      let progress = this.$numeral(task.downSize / task.totalSize).multiply(100)
      return new Number(progress.format('0'))
    }
  }
}
</script>
<style lang="less" scoped>
.task-detail-list-scroll {
  overflow-y: auto;
  height: 166px;
}
.task-detail-list-scroll > p > b {
  width: 15%;
}
.task-detail-list-scroll > p > div {
  width: 85%;
}
</style>
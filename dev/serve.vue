<script>
import Vue from 'vue'
import VueAmisEditor from '@/vue-amis-editor.vue'

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueAmisEditor,
  },
  data() {
    return {
      preview: false,
      mobile: false,
      theme: 'antd',
      schema: {
        type: 'tasks',
        name: 'tasks',
        items: [
          {
            label: 'hive 任务',
            key: 'hive',
            status: 4,
            remark: '查看详情<a target="_blank" href="http://www.baidu.com">日志</a>。',
          },
          {
            label: '小流量',
            key: 'partial',
            status: 4,
          },
          {
            label: '全量',
            key: 'full',
            status: 4,
          },
        ],
        id: 'u:5f649ab86d6a',
      },
    }
  },
  mounted() {
    this.$nextTick((e) => {
      // console.log(this.$refs)
      // this.$refs.amisEditor.onChange(this.schema)
    })
  },
})
</script>

<template>
  <div id="app">
    <vue-amis-editor :is-preview="preview" ref="amisEditor" :is-mobile="mobile" />
  </div>
</template>

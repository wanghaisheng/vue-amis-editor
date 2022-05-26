<script>
import 'font-awesome/css/font-awesome.css'
import 'bootstrap/dist/css/bootstrap.css'
import 'amis-editor/dist/style.css'
import 'amis/lib/helper.css'
import 'amis/sdk/iconfont.css'
import 'amis/lib/themes/antd.css'
// import 'amis/lib/themes/default.css'
// import 'amis/lib/themes/dark.css'
// import 'amis/lib/themes/cxd.css'
// import 'amis/sdk/sdk.js'

import { Editor } from 'amis-editor'
import { ReactInVue } from 'vuera'
export default /*#__PURE__*/ {
  name: 'VueAmisEditor', // vue component name
  data() {
    return {
      counter: 5,
      initCounter: 5,
      message: {
        action: null,
        amount: null,
      },
    }
  },
  components: {
    amisEditor: ReactInVue(Editor),
  },
  props: {
    isPreview: {
      type: Boolean,
      require: false,
      default: false,
    },
    isMobile: {
      type: Boolean,
      require: false,
      default: false,
    },
    theme: {
      type: String,
      require: false,
      default: 'antd',
    },
    value: {
      type: Object,
      require: false,
      default: function () {
        return {
          message: 'message',
        }
      },
    },
  },
  data() {
    return {
      refreshKey: Math.random() * (3 - 1),
      schema: 'message',
    }
  },
  created() {
    this.schema = this.value
    this.refreshKey = 9
  },
  methods: {
    setSchema(obj) {
      this.schema = obj
    },
    getSchema() {
      return this.schema
    },
    onChange(e) {
      this.$emit('onChange', e)
    },
  },
}
</script>

<template>
  <div class="vue-amis-editor">
    <amis-editor
      id="editorName"
      :key="refreshKey"
      class-name="is-fixed"
      :is-mobile="isMobile"
      :preview="isPreview"
      :theme="theme"
      :value="schema"
      @onChange="onChange"
    />
  </div>
</template>

<style lang="less">
.vue-amis-editor > #editor {
  width: 100%;
  height: 100vh !important;
}
.ae-Editor .ae-Editor-inner {
  height: 100vh !important;
}
</style>

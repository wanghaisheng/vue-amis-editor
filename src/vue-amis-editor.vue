<script>
  import copy from 'copy-to-clipboard';
  import { Layout, Switch, classnames as cx, toast, SchemaObject, Alert } from 'amis';
  import '@fortawesome/fontawesome-free/css/all.css'
  import 'bootstrap/dist/css/bootstrap.css'
  import 'amis-editor/dist/style.css'
  import 'amis/lib/helper.css'
  import 'amis/sdk/iconfont.css'
  import 'amis/lib/themes/antd.css'
  import 'amis/lib/themes/default.css';
  import 'amis/lib/themes/cxd.css';

  import {
    Editor
  } from 'amis-editor'
  import {
    ReactInVue
  } from 'vuera'
  export default /*#__PURE__*/ {
    name: 'VueAmisEditor', // vue component name
    data() {
      return {
        isPhone: false,
        preview: false,
        counter: 5,
        initCounter: 5,
      }
    },
    components: {
      amisEditor: ReactInVue(Editor),
      amisSwitch: ReactInVue(Switch),
      amisCx: ReactInVue(cx),
      amisToast: ReactInVue(toast),
      amisAlert: ReactInVue(Alert),
      amisSchemaObject: ReactInVue(SchemaObject),
    },
    props: {
      defaultMsg: {
        type: Object,
        require: false,
        default: function () {
          return {
            "type": "iframe",
            "src": "https://www.bilibili.com/video/av380701892?t=3.7",
            "id": "u:af8a682833e7",
            "width": "100%",
            "height": "100vh"
          }
        },
      },
      viewModes: {
        type: String,
        default: 'pc',
        require: false,
      },
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
      isTools: {
        type: Boolean,
        require: false,
        default: true,
      },
      navHeight: {
        type: Number,
        require: false,
        default: 50,
      },
      theme: {
        type: String,
        require: false,
        default: 'antd',
      },
      toolbar: {
        type: Object,
        require: false,
        default: function () {
          return {
            title: 'vue-amis-editor',
            preview: 'preview',
            release: 'release',
            edit: 'edit',
            obtain: 'obtain',
            copy: "copy",
            clear: 'clear',
            set: "set"
          }
        },
      },
      value: {
        type: Object,
        require: false,
        default: function () {
          return localStorage.getItem('amis-viewMode') ? JSON.parse(localStorage.getItem('amis-viewMode')) : {
            message: 'message',
          }
        },
      },
    },
    data() {
      return {
        refreshKey: Math.random() * (3 - 1),
        schema: 'message',
        isPhone: true,
      }
    },

    created() {
      this.schema = this.value
      this.isPhone = this.isMobile
      this.preview = this.isPreview
      this.refreshKey = 9
      this.viewMode = this.viewModes
    },
    methods: {
      obtain() {
        const schema = this.getSchema()
        console.log(schema)
        return schema
      },
      switchPreview(type) {
        if (typeof type == 'boolean') {
          this.preview = Boolean(type)
          this.refreshKey = new Date().getTime()
          const schema = this.getSchema()
          console.log(schema)
          this.setSchema(schema)
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      togggeMobile(type) {
        if (Boolean(type)) {
          this.viewMode = this.isPhone ? 'phone' : 'pc'
          this.isPhone = type
        } else {
          this.isPhone = !this.isPhone
          this.viewMode = this.isPhone ? 'phone' : 'pc'
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      setSchema(obj) {
        if (typeof obj == 'object') {
          this.schema = obj
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct', obj)
        }
      },
      getSchema() {
        return this.schema
      },
      onChange(e) {
        if (typeof e == 'object') {
          this.setSchema(e)
          this.$emit('onChange', e)
          localStorage.setItem('amis-viewMode', JSON.stringify(e))
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      clear() {
        localStorage.removeItem('amis-viewMode')
        this.setSchema({})
      },
      copy() {
        copy(JSON.stringify(this.getSchema()))
      },
      set(e) {
        if (typeof e == 'object') {
          this.setSchema(e)
          this.preview = true
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      }
    }
  }
</script>

<template>
  <div class="vue-amis-editor">
    <nav v-if="isTools" :style="{ height: navHeight + 'px' }">
      <div>
        <div class="row">
          <div class="col-3 ml-10">
            <h2>{{toolbar.title}}</h2>
            </title>
          </div>
          <div class="col-3 d-flex justify-content-center">
            <div className="editor-preview" style="text-align: center">
              <span> <i v-if="isPhone==true" style="font-size: 24px;" class="fa-solid fa-desktop"></i>
                <i v-if="isPhone==false" style="font-size: 24px;" class="fa-phone fa-solid"></i></span>
              <amis-switch :value="isPhone" @onChange="togggeMobile()" className="m-l-xs" inline />
            </div>
          </div>
          <div class="col-5 d-flex justify-content-center">
            <div className="editor-preview" style="text-align: center">
              <span> <i v-if="preview==true" style="font-size: 24px;" class="fa-solid fa-eye"></i>
                <i v-if="preview==false" style="font-size: 24px;" class="fa-solid fa-pen-to-square"></i></span>
              <amis-switch :value="preview" @onChange="switchPreview(!preview)" className="m-l-xs" inline />
            </div>

            <button type="button" class="btn  ml-10 btn-success" @click="obtain">{{toolbar.obtain}}</button>
            <button type="button" class="btn  ml-10 btn-success" @click="copy">{{toolbar.copy}}</button>

            <button type="button" class="btn  ml-10 btn-success" @click="clear">{{toolbar.clear}}</button>
            <button type="button" class="btn  ml-10 btn-success" @click="set(defaultMsg)">{{toolbar.set}}</button>
          </div>
        </div>
      </div>
    </nav>
    <amis-toast key="toast" position="top-right" theme="default" />
    <amis-alert key="alert" theme="default" />
    <amis-editor id="editorName" :key="refreshKey" class-name="is-fixed" ref="baiduAmis" :is-mobile="isPhone"
      :preview="preview" :theme="theme" :value="schema" @onChange="onChange" :viewMode="viewMode" @obtain="obtain"
      @copy="copy" @clear="clear" @getSchema="getSchema" @setSchema="setSchema" @set="set" @togggeMobile="togggeMobile"
      @togglePreview="switchPreview" />
  </div>
</template>

<style lang="less">
  .vue-amis-editor>#editor {
    width: 100%;
    height: calc(100vh - 50px) !important;
  }

  .ae-Editor .ae-Editor-inner {
    height: calc(100vh - 50px) !important;
  }
</style>
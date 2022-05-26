<script>
  import copy from 'copy-to-clipboard';

  import '@fortawesome/fontawesome-free/css/all.css'
  import 'bootstrap/dist/css/bootstrap.css'
  import 'amis-editor/dist/style.css'
  import 'amis/lib/helper.css'
  import 'amis/sdk/iconfont.css'
  import 'amis/lib/themes/antd.css'
  // import 'amis/lib/themes/default.css'
  // import 'amis/lib/themes/dark.css'
  // import 'amis/lib/themes/cxd.css'
  // import 'amis/sdk/sdk.js'

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
        isPhone: true,
      }
    },

    created() {
      this.schema = this.value
      this.isPhone = this.isMobile
      this.preview = this.isPreview
      this.refreshKey = 9
    },
    methods: {
      obtain() {
        const schema = this.getSchema()
        return schema
        console.log(schema)
      },
      togglePreview(type) {
        if (type) {
          const schema = this.getSchema()
          this.setSchema(schema)
          this.preview = type
          this.refreshKey = new Date().getTime()
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      togggeMobile(type) {
        if (type) {
          this.isPhone = !this.isPhone
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      setSchema(obj) {
        if (obj) {
          this.schema = obj
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }
      },
      getSchema() {
        return this.schema
      },
      onChange(e) {
        if (e) {
          this.setSchema(e)
          this.$emit('onChange', e)
        } else {
          throw new Error('The setting item is required, please make sure your parameters are correct')
        }

      },
      clear() {
        this.setSchema({})
      },
      copy() {
        copy(JSON.stringify(this.getSchema()))
      },
      set(e) {
        if (e) {
          this.setSchema(e)
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
          <div class="col-5 d-flex justify-content-center">
            <div class="form-check form-switch">
              <input class="form-check-input" type="checkbox" role="switch" id="flexSwitchCheckChecked"
                :checked="isPhone" @click="isPhone=!isPhone">
              <label class="form-check-label" for="flexSwitchCheckChecked"></label>
            </div>
            <i v-if="isPhone==true" style="font-size: 24px;" class="fa-solid fa-desktop"></i>
            <i v-else style="font-size: 24px;" class="fa-phone fa-solid"></i>
          </div>
          <div class="col-3 d-flex justify-content-center">
            <div class="btn-group" role="group" aria-label="Basic radio toggle button group">
              <input type="radio" class="btn-check" name="preview" id="true" autocomplete="off" checked />
              <label class="btn btn-outline-primary" for="true" @click="togglePreview(true)">{{toolbar.preview}}
              </label>

              <input type="radio" class="btn-check" name="preview" id="false" autocomplete="off" />
              <label class="btn btn-outline-primary" for="false"
                @click="togglePreview(false)">{{toolbar.release}}</label>
            </div>
            <button type="button" class="btn  ml-10 btn-success" @click="obtain">{{toolbar.obtain}}</button>
            <button type="button" class="btn  ml-10 btn-success" @click="copy">{{toolbar.copy}}</button>

            <button type="button" class="btn  ml-10 btn-success" @click="clear">{{toolbar.clear}}</button>
            <button type="button" class="btn  ml-10 btn-success" @click="set(json)">{{toolbar.set}}</button>
          </div>
        </div>
      </div>
    </nav>
    <amis-editor id="editorName" :key="refreshKey" class-name="is-fixed" ref="baiduAmis" :is-mobile="isPhone"
      :preview="preview" :theme="theme" :value="schema" @onChange="onChange" @obtain="obtain" @copy="copy"
      @clear="clear" @getSchema="getSchema" @setSchema="setSchema" @set="set" @togggeMobile="togggeMobile"
      @togglePreview="togglePreview" />
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
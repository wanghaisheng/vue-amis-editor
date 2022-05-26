# vue-amis-editor

<div align="center">

[![version](https://img.shields.io/npm/v/vue-amis-editor/latest)](https://github.com/h7ml/vue-amis-editor/blob/master/package.json#L36)
[![language](https://img.shields.io/github/languages/top/h7ml/vue-amis-editor)](https://github.com/h7ml/vue-amis-editor/search?l=css)
[![last](https://img.shields.io/github/last-commit/h7ml/vue-amis-editor.svg)](https://github.com/h7ml/vue-amis-editor/commits)
[![stars](https://img.shields.io/badge/Hosted-Vercel-brightgreen?style=flat&logo=Vercel)](https://amis.vercel.app/)
<img src="https://img.shields.io/github/commit-activity/m/h7ml/vue-amis-editor" alt="ommit-activity">
<img src="https://badgen.net/badge/package/%40dgiot%2Fdgiot-mqtt-dashboard/blue"
	alt="package" maxretrytimes="3" class="m-1 transition-all duration-1000">
<img src="https://badgen.net/npm/v/vue-amis-editor" alt="Npm Version"
	maxretrytimes="3" class="m-1 transition-all duration-1000">
<img src="https://badgen.net/npm/node/vue-amis-editor" alt="Node Version"
	maxretrytimes="3" class="m-1 transition-all duration-1000">
<br>
<img src="https://badgen.net/jsdelivr/hits/npm/vue-amis-editor"
	alt="Jsdeliver Month Downloads" maxretrytimes="3" class="m-1 transition-all duration-1000">
<img src="https://badgen.net/packagephobia/install/vue-amis-editor"
	alt="Install Size" maxretrytimes="3" class="m-1 transition-all duration-1000">
<img src="https://badgen.net/npm/types/vue-amis-editor" alt="Type Support"
	maxretrytimes="3" class="m-1 transition-all duration-1000">
<br>
<img src="https://img.shields.io/librariesio/release/npm/vue-amis-editor"
	alt="Outdated Dep" maxretrytimes="3" class="m-1 transition-all duration-1000">
<img src="https://img.shields.io/snyk/vulnerabilities/npm/vue-amis-editor"
	alt="Vulnerablities" maxretrytimes="3" class="m-1 transition-all duration-1000">
<a href="https://www.npmjs.com/package/vue-amis-editor"><img src="https://img.shields.io/npm/l/vue-amis-editor" alt="License"></a>

</div>

## Installation

```bash
yarn add vue-amis-editor --save
```

## Quick Start

### [Serve.vue](https://github.com/h7ml/vue-amis-editor/blob/master/dev/serve.vue)

```javascript
import VueAmisEditor from 'vue-amis-editor'
export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueAmisEditor,
  },
  data() {
    return {
      preview: true,
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
})
</script>
<template>
  <div id="app">
    <vue-amis-editor :is-preview="preview" :value="schema" />
  </div>
</template>

```

### Online examples

[![Edit gmullerb-react-reducer-provider](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/github/h7ml/vue-amis-editor)

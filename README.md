![Alt text](http://p5qgrn52w.bkt.clouddn.com/switch-ios-puge/20180820172408.png)

安装
```
npm i -save switch-ios-puge
或
yarn add switch-ios-puge
```

使用
```
<template>
  <div>
    <Switch v-model="active"></Switch>
  </div>
</template>

<script>
import Switch from 'switch-ios-puge'
export default {
  components: {
    Switch
  },
  data () {
    return {
      active: true
    }
  }
}
</script>
```
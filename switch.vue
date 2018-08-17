<template>
  <div v-once class="switch-bar">
    <input type="checkbox" :id="checkboxId" :checked="value"  @click.stop="updateValue">
    <label class="switch-label" :for="checkboxId">
      <span class="switch-inner" data-on="ON" data-off="OFF"></span>
      <span class="switch-switch"></span>
    </label>
  </div>
</template>


<script>
import { Order } from '@/components/Order.js'
export default {
  props: {
    value: Boolean,
    assemblyKey: String,
    updata: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
      checkboxId: Math.random().toString(36).substr(2),
      copyValue: this.value
    }
  },
  methods: {
    updateValue () {
      this.copyValue = !this.copyValue
      this.$emit('onClick', this.copyValue, this.assemblyKey)
      this.$emit('input', this.copyValue)
      // 需要将刷新放在最后面以保证正常刷新
      if (this.updata) {
        Order.$emit('needUpdata')
      }
    }
  }
}
</script>

<style lang='less' scoped>
input {
  width: 102px;
  height: 25px;
  border: none;
}
.switch-box {
  position: relative;
  user-select: none;
}

.switch-checkbox {
  display: none;
}

.switch-label {
  display: block;
  overflow: hidden;
  cursor: pointer;
  border-radius: 5px;
  width: 100px;
  position: relative;
  height: 25px;
}

.switch-inner {
  display: block;
  width: 200%;
  height: 25px;
  margin-left: -100%;
  transition: margin 0.3s ease-in 0s;
}

.switch-inner::before, .switch-inner::after {
  display: block;
  float: right;
  width: 50%;
  height: 25px;
  padding: 0;
  line-height: 25px;
  font-size: 14px;
  color: white;
  font-family: Trebuchet, Arial, sans-serif;
  font-weight: bold;
  box-sizing: border-box;
}

.switch-inner::after {
  content: attr(data-on);
  padding-left: 10px;
  background-color: #00e500;
  color: #FFFFFF;
}

.switch-inner::before {
  content: attr(data-off);
  padding-right: 10px;
  background-color: white;
  color: #999999;
  text-align: right;
}

.switch-switch {
  position: absolute;
  display: block;
  width: 19px;
  height: 19px;
  margin: 2px;
  background: #FFFFFF;
  top: 0;
  bottom: 0;
  right: 73px;
  border: 1px solid #999999;
  border-radius: 20px;
  transition: all 0.3s ease-in 0s;
}

.switch-checkbox:checked + .switch-label .switch-inner {
  margin-left: 0;
}

.switch-checkbox:checked + .switch-label .switch-switch {
  right: 0px;
}
</style>
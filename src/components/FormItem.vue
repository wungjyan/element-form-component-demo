<template>
  <div>
    <label for="">{{label}}</label>
    <div>
      <slot></slot>
      <p v-if="errStatus">{{errMessage}}</p>
    </div>
  </div>
</template>

<script>
import Schema from 'async-validator' // 引入插件
export default {
  inject: ['aForm'], // 接收 aForm
  props: {
    label: String,
    prop: String
  },
  data () {
    return {
      errStatus: false,
      errMessag: ''
    }
  },
  mounted () {
    // 监听自身触发的 validate 方法，进行验证逻辑
    this.$on('validate', this.handleValidate)
  },
  methods: {
    // 定义验证方法
    handleValidate () {
      // 获取此时正在输入的值
      // prop 是通过 props传入的，表示当前要验证的字段，此例中指的就是 username
      const value = this.aForm.model[this.prop]

      // 获取 username 的验证规则
      const rule = this.aForm.rules[this.prop]

      // 描述对象
      const descriptor = { [this.prop]: rule }

      // 传入描述对象，创建验证实例
      const validator = new Schema(descriptor)

      // 校验
      validator.validate({ [this.prop]: value }, errors => {
        if (errors) {
          this.errMessage = errors[0].message
          this.errStatus = true
        } else {
          this.errMessage = ''
          this.errStatus = ''
        }
      })
    }
  }
}
</script>

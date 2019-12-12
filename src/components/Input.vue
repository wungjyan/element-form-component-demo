<template>
  <div>
    <input :value="value" @input="onInput">
  </div>
</template>

<script>
export default {
  props: {
    value: [String, Number]
  },
  methods: {
    onInput (e) {
      this.$emit('input', e.target.value)
      this.$parent.$emit('validate') // 输入时，使 FormItem 自身触发 validate 事件
    }
  }
}
</script>

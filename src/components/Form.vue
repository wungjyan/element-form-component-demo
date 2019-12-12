<template>
  <div>
    <form>
      <slot></slot>
    </form>
  </div>
</template>

<script>
export default {
  provide () {
    return {
      aForm: this // 将 AForm 组件自身提供给下层组件
    }
  },
  props: {
    model: Object,
    rules: Object
  }
}
</script>

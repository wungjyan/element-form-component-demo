<template>
  <div id="app">
    <div style="width:300px;margin:100px auto;">
      <a-form :model="form" :rules="rules" ref="form">
        <a-form-item label="用户名" prop="username">
          <a-input v-model="form.username" />
        </a-form-item>
        <a-form-item label="密码" prop="password">
          <a-input v-model="form.password" />
        </a-form-item>
        <a-form-item label="确认密码" prop="checkPass">
          <a-input v-model="form.checkPass" />
        </a-form-item>
      </a-form>
    </div>
  </div>
</template>

<script>
import AInput from './components/Input'
import AFormItem from './components/FormItem'
import AForm from './components/Form'
export default {
  components: {
    AInput,
    AFormItem,
    AForm
  },
  data () {
    var validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'))
      } else {
        if (this.form.checkPass !== '') {
          this.$refs.form.validateField('checkPass')
        }
        callback()
      }
    }
    var validatePass2 = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请再次输入密码'))
      } else if (value !== this.form.password) {
        callback(new Error('两次输入密码不一致!'))
      } else {
        callback()
      }
    }
    return {
      form: {
        username: '',
        password: '',
        checkPass: ''
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        password: [
          { validator: validatePass, trigger: 'blur' }
        ],
        checkPass: [
          { validator: validatePass2, trigger: 'blur' }
        ]
      }
    }
  }
}
</script>

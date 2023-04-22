

<template>
  <div class="register">
    <el-form :model="form" ref="form" :rules="rules" label-width="80px" class="register-form">
      Library Registration
      <el-form-item label="UserAccount" prop="username">
        <el-input v-model="form.username"></el-input>
        The account can contain letters, underscores, and numbers, but must start with a letter
      </el-form-item>
      <el-form-item label="Nickname" prop="nickname">
        <el-input v-model="form.nickname"></el-input>
      </el-form-item>
      <el-form-item label="password" prop="password">
        <el-input type="password" v-model="form.password"></el-input>
        The password should be 6-20 digits long and contain letters, numbers, and special characters
      </el-form-item>
      <el-form-item label="ConfirmPassword" prop="confirmPassword">
        <el-input type="password" v-model="form.confirmPassword"></el-input>
      </el-form-item>
      <el-form-item label="birthday" prop="birthday">
        <el-input v-model="form.birthday"></el-input>
        Date Format:2016-11-22
      </el-form-item>
      <el-form-item label="Phone" prop="phone">
        <el-input v-model="form.phone"></el-input>
      </el-form-item>
      <el-form-item>
          <el-button type="primary" @click="dialogVisible = true" >
            Register
          </el-button>

          <el-dialog v-model="dialogVisible" title="Click to log in">
            <template #footer>
              <span class="dialog-footer">
                <el-button @click="dialogVisible = false">Cancel</el-button>
                <el-button type="primary" @click="dialogVisible = false">
                  Confirm
                </el-button>
              </span>
            </template>
          </el-dialog>
      </el-form-item>
    </el-form>
  </div>
</template>


<script lang="ts">
import { defineComponent } from 'vue';
import { ElForm, ElFormItem, ElInput, ElButton } from 'element-plus';
import { reactive, ref } from 'vue';
const dialogVisible = ref(false);

export default defineComponent({
  name: 'Register',
  components: {
    ElForm,
    ElFormItem,
    ElInput,
    ElButton,
  },
  
  data() {
    return {
      dialogVisible: false,
      form: {
        username: '',
        nickname:'',
        password: '',
        confirmPassword: '',
        birthday:'',
        phone: '',
      },
      rules: {
        username: [
          { required: true, trigger: 'blur' },
          {pattern: /^[a-zA-Z][a-zA-Z0-9_]*$/,trigger: 'blur'},
        ],
        nickname: [{ required: true,trigger: 'blur' }],
        password: [
          { required: true,  trigger: 'blur' },
          { min: 8, max: 32,pattern: /^(?=.*[0-9])(?=.*[a-zA-Z])(?=.*[!@#$%^&*])[0-9a-zA-Z!@#$%^&*]+$/,  trigger: 'blur' },
        ],
        confirmPassword: [
          { required: true, trigger: 'blur' },
          {
            validator: (rule, value, callback) => {
              if (value === '') {
                callback(new Error('Please enter the password again'));
              } else if (value !== this.form.password) {
                callback(new Error('The passwords entered twice are inconsistent'));
              } else {
                callback();
              }
            },
            trigger: 'blur',
          },
        ],
        birthday: [{ required: true, trigger: 'blur' }],
        phone: [
          { required: true, trigger: 'blur' },
          { pattern: /^1[3456789]\d{9}$/, message: 'Please enter the correct phone number', trigger: ['blur', 'change'] },
        ],
      },
    };
  },
});
</script>
<style scoped>
.register {
  width: 400px;
  margin: 50px auto;
  text-align: center;
}
.register-form {
  margin-top: 20px;
  text-align: center;
}
.el-button{
  text-align: center;
}
</style>












<!-- <template>
  <div style="font-size: xx-large;">
    此
  </div>
  <router-link to="/staff">如登陆后为工作人员点击此处跳转</router-link>
</template>

<script lang="ts">
import {
  ElInput,
  ElButton,
  ElSelect,
} from "element-plus"
import { defineComponent } from "vue";

export default defineComponent({
  name:"Login",
  data(){
    return{
      
    };
  },

  methods: {
    initData(){
      
    }
  },

  created(){
    this.initData()
  },

  components:{
    ElInput,
    ElButton,
    ElSelect
  }

})



</script>

<style scoped>
.box{
  padding: 100px
}
</style> -->

<template>
  <div class="login-wrap">
    <video loop autoplay>
      <source src="@/assets/video/beauty.mp4" />
    </video>

    <div class="ms-login">
      <div class="ms-title">后台管理系统</div>

      <el-form
        ref="ruleFormRef"
        :model="ruleForm"
        status-icon
        :rules="rules"
        label-width="85px"
        class="demo-ruleForm"
        label-position="left"
      >
        <el-form-item label="手机号" prop="mobile">
          <el-input
            v-model="ruleForm.mobile"
            type="text"
            autocomplete="off"
            maxlength="11"
            class="ms-body-text"
            placeholder="请输入手机号"
            :prefix-icon="User"
          />
        </el-form-item>

        <el-form-item label="密 码" prop="password">
          <el-input
            v-model="ruleForm.password"
            type="password"
            autocomplete="off"
            class="ms-body-text"
            placeholder="请输入密码"
            show-password
            :prefix-icon="Hide"
          />
        </el-form-item>

        <el-form-item>
          <el-button
            type="primary"
            @click="submitForm(ruleFormRef)"
            style="margin-left: 50px; width: 100px; height: 40px"
            >登 录</el-button
          >
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from "vue";
import type { FormInstance, FormRules } from "element-plus";
import { User , Hide } from '@element-plus/icons-vue'

const ruleFormRef = ref<FormInstance>();

const ruleForm = reactive({
  mobile: "",
  password: "",
});

const validateMobile = (rule: any, value: any, callback: any) => {
  if (value === "") {
    callback(new Error("请输入手机号"));
  } else {
    const reg = /^1[3|4|5|7|8][0-9]\d{8}$/;
    const isPhone = reg.test(value);
    value = Number(value);
    if (typeof value === "number" && !isNaN(value)) {
      value = value.toString();
      if (value.length < 0 || value.length > 12 || !isPhone) {
        callback(new Error("手机号码格式有误"));
      } else {
        callback();
      }
    }
  }
};

const validatePassword = (rule: any, value: any, callback: any) => {
  if (value === "") {
    callback(new Error("请输入密码"));
  } else {
    callback();
  }
};

// const checkAge = (rule: any, value: any, callback: any) => {
//   if (!value) {
//     return callback(new Error("Please input the age"));
//   }
//   setTimeout(() => {
//     if (!Number.isInteger(value)) {
//       callback(new Error("Please input digits"));
//     } else {
//       if (value < 18) {
//         callback(new Error("Age must be greater than 18"));
//       } else {
//         callback();
//       }
//     }
//   }, 1000);
// };
// const validateEmail = (rule: any, value: any, callback: any) => {
//   if (value === "") {
//     callback(new Error("请输入邮箱"));
//   } else {
//     const reg = /^[a-z0-9]+([._\\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$/;
//     const email = reg.test(value);
//     if(!email){
//       callback(new Error('邮箱格式有误'))
//     }else{
//       callback();
//     }
//   }
// };

const rules = reactive<FormRules<typeof ruleForm>>({
  mobile: [{ validator: validateMobile, trigger: "blur" }],
  password: [{ validator: validatePassword, trigger: "blur" }],
});

const submitForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return;
  formEl.validate((valid) => {
    if (valid) {
      
    } else {
      console.log("error submit!");
      return false;
    }
  });
};

// const resetForm = (formEl: FormInstance | undefined) => {
//   if (!formEl) return;
//   formEl.resetFields();
// };
</script>

<style scoped>
.login-wrap {
  position: relative;
  width: 100%;
  height: 100%;
  /* background-image: url("../assets/../img/img.jpg"); */
  background-size: 100%;
}
.ms-title {
  width: 100%;
  line-height: 50px;
  text-align: center;
  font-size: 20px;
  color: #fff;
  border-bottom: 1px solid #ddd;
}
.ms-login {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 350px;
  margin: -190px 0 0 -175px;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.3);
  overflow: hidden;
}

.ms-body-text {
  right: 20px;
}
>>> .el-form-item__label {
  color: #fff;
  height: 80px;
  font-size: 16px;
  padding: 24px 12px 0 7px;
}
>>> .el-form-item__error {
  top: 80%;
}
video {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>

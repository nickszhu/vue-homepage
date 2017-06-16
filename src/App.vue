<template>
  <div id="app">
    <div class = "header-wrapper">
      <div class = "header"></div>
    </div>
    <div class = "main-container">
      <div class="page-container">
        <div class="nav-ctn">
          <el-menu default-active="2" class="el-menu-vertical-demo" @open="handleOpen" @close="handleClose" theme="light">
            <el-submenu index="1">
              <template slot="title">导航一</template>
              <el-menu-item-group title="分组一">
                <el-menu-item index="1-1">选项1</el-menu-item>
                <el-menu-item index="1-2">选项2</el-menu-item>
              </el-menu-item-group>
              <el-menu-item-group title="分组2">
                <el-menu-item index="1-3">选项3</el-menu-item>
              </el-menu-item-group>
              <el-submenu index="1-4">
                <template slot="title">选项4</template>
                <el-menu-item index="1-4-1">选项1</el-menu-item>
              </el-submenu>
            </el-submenu>
            <el-menu-item index="2">导航二</el-menu-item>
            <el-menu-item index="3">导航三</el-menu-item>
          </el-menu>
        </div>
        <div class="info-ctn">
          <div class="info-subctn">
            <h1>姓名</h1>
            <el-input v-model="inputName" placeholder="请输入内容"></el-input>
          </div>
          <div class="info-subctn">
            <h1>教育经历</h1>
            <el-form :model="dynamicValidateForm" 
            ref="dynamicValidateForm" 
            label-width="100px" 
            class="demo-dynamic">
              <el-form-item label="本科">
                <el-input></el-input>
              </el-form-item>
              <el-form-item
              v-for="(domain, index) in dynamicValidateForm.domains"
              :label="'经历' + index"
              :key="domain.key"
              :prop="'domains.' + index + '.value'">
                <el-input v-model="domain.value"></el-input>
                <el-button @click.prevent="removeDomain(domain)">删除</el-button>
              </el-form-item>
              <el-form-item>
                <el-button @click="addDomain">新增经历</el-button>
                <el-button @click="resetForm('dynamicValidateForm')">重置</el-button>
                <el-button type="primary" @click="submitForm('dynamicValidateForm')">提交</el-button>
              </el-form-item>
            </el-form>

          </div>
          <div class="info-subctn">
            <h1>工作经历</h1>
            <el-input
  type="textarea"
  :rows="2"
  placeholder="请输入内容"
  v-model="textarea1">
</el-input>
          </div>

          <div class="info-subctn">
            <h1>个人项目</h1>
            <el-input
  type="textarea"
  :rows="2"
  placeholder="请输入内容"
  v-model="textarea2">
</el-input>
          </div>
          <div class="info-subctn">
            <h1>GitHub</h1>
            <el-input v-model="inputgh" placeholder="请输入内容"></el-input>

          </div>
          <div class="info-subctn"></div>
          <div class="info-subctn"></div>
        </div>
      </div>

    </div>

  </div>
</template>

<script>
  export default {
    data () {
      return {
        inputName: '',
        inputgh:'',
        dynamicValidateForm: {
          domains: [{
            value: ''
          }]
        },
        textarea1: '',
        textarea2: ''  
      }
    },

    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      },
      removeDomain(item) {
        var index = this.dynamicValidateForm.domains.indexOf(item)
        if (index !== -1) {
          this.dynamicValidateForm.domains.splice(index, 1)
        }
      },
      addDomain() {
        this.dynamicValidateForm.domains.push({
          value: '',
          key: Date.now()
        });
      }
    }
  }
</script>

<style>
  body {
    font-family: Helvetica, sans-serif;
  }

  *{
    margin: 0;
    padding: 0;
  }

  html,body{
    height: 100%;
  }

  .header{
    height: 80px;
    width: 100%;
    background-color: #20a0ff;
  }

  .main-container{
    width:100%;
    margin-top: -80px;
    padding: 80px 0 0 0;
    height: 100%;
  }

  .page-container{
    padding: 50px 30px;
    height: 100%;
  }

  .nav-ctn{
    width: 25%;
    height: 100%;
    background-color: grey;
    float:left;
  }

  .info-ctn{
    width: 75%;
    height: 100%;
    background-color: #ffa;
    float:left;
  }
</style>

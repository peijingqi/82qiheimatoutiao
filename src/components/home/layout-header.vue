<template>
  <el-row class="layout-header" type="flex" justify="space-between">
    <el-col :span="6" class="left">
      <i class="el-icon-s-unfold" icon></i>
      <span>江苏传智播客教育科技股份有限公司</span>
    </el-col>
    <el-col :span="3" class="right">
      <img class="head-img" :src="userInfo.photo ? userInfo.photo:defaultImg" alt />
      <el-dropdown trigger="click">
        <span class="el-dropdown-link">
          {{userInfo.name}}
          <i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item icon="el-icon-plus">个人信息</el-dropdown-item>
          <el-dropdown-item icon="el-icon-circle-plus">地址</el-dropdown-item>
          <el-dropdown-item icon="el-icon-circle-plus-outline">退出</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
    </el-col>
  </el-row>
</template>

<script>
export default {
  data () {
    return {
      userInfo: {},
      defaultImg: require('../../assets/img/avatar.jpg')
    }
  },
  methods: {
    getUserTnfo () {
      let token = window.localStorage.getItem('user-token')
      this.$axios({
        url: '/user/profile',
        headers: { Authorization: `Bearer ${token}` }
      }).then(result => {
        this.userInfo = result.data.data
      })
    }
  },
  created () {
    this.getUserInfo()
  }
}
</script>

<style lang="less" scoped>
.layout-header {
  padding: 10px 0;
  .left {
    .icon {
      font-size: 22px;
      margin-right: 100px;
    }
    display: flex;
    align-items: center;
  }
}
.right {
  display: flex;
  align-items: center;
  .head-img {
    border-radius: 50%;
    margin-right: 5px;
    width: 40px;
    height: 40px;
  }
}
</style>

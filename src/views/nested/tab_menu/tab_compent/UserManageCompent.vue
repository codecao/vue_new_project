<template>
  <div>用户管理用户管理用户管理用户管理 {{name}}
     <div @click="childClick">获取用户信息</div>
  </div>
 
</template>
 
<script>
export default {
  name: "UserManageCompent",
  props: {
    name: String,
    require: false
  },
  data() {
    return {  
      childValue: "我是子组件的数据"
    }
  },
  methods: {
    childClick: function(e) {
      this.$emit("childByValue", this.childValue);
    }
  },
  created: function() {
    console.log("this.$router....", this.$router);
  }
};
</script>

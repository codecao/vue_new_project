<template>
  <div style="padding:30px;">
    <el-tabs type="border-card" @tab-click="choseCompent">
      <template v-for="item in menu">
        <el-tab-pane :label="item" :key="item">
          <UserManageCompent :is="compentName" :name="name" v-if="name" v-on:childByValue="childByValue"></UserManageCompent>
        </el-tab-pane>
      </template>
    </el-tabs>
  </div>
</template>


<script>
import UserManageCompent from "./tab_compent/UserManageCompent";
export default {
  name: "TabMenu",
  data() {
    return {
      compentName: "UserManageCompent",
      menu: ["用户管理", "配置管理", "角色管理", "定时任务补偿"],
      name: "for Parent"
    };
  },
  components: {
    UserManageCompent
  },
  methods: {
    choseCompent: function(e) {
      var that = this;
      var index = e.index;
      that.compentName = index == 0 ? "UserManageCompent" : "";
      console.log("$that.......", this);
      console.log("$http.......", that.$http);
      that.$http
        .get("/api/Huodong/hdxcx/QuanziHuodong.aspx", {
          params: {
            //params参数必写 , 如果没有参数传{}也可以
            device_type: 2,
            clubid: 4,
            page: 1,
            pagesize: 3
          }
        })
        .then(res => {
          console.log("res........", res);
        })
        .catch(function(error) {
          console.log(error);
        });
    },
    childByValue: function(e) {
      console.log("for child Value...", e);
      this.name=e;
    }
  },
  created: function() {
    console.log("this.$router....", this.$router);
  }
};
</script>

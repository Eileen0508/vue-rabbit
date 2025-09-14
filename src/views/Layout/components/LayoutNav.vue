<script setup>
</script>

<template>
  <nav class="app-topnav">
    <div class="container">
      <ul>
        <template v-if="true">
          <li>
            <a href="javascrip:;">
              <i class="iconfont icon-user"></i>
              周杰伦
            </a></li>
          <li>
            <el-popconfirm title="确认退出吗？" confirm-button-text = "确认"  cancel-button-text = "取消" >
              <template #reference>
                <a href="javascrip:;">退出登录</a>
              </template>
            </el-popconfirm>
          </li>
          <li>
            <a href="javascrip:;">我的订单</a>
          </li>
          <li>
            <a href="javascrip:;">会员中心</a>
          </li>
        </template>
        <template v-else>
            <a href="javascrip:;">请先登录</a>
            <a href="javascrip:;">帮助中心</a>
            <a href="javascrip:;">关于我们</a>
        </template>
      </ul>
    </div>
  </nav>
</template>

<style scoped lang="scss">
.app-topnav{
  background: #333;
  ul{
    display: flex;
    height: 53px;
    justify-content: flex-end;
    align-items: center;
    li{
      a{
        padding: 0 15px;
        color: #cdcdcd;
        line-height: 1;//设置文本的行高（行间距）为 1，即行高等于字体大小。
        display: inline-block;

        i {
          font-size: 14px;
          margin-right: 2px;
        }

        // &：代表父选择器，&:hover 等价于 a:hover
        &:hover {
          color: $xtxColor;
        }
      }
      //~ 通用兄弟选择器
      // 所有 <li> 之间都有分隔线，但最后一个没有右边框。
      ~li{
        a{
          border-left: 2px solid #666;
        }
      }
    }
  }
}
</style>
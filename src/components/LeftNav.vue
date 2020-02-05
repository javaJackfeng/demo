<template>
  <div class="leftnav">
    <ul>
      <li>
        <i class="icon iconfont icon-money"></i>
        <div>收银</div>
      </li>

      <li>
        <i class="icon iconfont icon-alipay"></i>
        <div>店铺</div>
      </li>

      <li>
        <i class="icon iconfont icon-icon-test3"></i>
        <div>商品</div>
      </li>

      <li>
        <i class="icon iconfont icon-icon-test1"></i>
        <div>会员</div>
      </li>

      <li>
        <i class="icon iconfont icon-icon-test"></i>
        <div>统计</div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "leftNav"
};
</script>

<style >
.leftnav {
  height: 100vh;
  background-color: #1d8ce0;
  color: #fff;
  font-size: 10px;
  float: left;
  width: 5%;
}
.iconfont {
  font-size: 24px;
}

.leftnav ul {
  padding: 0px;
  margin: 0px;
  height: 100%;
  display: flex;
  flex-direction: column;
  /* align-items: center; */
  justify-content: space-around;
}
.leftnav ul li {
  list-style: none;
}
</style>
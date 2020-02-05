<template>
  <el-row class="pos">
    <el-row>
      <el-col :span="7" id="el-row-left">
        <!-- 我是菜单栏 -->
        <el-tabs>
          <el-tab-pane label="点餐">
            <el-table :data="tableData" border style="width: 100%">
              <el-table-column prop="goodsName" label="商品"></el-table-column>
              <el-table-column prop="count" label="量" width="50"></el-table-column>
              <el-table-column prop="price" label="单价" width="70"></el-table-column>
              <el-table-column label="操作" width="100" fixed="right">
                <template slot-scope="scope">
                  <el-button type="text" size="small" @click="delSingleGoods(scope.row)">删除</el-button>
                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="totalDiv">
              <small>数量：</small>
              <strong>{{totalCount}}</strong> &nbsp;&nbsp;&nbsp;&nbsp;
              <small>总计：</small>
              <strong>{{totalMoney}}</strong> 元
            </div>
            <div class="div-btn">
              <el-button type="warning" @click="testAxios">挂单</el-button>
              <el-button type="danger" @click="delAllGoods()">删除</el-button>
              <el-button type="success" @click="checkout()">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单">挂单</el-tab-pane>
          <el-tab-pane label="外卖">外卖</el-tab-pane>
        </el-tabs>
      </el-col>
      <!--商品展示-->
      <el-col :span="17">
        <div class="often-goods">
          <div class="title">常用商品</div>
          <div class="often-goods-list">
            <ul>
              <li
                v-for="(goods,index) in oftenGoods"
                v-bind:key="index"
                @click="addOrderList(goods)"
              >
                <span>{{goods.goodsName}}</span>
                <span class="o-price">￥{{goods.price}}元</span>
              </li>
            </ul>
          </div>
        </div>
        <div class="goods-type">
          <el-tabs>
            <el-tab-pane label="汉堡">
              <ul class="cookList">
                <li v-for="type0 in type0Goods" :key="type0.id" @click="addOrderList(type0)">
                  <span class="foodImg">
                    <img :src="type0.goodsImg" width="100%" />
                  </span>
                  <span class="foodName">{{type0.goodsName}}</span>
                  <span class="foodPrice">￥{{type0.price}}元</span>
                </li>
              </ul>
            </el-tab-pane>
            <el-tab-pane label="小食">小食</el-tab-pane>
            <el-tab-pane label="饮料">饮料</el-tab-pane>
            <el-tab-pane label="套餐">套餐</el-tab-pane>
          </el-tabs>
        </div>
      </el-col>
    </el-row>
  </el-row>
</template>

<script>
import axios from "axios";
// Vue.prototype.axios=axios;
export default {
  name: "Pos",
  data() {
    return {
      //  this.totalCount=0; //汇总数量清0
      totalCount: 0,
      totalMoney: 0,
      tableData: [
        // {
        //   goodsName: "可口可乐",
        //   price: 8,
        //   count: 1
        // },
        // {
        //   goodsName: "香辣鸡腿堡",
        //   price: 15,
        //   count: 1
        // },
        // {
        //   goodsName: "爱心薯条",
        //   price: 8,
        //   count: 1
        // },
        // {
        //   goodsName: "甜筒",
        //   price: 8,
        //   count: 1
        // }
      ],
      oftenGoods: [
        // {
        //   goodsId: 1,
        //   goodsName: "香辣鸡腿堡",
        //   price: 18
        // },
        // {
        //   goodsId: 2,
        //   goodsName: "田园鸡腿堡",
        //   price: 15
        // },
        // {
        //   goodsId: 3,
        //   goodsName: "和风汉堡",
        //   price: 15
        // },
        // {
        //   goodsId: 4,
        //   goodsName: "快乐全家桶",
        //   price: 80
        // },
        // {
        //   goodsId: 5,
        //   goodsName: "脆皮炸鸡腿",
        //   price: 10
        // },
        // {
        //   goodsId: 6,
        //   goodsName: "魔法鸡块",
        //   price: 20
        // },
        // {
        //   goodsId: 7,
        //   goodsName: "可乐大杯",
        //   price: 10
        // },
        // {
        //   goodsId: 8,
        //   goodsName: "雪顶咖啡",
        //   price: 18
        // },
        // {
        //   goodsId: 9,
        //   goodsName: "大块鸡米花",
        //   price: 15
        // },
        // {
        //   goodsId: 20,
        //   goodsName: "香脆鸡柳",
        //   price: 17
        // }
      ],
      type0Goods: [
        // {
        //   goodsId: 1,
        //   goodsImg:
        //     "https://img.4008823823.com.cn/kfcios/Version/713_852038.jpg",
        //   goodsName: "香辣鸡腿堡",
        //   price: 18
        // },
        // {
        //   goodsId: 2,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
        //   goodsName: "田园鸡腿堡",
        //   price: 15
        // },
        // {
        //   goodsId: 3,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
        //   goodsName: "和风汉堡",
        //   price: 15
        // },
        // {
        //   goodsId: 4,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
        //   goodsName: "快乐全家桶",
        //   price: 80
        // },
        // {
        //   goodsId: 5,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
        //   goodsName: "脆皮炸鸡腿",
        //   price: 10
        // },
        // {
        //   goodsId: 6,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos004.jpg",
        //   goodsName: "魔法鸡块",
        //   price: 20
        // },
        // {
        //   goodsId: 7,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos001.jpg",
        //   goodsName: "可乐大杯",
        //   price: 10
        // },
        // {
        //   goodsId: 8,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos003.jpg",
        //   goodsName: "雪顶咖啡",
        //   price: 18
        // },
        // {
        //   goodsId: 9,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
        //   goodsName: "大块鸡米花",
        //   price: 15
        // },
        // {
        //   goodsId: 20,
        //   goodsImg: "http://7xjyw1.com1.z0.glb.clouddn.com/pos002.jpg",
        //   goodsName: "香脆鸡柳",
        //   price: 17
        // }
      ]
    };
  },
  mounted: function() {
    var leftHeight = document.body.clientHeight;
    console.log(leftHeight);
    document.getElementById("el-row-left").style.height = leftHeight + "px";
  },
  created: function() {
    this.$axios
      .get("/")
      .then(response => {
        console.log(response);
        // this.tableData=response.data.tableData;
        this.oftenGoods=response.data.oftenGoods;
        this.type0Goods=response.data.type0Goods;
      })
      .catch(error => {
        console.log(error);
        // alert('网络错误，不能访问');
      });
  },
  methods: {
    testAxios() {
      this.$axios
        .get("/")
        .then(response => {
          if (response.data) {
            console.log(response.data);
          }
        })
        .catch(err => {
          alert("请求失败");
        });
    },
    checkout() {
      if (this.totalCount != 0) {
        this.tableData = [];
        this.totalCount = 0;
        this.totalMoney = 0;
        this.$message({
          message: "结账成功，感谢你又为店里出了一份力!",
          type: "success"
        });
      } else {
        this.$message.error("不能空结。老板了解你急切的心情！");
      }
    },

    delAllGoods() {
      this.tableData = [];
      this.totalCount = 0;
      this.totalMoney = 0;
    },
    getAllMoney() {
      this.totalCount = 0;
      this.totalMoney = 0;
      if (this.tableData) {
        this.tableData.forEach(element => {
          this.totalCount += element.count;
          this.totalMoney = this.totalMoney + element.price * element.count;
        });
      }
    },
    delSingleGoods(goods) {
      console.log(goods);
      this.tableData = this.tableData.filter(o => o.goodsId != goods.goodsId);
    },
    addOrderList(goods) {
      this.totalCount = 0; //汇总数量清0
      this.totalMoney = 0;
      console.log("addOrderList()");
      let isHave = false;
      //  this.tableData.forEach((value,index)=>{
      //     console.log(value);
      //     if(value.goodsId==goods.goodsId){
      //        isHave=true;
      //     }
      //  });
      for (let i = 0; i < this.tableData.length; i++) {
        // console.log(this.tableData[i].goodsId);
        if (this.tableData[i].goodsId == goods.goodsId) {
          isHave = true; //存在
          break;
        }
      }
      if (isHave) {
        let arr = this.tableData.filter(o => o.goodsId == goods.goodsId);
        arr[0].count++;
      } else {
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        };
        this.tableData.push(newGoods);
      }
      this.tableData.forEach(element => {
        this.totalCount += element.count;
        this.totalMoney += element.price * element.count;
      });
    }
  }
};
</script>
<style scoped>
#el-row-left {
  border-right: 1px solid #c0ccda;
  background-color: #f9fafc;
}
.div-btn {
  margin-top: 10px;
}
.title {
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
}
.often-goods-list ul li {
  float: left;
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
}
.o-price {
  color: #58b7ff;
}
.goods-type {
  clear: both;
}
img {
  width: 100px;
  height: 100px;
}
.cookList li {
  list-style: none;
  width: 23%;
  border: 1px solid #e5e9f2;
  height: auto;
  overflow: hidden;
  background-color: #fff;
  padding: 2px;
  float: left;
  margin: 2px;
}
.cookList li span {
  display: block;
  float: left;
}
.foodImg {
  width: 40%;
}
.foodName {
  font-size: 18px;
  padding-left: 10px;
  color: brown;
}
.foodPrice {
  font-size: 16px;
  padding-left: 10px;
  padding-top: 10px;
}
</style>
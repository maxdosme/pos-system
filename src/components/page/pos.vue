<template>
  <div class="pos">
      <el-row>
        <el-col :span="7" class="pos-order" id="order-list">
          <el-tabs>
            <el-tab-pane label="点餐">
              <el-table :data="tableData" style="width: 100%">
                <el-table-column prop="goodsName" label="商品名称"></el-table-column>
                <el-table-column prop="count" label="数量"></el-table-column>
                <el-table-column prop="price" label="金额"></el-table-column>
                <el-table-column label="操作" fixed="right">
                  <template slot-scope="scoped">
                    <el-button type="text" size="small">删除</el-button>
                    <el-button type="text" size="small">增加</el-button>
                  </template>
                </el-table-column>
              </el-table>
              <div class="div-btn">
                <el-button type="warning">挂单</el-button>
                <el-button type="danger">删除</el-button>
                <el-button type="success">结账</el-button>
              </div>
            </el-tab-pane>
            <el-tab-pane label="挂单">
              挂单
            </el-tab-pane>
            <el-tab-pane label="外卖">
              外卖
            </el-tab-pane>
          </el-tabs>
        </el-col>
        <el-col :span="17">
          <div class="often-goods">
            <div class="title">常用商品</div>
            <div class="often-goods-list">
              <ul>
                <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                  <span>{{ goods.goodsName }}</span>
                  <span class="o-price">￥{{ goods.price }}元</span>
                </li>
              </ul>
            </div>
          </div>
          <div class="goods-type">
            <el-tabs>
              <el-tab-pane label="汉堡">
                <ul class="cookList">
                  <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                     <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                     <span class="foodName">{{ goods.goodsName }}</span>
                     <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="小食">
                <ul class="cookList">
                  <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                     <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                     <span class="foodName">{{ goods.goodsName }}</span>
                     <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="饮料">
               <ul class="cookList">
                  <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                     <span class="foodImg"><img :src="goods.goodsImg" width="100%"></span>
                     <span class="foodName">{{ goods.goodsName }}</span>
                     <span class="foodPrice">￥{{ goods.price }}元</span>
                  </li>
                </ul>
              </el-tab-pane>
              <el-tab-pane label="套餐">
               <ul class="cookList">
                  <li v-for="tGoods in type3Goods" @click="addOrderList(tGoods)">
                     <span class="foodImg"><img :src="tGoods.goodsImg" width="100%"></span>
                     <span class="foodName">{{ tGoods.goodsName }}</span>
                     <span class="foodPrice">￥{{ tGoods.price }}元</span>
                  </li>
                </ul>
              </el-tab-pane>
            </el-tabs>
          </div>
        </el-col>
      </el-row>
  </div>
</template>
<script>
// 引入axios插件
import axios from 'axios';
export default {
  name: 'pos',
  // 模拟数据
  data(){
    return {
      tableData: [],
      // 创建数据存储容器
      oftenGoods:[],
      type0Goods:[],
      type1Goods:[],
      type2Goods:[],
      type3Goods:[]
    }
  },
  // 创建后端数据请求
  created:function(){
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    // 使用箭头函数跨作用域
    .then(reponse=>{
      // console.log(reponse);
      this.oftenGoods = reponse.data;
    })
    .catch(error=>{
      // console.log(error);
      alert("网络错误，无法访问！");
    })


    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(reponse=>{
      this.type0Goods = reponse.data[0];
      this.type1Goods = reponse.data[1];
      this.type2Goods = reponse.data[2];
      this.type3Goods = reponse.data[3];      
    })
    .catch(error=>{
      alert("网络错误，无法访问！")
    })
  },
  mounted:function(){
    //  设置height:100%;
    var orderHeiht = document.body.clientHeight;
    // console.log(orderHeiht);
    document.getElementById('order-list').style.height = orderHeiht+'px';
  },
  methods:{
    addOrderList(goods){
      // 商品是否存在于列表中
      let _this = this;
      let isHave = false;
      for(let i = 0;i<_this.tableData.length;i++){
        if(_this.tableData[i].goodsId == goods.goodsId){
            isHave = true;
        }
      }
      // 根据判断的值处理业务逻辑
      if(isHave){
        // 改变列表商品数量
        let arr = _this.tableData.filter(o=>o.goodsId == goods.goodsId);
        arr[0].count++;
        // console.log(arr);
      }else {
        // 填入产品
        let newGoods = {
          goodsId: goods.goodsId,
          goodsName: goods.goodsName,
          price: goods.price,
          count: 1
        }
         // 填入商品列表
         _this.tableData.push(newGoods);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only(本范围内有效，不加=全局有效) -->
<style scoped>
  .pos-order {
    background-color: #f9fafc;
    border-right: 1px solid #c0ccda;
  }
  .div-btn {
    margin-top: 10px;
  }
  .title {
    height: 20px;
    border-bottom: 1px solid #d3dce6;
    background-color: #f9fafc;
    padding: 10px;
    text-align: left;
  }
  .often-goods-list ul li {
    list-style: none;
    float: left;
    border: 1px solid #e5e9f2;
    padding: 10px;
    margin: 10px;
    background-color: #fff;
    cursor: pointer;
  }
  .o-price {
    color: #58b7ff;
  }
  .goods-type {
    clear: both;
  }
  .cookList li{
    list-style: none;
    float: left;
    width: 23%;
    border: 1px solid #E5E9F2;
    height: auto;
    overflow: hidden;
    background-color: #fff;
    margin: 2px;
    padding: 2px;
    cursor: pointer;
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
    padding: 10px 0 0 10px;
  }
</style>

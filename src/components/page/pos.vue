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
        <el-col>
          我是产品栏
        </el-col>
      </el-row>
  </div>
</template>
<script>
export default {
  name: 'pos',
  // 模拟数据
  data(){
    return {
      tableData: [{
          goodsName: '可口可乐',
          price: 8,
          count:1
        }, {
          
          goodsName: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
         
          goodsName: '爱心薯条',
          price: 6,
          count:1
        }, {
         
          goodsName: '甜筒',
          price: 3,
          count:1
        }]
    }
  },
  mounted:function(){
    //  设置height:100%;
    var orderHeiht = document.body.clientHeight;
    // console.log(orderHeiht);
    document.getElementById('order-list').style.height = orderHeiht+'px';
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
</style>

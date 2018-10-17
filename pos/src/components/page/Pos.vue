<template>
 <div class="pos">
   <el-row>
     <el-col :span='7' class="pos-order" id="orderlist">
       <el-tabs type="border-card">
        <el-tab-pane label="点餐">
          <el-table :data="tableData" border show-summary style="width: 100%">
            <el-table-column prop="product"  label="商品名称" >
            </el-table-column>
            <el-table-column prop="count" width="60" label="数量">
            </el-table-column>
            <el-table-column prop="price" width="70" label="金额">
            </el-table-column>
            <el-table-column  label="操作" width="100" fixed="right">
              <template slot-scope="scope">
                <el-button type="text">添加</el-button>
                <el-button type="text">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
          <div class="btn">
            <el-button type="warning">挂单</el-button>
            <el-button type="danger">删除</el-button>
            <el-button type="success">结账</el-button>
          </div>
        </el-tab-pane>
        <el-tab-pane label="挂单">挂单</el-tab-pane>
        <el-tab-pane label="外卖">外卖</el-tab-pane>
      </el-tabs>
     </el-col>
     <el-col :span='17'>
       <div class="often-goods-list">
         <div class="title">常用商品</div>
         <div>
           <ul>
             <li v-for="(goods,index) in oftenGoods" :key="index">
               <span>{{goods.goodsName}}</span>
               <span class="o-price">￥{{goods.price}}元</span>
             </li>
           </ul>
         </div>
       </div>


       <div class="goods-type">
          <el-tabs type="border-card">
           <el-tab-pane label="汉堡">
            <ul class="cookList">
              <li v-for="(goods,index) in type0Goods " :key="index">
                <span class="foodImg">
                  <img :src="goods.goodsImg" />
                </span>
                <span class="foodName">{{goods.goodsName}}</span>
                <span class="foodPrice">￥{{goods.price}}元</span>
              </li>
            </ul>
           </el-tab-pane>
           <el-tab-pane label="小食">
             小食
           </el-tab-pane> 
            <el-tab-pane label="饮料">
              饮料
           </el-tab-pane>
            <el-tab-pane label="套餐">
              套餐
           </el-tab-pane>
         </el-tabs>
       </div>
     </el-col>
   </el-row>
 </div>
</template>

<script>
export default {
  name: 'pos',
  data () {
    return {
     tableData: [{
          product: '可口可乐',
          price: 8,
          count:1
        }, {
          product: '香辣鸡腿堡',
          price: 15,
          count:1
        }, {
          product: '爱心薯条',
          price: 8,
          count:1
        }, {
          product: '甜筒',
          price: 8,
          count:1
        }],
        oftenGoods:[
          {
              goodsId:1,
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
              goodsName:'香脆鸡柳',
              price:17
          }],
          type0Goods:[
          {
              goodsId:1,
              goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'香辣鸡腿堡',
              price:18
          }, {
              goodsId:2,
              goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'田园鸡腿堡',
              price:15
          }, {
              goodsId:3,
              goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'和风汉堡',
              price:15
          }, {
              goodsId:4,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'快乐全家桶',
              price:80
          }, {
              goodsId:5,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'脆皮炸鸡腿',
              price:10
          }, {
              goodsId:6,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'魔法鸡块',
              price:20
          }, {
              goodsId:7,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'可乐大杯',
              price:10
          }, {
              goodsId:8,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'雪顶咖啡',
              price:18
          }, {
              goodsId:9,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'大块鸡米花',
              price:15
          }, {
              goodsId:20,
               goodsImg:"https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2114375774,3087841129&fm=26&gp=0.jpg",
              goodsName:'香脆鸡柳',
              price:17
          }
      ],
    }
  },
  mounted() {
    var Height = document.body.clientHeight;
    console.log(Height);
    document.getElementById('orderlist').style.height = Height + 'px';
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.pos-order {
  background: #f9fafc;
  border-right: 1px solid #c0ccda;
  
}

.btn {
  margin-top: 10px;
  text-align:center;
}

.often-goods-list {
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
}
.title{
  height: 20px;
  border-bottom: 1px solid #d3dce6;
  background-color: #f9fafc;
  padding: 10px;
}

.often-goods-list ul li {
  list-style-type: none;
  /* float: left; */
  border: 1px solid #e5e9f2;
  padding: 10px;
  margin: 5px;
  background-color: #fff;
}

.o-price {
  color: #58b7ff;
}

.cookList li{
       list-style: none;
       width:23%;
       border:1px solid #E5E9F2;
       height: auto;
       overflow: hidden;
       background-color:#fff;
       padding: 2px;
       float:left;
       margin: 2px;
   }
   .cookList li span{
        display: block;
        float:left;
   }
   .foodImg{
       width: 40%;
   }
.foodImg img {
  width:100%;
}
   .foodName{
       font-size: 18px;
       padding-left: 10px;
       color:brown;
   }
   .foodPrice{
       font-size: 16px;
       padding-left: 10px;
       padding-top:10px;
   }
</style>

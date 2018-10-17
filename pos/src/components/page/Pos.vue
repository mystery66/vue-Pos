<template>
 <div class="pos">
   <el-row>
     <el-col :span='7' class="pos-order" id="orderlist">
       <el-tabs type="border-card">
        <el-tab-pane label="点餐">
          <el-table :data="tableData" border style="width: 100%" >
            <el-table-column prop="product"  label="商品名称" >
            </el-table-column>
            <el-table-column prop="count" width="60" label="数量">
            </el-table-column>
            <el-table-column prop="price" width="70" label="金额">
            </el-table-column>
            <el-table-column  label="操作" width="100" fixed="right">
              <template slot-scope="scope">
                <el-button type="text" size="small" @click="addGoodsList(scope.row)">添加</el-button>
                <el-button type="text" size="small" @click="handleDelete(scope.row)">删除</el-button>
              </template>
            </el-table-column>
          </el-table>
          <div class="total">
            <small>数量:</small>  {{totalCount}} &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; <small>总价:</small>  {{totalMoneny}}
          </div>
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
             <li v-for="(goods,index) in oftenGoods" :key="index" @click="addGoods(goods)">
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
              <li v-for="(goods,index) in typeGoods " :key="index"  @click="addGoods(goods)">
                <span class="foodImg">
                  <img :src="goods.goodsImg" />
                </span>
                <span class="foodName">{{goods.goodsName}}</span>
                <span class="foodPrice">￥{{goods.price}}元</span>
              </li>
            </ul>
           </el-tab-pane>
           <el-tab-pane label="小食">
             <ul class="cookList">
              <li v-for="(goods,index) in typeGoods1 " :key="index"  @click="addGoods(goods)">
                <span class="foodImg">
                  <img :src="goods.goodsImg" />
                </span>
                <span class="foodName">{{goods.goodsName}}</span>
                <span class="foodPrice">￥{{goods.price}}元</span>
              </li>
            </ul>
           </el-tab-pane> 
            <el-tab-pane label="饮料">
              <ul class="cookList">
              <li v-for="(goods,index) in typeGoods2 " :key="index"  @click="addGoods(goods)">
                <span class="foodImg">
                  <img :src="goods.goodsImg" />
                </span>
                <span class="foodName">{{goods.goodsName}}</span>
                <span class="foodPrice">￥{{goods.price}}元</span>
              </li>
            </ul>
           </el-tab-pane>
            <el-tab-pane label="套餐">
              <ul class="cookList">
              <li v-for="(goods,index) in typeGoods3 " :key="index"  @click="addGoods(goods)">
                <span class="foodImg">
                  <img :src="goods.goodsImg" />
                </span>
                <span class="foodName">{{goods.goodsName}}</span>
                <span class="foodPrice">￥{{goods.price}}元</span>
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
import axios from 'axios'
export default {
  name: 'pos',
  data () {
    return {
     tableData: [],
     oftenGoods: [],
     typeGoods: [],
     typeGoods1:[],
     typeGoods2:[],
     typeGoods3:[],
     totalCount: null,
     totalMoneny: null,
    }
  },
  created() {
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/oftenGoods')
    .then((res) => {
      console.log(res);
      this.oftenGoods = res.data;
    })
    .catch(err => {
      console.log(err);
    }),
    axios.get('https://www.easy-mock.com/mock/5b8b30dbf032f03c5e71de7f/kuaican/typeGoods')
    .then(res => {
      console.log(res.data);
      this.typeGoods=res.data[0];
      this.typeGoods1=res.data[1];
      this.typeGoods2=res.data[2];
      this.typeGoods3=res.data[3];
      
    })
    .catch(err => {
      console.log(err);
    })

  },
  mounted() {
    var Height = document.body.clientHeight;
    console.log(Height);
    document.getElementById('orderlist').style.height = Height + 'px';
  },
  methods: {
    addGoods(goods) {
      // console.log(goods.goodsName)
      let isHas = false;
     
      let len = this.tableData.length
      for(let i =0;i < len;i++) {
        console.log(this.tableData[i].goodsId)
        if(goods.goodsId == this.tableData[i].goodsId) {
          isHas = true;
        }
      }
      if(isHas) {
        let arr = this.tableData.filter(item =>  item.goodsId == goods.goodsId);
        console.log(arr);
        arr[0].count++;
       
      } else {
        let newarr = {goodsId: goods.goodsId, product:goods.goodsName,price:goods.price,count:1};
        this.tableData.push(newarr);
        
      }
      this.AllMoneny();
    },
    addGoodsList(row) {
      row.count++;
      this.AllMoneny();
    },
    handleDelete(row) {
      this.tableData.shift(row);
      this.AllMoneny()
    },
    AllMoneny(){
    console.log(1)
      this.totalCount = 0;
      this.totalMoneny = 0;
      if(this.tableData) {
        this.tableData.forEach(element => {
        this.totalCount += element.count;
        this.totalMoneny +=element.price * element.count;
      });
      }
  },
  
      
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
  text-align: center;
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
   .total {
     background: #fff;
     padding: 10px;
     border-bottom: 1px solid #dcdce6;
   }
</style>

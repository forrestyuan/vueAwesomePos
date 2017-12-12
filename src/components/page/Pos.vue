<template>
  <div class="pos">
      <el-row>
          <el-col :span='8' class="pos-order" id="order-list">
              <el-tabs>
                  <el-tab-pane label="点餐">
                      <el-table :data="tableData" border style="width:100%">
                          <el-table-column prop="goodsName" label="商品"></el-table-column>
                          <el-table-column prop="count" label="数量" width="60"></el-table-column>
                          <el-table-column prop="price" label="金额" width="60"></el-table-column>
                          <el-table-column label="操作" width="100" fixed="right">
                              <template scope="scope">
                                  <el-button type="text" size="small" @click="delSigleGoods(scope.row)">删除</el-button>
                                  <el-button type="text" size="small" @click="addOrderList(scope.row)">增加</el-button>
                              </template>
                          </el-table-column>
                      </el-table>
                      <div class="totalDiv">
                          <small> 数量</small>：{{totalCount}} <small>金额</small>： {{totalMoney}}元
                      </div>
                      <div class="div-btn">
                          <el-button type="warning">挂单</el-button>
                          <el-button type="danger" @click="delAllGoods">删除</el-button>
                          <el-button type="success" @click="checkout">结账</el-button>
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
          <el-col :span="16">
              <div class="o-goods">
                  <div class="o-title">热门商品</div>
                  <div class="o-list">
                      <ul>
                          <li v-for="goods in oftenGoods" @click="addOrderList(goods)">
                              <span>{{goods.goodsName}}</span>
                              <span class="o-price">￥{{goods.price}}</span>
                          </li>
                      </ul>
                  </div>
              </div>
              <div class="goods-type">
                  <el-tabs>
                    <el-tab-pane label="汉堡">
                        <div>
                            <dl v-for="typegood in type0Goods" class="cookList" @click="addOrderList(typegood)">
                                <dt class="foodImg"><img :src="typegood.goodsImg" :alt="typegood.goodsName"></dt>
                                <dd>
                                    <span class="foodName">{{typegood.goodsName}}</span>
                                    <span class="foodPrice">￥{{typegood.price}}</span>
                                </dd>
                            </dl>
                        </div>
                    </el-tab-pane>
                    <el-tab-pane  label="小食">
                        <div>
                            <dl v-for="typegood in type1Goods" class="cookList" @click="addOrderList(typegood)">
                                <dt class="foodImg"><img :src="typegood.goodsImg" :alt="typegood.goodsName"></dt>
                                <dd>
                                    <span class="foodName">{{typegood.goodsName}}</span>
                                    <span class="foodPrice">￥{{typegood.price}}</span>
                                </dd>
                            </dl>
                        </div>
                    </el-tab-pane >
                    <el-tab-pane  label="饮料">
                        <div>
                            <dl v-for="typegood in type2Goods" class="cookList" @click="addOrderList(typegood)">
                                <dt class="foodImg"><img :src="typegood.goodsImg" :alt="typegood.goodsName"></dt>
                                <dd>
                                    <span class="foodName">{{typegood.goodsName}}</span>
                                    <span class="foodPrice">￥{{typegood.price}}</span>
                                </dd>
                            </dl>
                        </div>
                    </el-tab-pane >
                    <el-tab-pane  label="套餐">
                        <div>
                            <dl v-for="typegood in type3Goods" class="cookList" @click="addOrderList(typegood)">
                                <dt class="foodImg"><img :src="typegood.goodsImg" :alt="typegood.goodsName"></dt>
                                <dd>
                                    <span class="foodName">{{typegood.goodsName}}</span>
                                    <span class="foodPrice">￥{{typegood.price}}</span>
                                </dd>
                            </dl>
                        </div>
                    </el-tab-pane >
                  </el-tabs>
              </div>
          </el-col>
      </el-row>
  </div>
</template>
<script>
    import axios from 'axios';
    export default{
        name:'pos',
        created:function(){
            axios.get('http://jspang.com/DemoApi/oftenGoods.php')
                .then(res=>{
                    console.log(res);
                    this.oftenGoods = res.data;
                })
                .catch(err=>{
                    console.log(err);
                    alert('商品读取失败，请刷新重试');
                });

             axios.get('http://jspang.com/DemoApi/typeGoods.php')
                .then(res=>{
                    console.log(res);
                    this.type0Goods = res.data[0];
                    this.type1Goods = res.data[1];
                    this.type2Goods = res.data[2];
                    this.type3Goods = res.data[3];
                })
                .catch(err=>{
                    console.log(err);
                    alert('商品读取失败，请刷新重试');
                });
        },
        mounted:function(){
            var oWindow;
            if(document.body){
                oWindow = document.body;
            }else if(document.documentElement){
                oWindow = docuement.documentElement;
            }else{
                oWindow = window;
            }
            var orderHeight=oWindow.clientHeight;
            console.log(orderHeight);
            document.getElementById('order-list').style.height = orderHeight + 'px';
            window.onresize=function(){
                 var orderHeight=oWindow.clientHeight;
                document.getElementById('order-list').style.height = orderHeight + 'px';
            }
        },
        data(){
            return{
                tableData:[],
                oftenGoods:[],
                type0Goods:[],
                type1Goods:[],
                type2Goods:[],
                type3Goods:[],
                totalMoney:0,
                totalCount:0
            }
        },
        methods:{
            addOrderList(goods){
                this.totalMoney = 0;
                this.totalCount = 0;
                //商品是否已存在与订单列表中。
                let isHave = false;
                for(let i=0; i<this.tableData.length; i++){
                    if(this.tableData[i].goodsId==goods.goodsId){
                        //改变数量
                        isHave=true;
                    }
                }
                //根据判断的值编写业务逻辑
                if(isHave){
                    //改变数量
                    let arr = this.tableData.filter(a=>a.goodsId == goods.goodsId);
                    arr[0].count++;
                }else{
                    let newGoods ={goodsId:goods.goodsId,goodsName:goods.goodsName,price:goods.price,count:1};
                    this.tableData.push(newGoods);
                }
                this.getAllmoney();
            },
            delSigleGoods(goods){
                //删除单个商品
                this.tableData = this.tableData.filter(o=>o.goodsId !=goods.goodsId);
                thia.getAllmoney();
            },delAllGoods(goods){
                this.tableData = [];
                this.totalMoney =0;
                this.totalCount = 0;
            },
            checkout(){
                if(this.totalCount != 0){
                    this.tableData = [];
                    this.totalMoney =0;
                    this.totalCount = 0;
                    this.$message({
                        message:'结账成功，感谢您的购买！',
                        type:'success'
                    });
                }else{
                    this.$message.error('您还没有添加任何商品！');
                }
            },
            getAllmoney(){
                this.totalMoney = 0;
                this.totalMoney = 0;
                if(this.tableData){
                    //计算汇总金额和数量
                    this.tableData.forEach((element)=>{
                        this.totalCount += element.count;
                        this.totalMoney =this.totalMoney+(element.price *element.count);
                    });
                }
            }
        }
    }   

</script>
<style scoped>
.pos-order{
    background-color: #F9fafc;
    border-right: solid 1px #c0ccDa;
    padding-left: 5px;
}
.div-btn{
    margin-top:10px; 
}
.o-title{
    height: 20px;
    border-bottom: solid 1px #D3dce6;
    background-color: #F9fafc;
    padding: 10px;
    text-align: left;
}
.o-goods{

}
.o-list ul li{
    position: relative;
    list-style: none;
    float: left;
    border: 1px solid #e5e9f2;
    margin:10px;
    background-color: #ffffff;
    padding: 5px;
    cursor: pointer;
}
.o-price{
    color:#58B7FF;

}
.goods-type{
    clear: both;
    padding-left: 5px;
    overflow: hidden;
}
.cookList{
    position: relative;
    background-color: #ffffff;
    overflow: hidden;
    color:#58B;
    margin: 5px;
    padding: 10px;
    float: left;
    width:160px;
    height: auto;
    border: solid 1px #ccc;
}
.cookList:hover{
    cursor: pointer;
    box-shadow: 2px 2px 5px 2px #ccc;
    color:red;
}
.cooklist dt{
    float: left;
}
.cooklist dd{
    float: right;
}
.foodImg img{
    float: left;
    width:50px;
    height: 50px;
}
.foodName{
    display: block;
}
.foodPrice{
    display: block;
}
.totalDiv{
    background-color: #fff;
    padding:10px;
    border-bottom: 1px solid #D3dce6
}
</style>

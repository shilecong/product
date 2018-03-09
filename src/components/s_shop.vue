<template>
    <div class="s_shop_all">
        <img src="../img/s_mine_img/cart.png" alt="" class="s_shop_all_img">
        <p  class="s_shop_p">{{ totalCount }} </p>
        <div class="s_shop_top" @click="show">满40减12</div>
        <div class="s_shop_show" :style="{display: display}">
            <div class="s_shop_show_food" v-for="product in ProductList" :key="product.id">
                <div class="s_shop_show_food_div">{{ product.name }}</div>
                <div class="l_price_div">
                    <!-- <img src="../img/s_mine_img/jian.png" alt="减去商品"> -->
                    <img src="../img/s_mine_img/jian.png" alt="减去商品" class="L_price_img1">
                    <span class="L_price_imgSpan">{{ product.count  }}</span>
                    <img src="../img/L_img/iconP5.jpg" alt="添加商品" class="L_price_img2"
                    @click="adds(product)">
                </div>
            </div>
        </div>
        <div class="s_shop">
           <div class="s_shop_left" @click="show">
               ￥{{ totalPrice.toFixed(2) }}
           </div>
           <router-link class="s_shop_right" to="/s_dingdan" :class="changeColor">
               {{ change ? '去结算':'请添加' }}
           </router-link>
       </div>
    </div>
</template>
    
<script>
export default {
    name: "s_shop",
    data () {
        return {
            change: false,
            display: 'none'
        };
    },
    methods: {
        show() {
            if(this.display ==  'none') {
                this.display =  'block'
            } else{
                this.display =  'none'
            }
        },
        adds(product) {
            // product.count++;
            // this.$store.dispatch('adds', product)
        },
    },
    // 我们一般会使用计算属性来获取vuex仓库中的数据
    computed: {
        ProductList() {
            return this.$store.state.cartProductList
        },
       	totalCount() {
			return this.$store.getters.totalCount
        },
		totalPrice() {
			return this.$store.getters.totalPrice
        },
        changeColor() {
            if(this.$store.getters.totalCount == 0) {
                this.change = false
                return 'red'
            }else if(this.$store.getters.totalCount > 0) {
                this.change = true
                return 'green'
            } 
        }
    }
}
</script>
    
<style lang="css" scoped>
    .red{
        background: gray;
    }
    .green{
        background: #4cd964; 
    }
    /* ==================== */
    .s_shop_show{
        width: 100%;
        /* height: auto ! important; */
        /* min-height: 2rem; */
        height: 2rem;
        overflow-x:scroll; 
        background: rgb(228, 223, 223);
    }
    .s_shop_show_food{
        width: 100%;
        height: .65rem;
        padding: 0 0 .2rem 0;
        line-height: .65rem;
    }
    .s_shop_show::-webkit-scrollbar {display: none;}
/* 
    .L_meishi_header_nav1{
    width: 7.5rem;
    overflow-x:scroll;     
    height: .7rem;    
    
}
.L_meishi_header_nav1::-webkit-scrollbar {display: none;}
    */
    .s_shop_show_food_div{
        width: 60%;
        text-align: center;
        font-size: .26rem;
        /* background: #4cd964; */
        float: left;
        margin-left: .1rem;
    }
    .l_price_div{
        float: right;
        width: 1.5rem;
        height: 100%;
        line-height: .6rem;
        /* background: white; */
        margin-right: .6rem;
        position: relative;
        text-align: center;
    }
/* .L_price_span{
    float: right;
    margin-left: .05rem;
    font-size: .12rem;
    color: #666666;
    text-decoration: line-through;
} */
.l_price_div img{
    border-radius: 50%;
    width: .45rem;
    height: .45rem;
    margin-top: .1rem;
}
.L_price_img1{
    position: absolute;
    left: 0;
    top:0;
}
.L_price_img2{
    position: absolute;
    right: 0;
    top:0;
}










    .s_shop_all{
        width: 100%;
        /* height: 1.36rem; */
        position: fixed;
        left: 0;
        bottom: 0;
    }
     .s_shop_all_img{
         width: 1rem;
         height: 1rem;
         border-radius: 50%;
         position: absolute;
         left: .24rem;
         bottom: .15rem;
     }
     .s_shop_p{
         width: .3rem;
         height: .28rem;
         line-height: .28rem;
         text-align: center;
         position: absolute;
         background: #ff6216;
         border-radius: 50%;
         left: .95rem;
         bottom: .87rem;
         color: white;
     }
    .s_shop_top{
        text-align: center;
        width: 100%;
        height: .4rem;
        background: #fffad7;
        border: .01rem solid #f9e8a6;
    }
    .s_shop{
        width: 100%;
        height: .96rem;
        background: #505051;
    }
    .s_shop_left{
        width: 5.4rem;
        height: .96rem;
        float: left;
        color: white;
        padding-top: .16rem;
        text-indent: 1.4rem;
        font-size: .4rem;
    }
      .s_shop_right{
        width: 2.1rem;
        height: .96rem;
        line-height: .96rem;
        text-align: center;
        float: left;
        color: white;
        font-size: .32rem;
        font-weight: bold;
    }
</style>
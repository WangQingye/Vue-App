<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul>
                <li v-for="item in goods">
                    <span class="text">
                        <span v-show="item.type>0" class="icon"></span>
                        {{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="food-wrapper"></div>
    </div>
</template>

<script type="text/ecmascript-6">
    export default {
        props: {
            seller: {
                type: Object
            }
        },
        data() {
            return {
                goods: []
            };
        },
        created() {
            this.classMap = ['decrease', 'discount', 'special', 'invoice', 'guarantee'];
            this.$http.get('/api/goods').then((response) => {
                response = response.body;
                console.log(response);
                if (response.code === 0) {
                    this.goods = response.goods;
                    console.log('goods1', this.goods);
                }
            });
        }
    };
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .goods
        display flex
        position absolute
        top 174px
        bottom 46px
        width 100%
        overflow hidden
        .menu-wrapper
            flex 0 0 80px
            width 80px
            background #f3f5f7
        .food-wrapper
            flex 1
</style>

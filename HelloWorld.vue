<template>
    <div class="bill-content">
        <div v-for="(item,index) in arr" :key="item.id" @touchstart.prevent="touchinUk(index)" @touchend.prevent="cleartime(index)">
            <div>
                <p>{{item.address}}</p>
                <p>备注：{{item.remarks}}</p>
            </div>
            <div>
                <i class="iconfont icon-gengduo"></i>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        data() {
            return {
                arr: [{
                        address: "安徽省苏州市连旱想",
                        remarks: "imtoken"
                    }, {
                        address: "安徽省亳州市司马组",
                        remarks: "大多数"
                    },
                    {
                        address: "安徽水果和共同我上课晚上开门",
                        remarks: "张是为为了"
                    },
                ]
            }
        },
        created() {},
        beforeRouteEnter(to, from, next) {
            next(vm => {
                vm.$parent.$data.showfooter = false
                vm.$parent.$data.showmenu = false
            })
        },
        beforeRouteLeave(to, from, next) {
            this.$parent.$data.showfooter = true
            this.$parent.$data.showmenu = true
            next()
        },
        methods: {
            touchinUk(index) {
                console.log(index)
                clearInterval(this.Loop); //再次清空定时器，防止重复注册定时器
                this.Loop = setTimeout(function() {
                    this.$dialog.confirm({
                        message: '是否删除地址'
                    }).then(() => {
                        console.log("删除")
                        this.arr.splice(index, 1);
                    }).catch(() => {
                        // on cancel
                        console.log("不删")
                    });
                }.bind(this), 1000);
            },
            cleartime(index) {
                // 这个方法主要是用来将每次手指移出之后将计时器清零
                clearInterval(this.Loop);
            }
        },
        components: {}
    }
</script>
<style scoped>
    .bill-content {
        background-color: #fff
    }
    .center {
        padding-top: 10px;
        padding-left: 8px;
        padding-right: 8px
    }
    .yd-navbar {
        border-bottom: 1px solid #ccc
    }
</style>



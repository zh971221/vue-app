<template>
    <briup-fulllayout title="常用地址">
     <van-list>
    <van-cell
    v-for="item in addresses"
    :key="item.id"
    :title="item.province+''+item.city+''+item.area+''+item.address"
    />
    <van-button block type="default" @click="toAddressEditHandler">添加</van-button>
     </van-list>
    </briup-fulllayout>
    
</template>

<script>
import {mapState} from 'vuex'
import {get}from '../../../http/axios'
export default {
    data(){
        return{
            addresses:[]
        }

    },
    computed:{//获取属性
        //将状态机中的user对象中的info对象获取到
        ...mapState("user",["info"])

    },
    created(){
        this.loadAddress();

    },
    methods:{
        //加载当前顾客地址信息
        loadAddress(){
            let id = this.info.id;
            let url = "/address/findByCustomerId?id= "+id;
            get(url).then((Response)=>{
                this.addresses = Response.data;
            })
        },
        toAddressEditHandler(){
            this.$router.push("/manager/address_edit")
        }
        

    }
}
</script>
<style scoped>

</style>
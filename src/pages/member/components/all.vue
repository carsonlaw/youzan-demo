<template>
    <div class="container " style="min-height: 597px;">
        <div class="block-list address-list section section-first js-no-webview-block">
            <a class="block-item js-address-item address-item" 
            :class="{'address-item-default':address.isDefault}" 
            @click="toEdit(address)" v-for="address in addressList" :key="address.id"
            v-if="addressList"
            >
            <div class="address-title">{{address.name}} {{address.tel}}</div>
            <p>{{address.provinceName}}{{address.cityName}}{{address.districtName}}{{address.address}}</p>
            </a>
        </div>
        <div v-show="!addressList.length" style="text-align:center;font-size:16px;">没有地址啦，请新增~</div>
        <div class="block stick-bottom-row center">
            <router-link class="btn btn-blue js-no-webview-block js-add-address-btn" :to="{name:'form',query:{type:'add'}}">
                新增地址
            </router-link>
        </div>
    </div>
</template>
<style>
    @import 'address_base.css';
    @import 'address.css';
</style>
<script>
import address from 'js/addressService.js'
export default {
    data(){
        return {
        }
    },
    computed:{
        addressList(){
            if(this.$store.state.lists){
                return this.$store.state.lists
            }
            return false
        }
    },
    created(){
        // address.getList().then(response=>{
        //     this.addressList=response.data.lists
        // })
        if (!this.addressList){
            this.$store.dispatch('getLists')
        }
    },
    methods:{
        toEdit(data){
            this.$router.push({path:'form',query:{
                type:'edit',
                instance:data
            }})
        }
    }
}
</script>
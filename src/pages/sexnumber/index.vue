<template>
    <div class="num">
        <div class="num-title">
            报名总人数累计达
        </div>
        <div class="num-num">
            <div v-for="(item,index) in total_number" :key="index">{{item}}</div>
        </div>
        <img class="girl"  v-if="imgUrl" :src="imgUrl+'girl.png'"/>
        <div class="girl-num">{{full_info.woman}}</div>
        <img class="follower"  v-if="imgUrl" :src="imgUrl+'3.png'"/>
        <img class="boy"  v-if="imgUrl" :src="imgUrl+'boy.png'"/>
        <div class="boy-num">{{full_info.man}}</div>
        <div class="jump">
            <div class="jump-title">跨部门人数</div>
            <div class="jump-num">{{full_info.crossNumber}}</div>
        </div>
        <div class="line1">
        </div>
        <div class="line2">
        </div>
        <div class="line3">
        </div>
        <img class="bottom" v-if="imgUrl" :src="imgUrl+'10.png'"/>
    </div>
</template>
<script>
import {getMembersDetail} from '@/apis/api'
import {getStorageSync} from '@/utils/index'
const departMap={
    '网络技术工作室':'1',
    '环保部':'2',
    '红十字会':'3',
    '交流部':'4',
    '培训部':'5',
    '支教部':'6',
    '宣传部':'7',
    '项目部':'8',
    '活动部':'9',
    '统事部':'10',
    '决策层':'11',
}
export default {
    data() {
        return {
            imgUrl: this.GLOBAL.localImg,
            sex: 'man',
            userData:null,
            total_number:null,
            full_info:{
                woman:0
            },
        }
    },
    methods:{
        _getUserData(){
            this.userData=getStorageSync('userInfo');
            console.log(this.userData)
        },
        _getNumbers(){
            getMembersDetail({
                department:departMap[this.userData.department],
            }).then(res=>{
                this.full_info=res.data.data;
                this.total_number=this._totalInit(this.full_info.enrollNumber);
            })
        },
        _totalInit(number){
            let newArr=String(number).split('');
            return newArr;
        }
    },
    onLoad(){
        this._getUserData();
        this._getNumbers();
    },
    onShow(){
        this._getUserData();
        this._getNumbers();
    }
}
</script>
<style lang="scss" scoped>
.num{
    padding: 30rpx;
    &-title{
        font-size: 44rpx;
    }
    &-num{
        display: flex;
        justify-content: center;
        margin-top: 60rpx;  
        div{
            // width: 
            width: 150rpx;
            height: 230rpx;
            line-height: 230rpx;
            text-align: center;
            margin-right: 30rpx;
            border-radius: 15rpx;
            font-size: 120rpx;
            background-color: rgba(225, 225, 225, 0.12);
            box-shadow: 1px 1px 1px 1px rgba(170, 170, 170, 1);
            border: 1px solid rgba(255, 255, 255, 0);
            font-weight: 500;
        }
    }
}
.girl{
    width: 168rpx;
    height: 260rpx;
    position: absolute;
    top: 410rpx;
    left: 80rpx;
}
.girl-num{
    position: absolute;
    left: 270rpx;
    top: 450rpx;
    font-size: 120rpx;
    color: rgba(236, 114, 137, 1);
}
.boy{
    width: 168rpx;
    height: 260rpx;
    position: absolute;
    right: 60rpx;
    top: 630rpx;
}
.boy-num{
    position: absolute;
    left: 330rpx;
    top: 682rpx;
    font-size: 120rpx;
    color: #5792DF;
}
.follower{
    height: 116rpx;
    width: 210rpx;
    position: absolute;
    left: 428rpx;
    top: 418rpx;
}
.jump{
    width: 200rpx;
    height: 300rpx;
    position: absolute;
    top: 740rpx;
    left: 60rpx;
    text-align: center;
    font-size: 40rpx;
    margin-top: 20rpx;
    &-num{
        font-size: 120rpx;
        margin-top: 5rpx;
        color: #5A976C;
    }
}
.bottom{
    width: 480rpx;
    height: 260rpx;
    position: absolute;
    bottom: 0;
    right: 0;
}
.line1{
    height: 0rpx;
    width: 240rpx;
    position: absolute;
    top: 705rpx;
    left: 29px;
    box-shadow: 2rpx 2rpx 2rpx 0px rgba(190, 77, 217, 1);
    border: 1rpx solid rgba(224, 163, 238, 1);
}
.line2{
    height: 0rpx;
    width: 258rpx;
    position: absolute;
    top: 641rpx;
    left: 285rpx;
    box-shadow: 2rpx 2rpx 2rpx 0px #67AFE3;
    border: 1rpx solid #67AFE3;
    transform:rotate(-30deg);
}
.line3{
    height: 0rpx;
    width: 258rpx;
    position: absolute;
    top: 838rpx;
    left: 171rpx;
    box-shadow: 2rpx 2rpx 2rpx 0px #7E9F78;
    border: 1rpx solid #7E9F78;
    transform:rotate(-90deg);
}
</style>

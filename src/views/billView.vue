<template>
    <main>
        <div class="bg-dark text-white text-center py-3 mb-3">停車費繳費</div>
        <div class="container">
            <div class="plate-bg">
                {{ billDetail.plate }}
            </div>
            <div class="billDetail mt-2">
                <div class="detailContent">
                    <div class="amount">
                        <p class="text-secondary pt-3 ps-3">應繳金額</p>
                        <p class="text-center">NT$ <span class="fs-3">{{ billDetail.amount }}</span></p>
                    </div>
                    <div class="detail">
                        <p class="text-secondary">停車地點<span class="text-primary">　{{ billDetail.location }}</span></p>
                        <p class="text-secondary">進場時間<span class="text-primary">　{{ billDetail.inTime }}</span></p>
                        <p class="text-secondary">折抵時數<span class="text-primary">　{{ billDetail.totalDiscount }} 小時</span>
                        </p>
                    </div>
                    <div class="btns d-flex justify-content-around">
                        <button class="btn btn-primary">發票折抵</button>
                        <button class="btn" :class="billDetail.amount == 0 ? 'btn-secondary' : 'btn-primary'">繳費離場</button>
                    </div>
                    <div v-if="billDetail.amount == 0" class="warningInfo">
                        <p class="text-success fs-6 mt-1"><img src="../assets/icons8-info-success.svg" alt="info-icon">
                            無需繳費，請儘速離場，謝謝！</p>
                    </div>
                    <div class="discountDetail mt-2 pb-2">
                        <p class="text-center">折抵明細</p>
                        <p class="text-secondary">緩衝時間<span class="text-primary">　{{ billDetail.discount.buffer }} 小時</span>
                        </p>
                        <p class="text-secondary">發票折抵<span class="text-primary">　{{ billDetail.discount.coupon }} 小時</span>
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>
  
<script>
import { RouterLink, RouterView } from 'vue-router'
import router from '../router';
const { VITE_APP_URL, VITE_APP_PATH } = import.meta.env

export default {
    data() {
        return {
            isLoading: false,
            billDetail: {
                plate: "ABC-1111",
                amount: 50,
                location: '台中誠品',
                inTime: '2023-01-01 11:11:11',
                totalDiscount: 1,
                discount: {
                    buffer: 0.5, // 緩衝時間
                    coupon: 0.5
                }
            }
        }
    },
    components: {
        RouterView,
        RouterLink,
    },
    methods: {}
}
</script>

<style>
.plate-bg {
    background-image: url(../assets/blank_plate3-sm.png);
    background-repeat: no-repeat;
    max-height: auto;
    background-position: center;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 30px 0;
    font-size: 32px;
}

.billDetail {
    width: 324px;
    margin: 0 auto;
    /* offset-x | offset-y | blur-radius | spread-radius | color */
    box-shadow: 2px 2px 25px 2px rgba(0, 0, 0, 0.2);
}

.detailContent {
    max-width: 265px;
    margin: 0 auto;
}

.amount {
    border-bottom: 1px solid gray;
}
</style>
  
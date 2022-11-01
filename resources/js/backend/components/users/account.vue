<template>
    <div>


        <div class="layout-content">
              <!---->
              <div data-v-baaa4d88="" style="padding: 20px 20px 70px;">
                 <div data-v-baaa4d88="" class="van-row van-row--flex van-row--justify-center">
                    <div data-v-baaa4d88="" class="van-col van-col--4" style="padding-right: 13.3333px;">
                       <div data-v-baaa4d88="" class="van-image van-image--round" style="width: 50px; height: 50px;"><img src="https://beximco66.com/static/img/tx0.3e21444c.svg" class="van-image__img"></div>
                    </div>

                    <div data-v-baaa4d88="" class="col van-col van-col--8" style="padding-left: 6.66667px; text-align: left; padding-right: 6.66667px;"><span data-v-baaa4d88="">{{ row.user.mobile }}</span></div>

                     <button data-v-baaa4d88="" class="van-button van-button--info van-button--normal van-button--plain van-button--block van-button--round" style="background: rgb(54, 64, 78); color: rgb(181, 138, 72); border: none;">আমন্ত্রণ কোড: {{ row.user.username }} </button>

                 </div>

                 <div data-v-baaa4d88="" class="my-info-grid van-grid">
                    <div data-v-baaa4d88="" class="van-grid-item" style="flex-basis: 50%;">
                        <span data-v-baaa4d88="">ভারসাম্য</span><!---->
                        <span class="van-grid-item__text">{{ parseFloat(row.user.balance).toFixed(2) }}</span>
                    </div>
                    <div data-v-baaa4d88="" class="van-grid-item" style="flex-basis: 50%;">
                        <span data-v-baaa4d88="">আজ কাজের চাপ</span><!---->
                        <span class="van-grid-item__text">{{ parseFloat(row.taskearn).toFixed(2) }}</span>
                    </div>
                    <!-- <div data-v-baaa4d88="" class="van-grid-item" style="flex-basis: 50%;">
                        <span data-v-baaa4d88="">অর্থ</span>
                        <span class="van-grid-item__text">00000</span>
                    </div>
                    <div data-v-baaa4d88="" class="van-grid-item" style="flex-basis: 50%;">
                        <span data-v-baaa4d88="">স্থূল আয়</span>
                        <span class="van-grid-item__text">0.00</span>
                    </div> -->
                 </div>



                 <div data-v-baaa4d88="" class="van-row van-row--flex van-row--justify-center">
                     <router-link :to="{name:'Recharge'}" data-v-baaa4d88="" style="text-align: center;display: flex;justify-content: center;align-items: center;color: white;text-decoration: none;" class="money-btn van-button van-button--primary van-button--normal van-button--block">রিচার্জ</router-link>
                     <router-link :to="{name:'Withdraw'}"  data-v-baaa4d88="" style="text-align: center;display: flex;justify-content: center;align-items: center;color: white;text-decoration: none;" class="money-btn van-button van-button--primary van-button--normal van-button--block">প্রত্যাহার</router-link>
                 </div>






                <a href="#" data-v-baaa4d88="" class="van-cell__title"><span data-v-baaa4d88="" class="van-tag van-tag--warning">বন্ধুদের আমন্ত্রণ করুন</span></a>


           <router-link :to="{name:'teamMember'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">আমার দল</router-link>
           <router-link :to="{name:'orders'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">অ্যাকাউন্টের বিশদ বিবরণ</router-link>
           <router-link :to="{name:'rechargeHistory'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">টপ-আপ ইতিহাস</router-link>
           <router-link :to="{name:'WithdrawHistory'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">প্রত্যাহারের ইতিহাস</router-link>
           <router-link :to="{name:'bankAccount'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">ওয়ালেট সেটিংস</router-link>
           <router-link :to="{name:'RechangePass'}" data-v-baaa4d88="" role="button" tabindex="0" class="info-cell van-cell van-cell--clickable van-cell--borderless">পাসওয়ার্ড সেটিংস</router-link>

           <router-link :to="{name:'logout'}" data-v-baaa4d88="" style="display: flex;justify-content: center;align-items: center;color: white !important;" class="money-btn van-button van-button--primary van-button--normal van-button--block">সাইন আউট করুন</router-link>

              </div>
           </div>





<!--




        <section id="topbar">
            <div class="title">
                <a href="javascript:void(0)" @click="$router.go(-1)" ><i class="fa fa-angle-left"></i></a>
                <p>{{ $t('My_Account.value') }}</p>
                <LanguageComponent/>
            </div>
        </section>


        <section class="accontDetails">
            <div class="row">
                <div class="col-md-6">


                            <h6 class="card-title">{{ $t('Name.value') }} : {{ row.user.name }}</h6>
                            <h6 class="card-title">{{ $t('Plan.value') }} : {{ row.plans.name }}</h6>
                            <h6 class="card-title">{{ $t('Invitation_code.value') }} : {{ row.user.username }}</h6>

                </div>
                <div class="col-md-6">

                            <h6 class="card-title">{{ $t('Task_income.value') }} : {{ parseFloat(row.taskearn).toFixed(2) }}</h6>
                            <h6 class="card-title">{{ $t('Balance.value') }} : {{ parseFloat(row.user.balance).toFixed(2) }}</h6>


                </div>
            </div>
        </section>





        <section id="btn-area">

            <div class="row">
                <div class="col-6 p-0"> <router-link :to="{name:'Recharge'}">{{ $t('Recharge.value') }}</router-link></div>
                <div class="col-6 p-0"> <router-link :to="{name:'Withdraw'}">{{ $t('Withdraw.value') }}</router-link></div>
            </div>


        </section>
        <section id="accounDetlist">


                <ul>
                    <li><router-link :to="{name:'license'}" class="accountList odd listCompanny " ><img src="https://petpat.lv/wp-content/uploads/2018/12/license-icon-27934542-2.png">
                            <p>{{ $t('Company_Profile.value') }}</p></router-link>
                    </li>

                    <li><router-link :to="{name:'information'}" class="accountList even listInformaion"><img :src="$asseturl+'frontend/img/inf.png'">
                            <p>{{ $t('Information.value') }}</p>
                        </router-link></li>
                    <li><router-link :to="{name:'orders'}" class="accountList odd listorder"><img :src="$asseturl+'frontend/img/order.png'">
                            <p>{{ $t('Order_Record.value') }}</p>
                        </router-link></li>
                    <li><router-link :to="{name:'rechargeHistory'}" class="accountList even listReHis"><img :src="$asseturl+'frontend/img/rech.png'">
                            <p>{{ $t('Recharge_History.value') }}</p>
                        </router-link></li>
                    <li><router-link :to="{name:'WithdrawHistory'}" class="accountList odd listWithHis"><img :src="$asseturl+'frontend/img/with.png'">
                            <p>{{ $t('Withdraw_History.value') }}</p>
                        </router-link></li>


                    <li><router-link :to="{name:'invite'}" class="accountList even listInvite"><img :src="$asseturl+'frontend/img/5811623.png'">
                            <p>{{ $t('Invite.value') }}</p>
                        </router-link></li>

                    <li v-if="settings.telegroup"><a :href="settings.telegroup" class="accountList odd listTeleGroup" target="_blank"><img :src="$asseturl+'frontend/img/Telegram.png'">
                            <p>{{ $t('Official_Telegram_Group.value') }}</p>
                        </a></li>

                    <li v-if="settings.telesupport1"><a :href="settings.telesupport1" class="accountList even listCus1" target="_blank"><img :src="$asseturl+'frontend/img/aGroup.jpeg'">
                            <p>{{ $t('Customer_Service.value') }} 1</p></a>
                    </li>

                    <li v-if="settings.telesupport2"><a :href="settings.telesupport2" class="accountList odd listCus2" target="_blank"><img src="https://cdn5.vectorstock.com/i/1000x1000/01/69/businesswoman-character-avatar-icon-vector-12800169.jpg">
                            <p>{{ $t('Customer_Service.value') }} 2</p></a>
                    </li>

                    <li v-if="settings.telesupport3"><a :href="settings.telesupport3" class="accountList even listCus3" target="_blank"><img src="https://cdn5.vectorstock.com/i/1000x1000/01/69/businesswoman-character-avatar-icon-vector-12800169.jpg">
                            <p>{{ $t('Customer_Service.value') }} 2</p></a>
                    </li>
                </ul>
                <router-link :to="{name:'logout'}" class="logout">{{ $t('Log_out.value') }}</router-link>
        </section>

 -->








    </div>
</template>
<script>
export default {
    data(){
        return {
            settings:{},
              row: {
                plans:{},
                deposit:{},
                depositamount:0,
                user:{},
                withdraw:{},
                withdrawamount:0,
                refercount:0,
            },
        }
    },
    methods: {
          async getData() {



            var resN = await this.callApi('get',`/api/admin/setting`,[])
              this.settings = resN.data

             var id = localStorage.getItem('userid');
            var res = await this.callApi('get', `/api/admin/user/${id}`, []);
            this.row = res.data;

        },



    },
    mounted() {
            this.getData();

    },
}
</script>

<style>

section.accontDetails {
    background: #008dff;
    color: white;
    padding: 32px 16px;
    margin-top: -40px;
}

a.accountList {
    color: white !important;
}

a.accountList.odd {
    background: #003cff !important;
}

a.accountList.even {
    background: #af5016 !important;
}



/*
a.accountList.listCompanny {
    background: #af1616 !important;
}

a.accountList.listInformaion {}

a.accountList.listInformaion {
    background: #af165b !important;
}

a.accountList.listorder {
    background: #9516af !important;
}

a.accountList.listReHis {
    background: #5616af !important;
}

a.accountList.listWithHis {
    background: #2716af !important;
}

a.accountList.listInvite {
    background: #1653af !important;
}

a.accountList.listCus1 {
    background: #16af56 !important;
}

a.accountList.listTeleGroup {
    background: #1692af !important;
}

a.accountList.listCus2 {
    background: #82af16 !important;
}




a.accountList.listCompanny:hover {
    background: #d51919 !important;
}



a.accountList.listInformaion:hover {
    background: #d7186e !important;
}

a.accountList.listorder:hover {
    background: #bd1cde !important;
}

a.accountList.listReHis:hover {
    background: #6719d4 !important;
}

a.accountList.listWithHis:hover {
    background: #2f17e2 !important;
}

a.accountList.listInvite:hover {
    background: #1c69dc !important;
}

a.accountList.listCus1:hover {
    background: #19d969 !important;
}

a.accountList.listTeleGroup:hover {
    background: #1ab3d5 !important;
}

a.accountList.listCus2:hover {
    background: #97cc1a !important;
} */




</style>

<template>
  <div>

    <div class="layout-content">
                    <div class="van-nav-bar van-nav-bar--fixed">
                        <div class="van-nav-bar__content"><div class="van-nav-bar__title van-ellipsis">হোম পৃষ্ঠা</div></div>
                    </div>
                    <div data-v-e9381f42="" style="padding: 83px 20px;">
                        <div data-v-e9381f42="" class="home-info-cell-group van-cell-group">
                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <i data-v-e9381f42="" class="van-icon van-icon-gem van-cell__left-icon"><!----></i>
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42=""><i class="fa-solid fa-gem"></i>আরও বার পান</span></div>
                                <i data-v-e9381f42="" class="van-icon van-icon-arrow van-cell__right-icon"><!----></i>
                            </div>



                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42="">মোট পরিমাণ</span></div>
                                <div data-v-e9381f42="" class="van-cell__value"><span data-v-e9381f42="">{{ user.user.balance }}</span></div>
                            </div>





                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42="">দৈনিক কাজের চাপ</span></div>
                                <div data-v-e9381f42="" class="van-cell__value"><span data-v-e9381f42="">{{ user.plans.totalorder-user.user.task }}/{{ user.plans.totalorder }}</span></div>
                            </div>
                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42="">আজকের কমিশন</span></div>
                                <div data-v-e9381f42="" class="van-cell__value"><span data-v-e9381f42="">{{ user.taskearn }}</span></div>
                            </div>
                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42="">টিম কমিশন</span></div>
                                <div data-v-e9381f42="" class="van-cell__value"><span data-v-e9381f42="">{{ teamdetails.refer_task_bonus }}</span></div>
                            </div>
                            <div data-v-e9381f42="" role="button" tabindex="0" class="home-info-cell-group-cell van-cell van-cell--clickable">
                                <div data-v-e9381f42="" class="van-cell__title"><span data-v-e9381f42="">গতকালের কমিশন</span></div>
                                <div data-v-e9381f42="" class="van-cell__value"><span data-v-e9381f42="">{{ user.YesterdayEarn }}</span></div>
                            </div>
                            <!---->
                        </div>
                        <router-link :to="{name:'Usertask'}" data-v-e9381f42="" class="home-start-work-btn van-button van-button--primary van-button--normal van-button--block">
                            <div data-v-e9381f42="" class="van-button__content" style="    padding: 13px 6px;"><span data-v-e9381f42="" class="van-button__text" >কাজটি শুরু করুন</span></div>
                        </router-link>
                    </div>
                </div>

































    <div class="notice" v-if="notice">

<p> <h3>Welcome</h3>
    <br>
    <p v-html="settings.notice"></p>
</p>

        <button class="closebtn" @click="closeNotice">Close</button>
    </div>




  </div>
</template>

<script>


export default {
    created() {
        if(localStorage.getItem('notice')==1){
             this.notice = false
        }
        this.getplans()
        // console.log(this.slider.length)
        var indexx = 1;
        this.slideimage = this.slider[0]
        setInterval(() => {
            if(indexx===this.slider.length)indexx = 0;
            // console.log(indexx);
            this.slideimage = this.slider[indexx]
            indexx++
        }, 5000);

    },
    data(){
        return {
            row:{},
            notice:true,
            slideimage:'',
            settings:{},
            teamdetails:{},
            user:{
                user:{},
                plans:{}
            },
            slider:[
            this.$asseturl+'frontend/img/Daily-Task-Commisson-Chart.png',
            this.$asseturl+'frontend/img/Refar-Deposit-Bonus.png',
            this.$asseturl+'frontend/img/Refar-Task-income.png',
            this.$asseturl+'frontend/img/Self-Deposit.png'
            ]
        }
    },
    methods: {
        generator(){
        return '#'+(Math.random()*0xFFFFFF<<0).toString(16);
      },

        closeNotice(){
            this.notice = false

        localStorage.setItem('notice',1)

        },

       async getplans(){

        var resN = await this.callApi('get',`/api/admin/setting`,[])
              this.settings = resN.data


            var res = await this.callApi('get',`/api/admin/plan`,[])
            this.row = res.data


             var id = localStorage.getItem('userid');
            var results = await this.callApi('get', `/api/admin/user/${id}`, []);
            this.user = results.data;

            var teamdetailsres = await this.callApi('get',`/api/front/teamdetails?id=${id}`,[]);
            this.teamdetails = teamdetailsres.data;


        }
    },

}
</script>
<style>

section#topbar .title {
    display: flex !important;
    justify-content: space-between;
    padding: 0 18px;
}

#marquee {
  margin: 24px 0;
}

    .reImage {
        padding: 6px;
background: #e1e1e1;
box-shadow: 0px 0px 10px 0px #0000008c;
    }
    .notice {
    width: 340px;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    background: #f0f0f0;
    padding: 52px 11px;
    z-index: 99;
    border-radius: 10px;
    text-align: center;
}

.closebtn {
  position: absolute;
  bottom: 7px;
  background: transparent;
  border: 2px solid #7683aa;
  border-radius: 6px;
  right: 23px;
}
.plansdesign{
    display: flex;
justify-content: space-between;
}

/* .planPack {
  width: 30%;
} */

</style>

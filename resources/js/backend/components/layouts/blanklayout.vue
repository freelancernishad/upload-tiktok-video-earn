<template>
    <div>
        <h1 v-if="Frontloader">loading....</h1>

    <!-- <section id="call">
      <img :src="$asseturl+'frontend/img/phone.png'" alt="phone" />
    </section> -->
 

        <slot></slot>







        <div data-v-fbb34206="" class="van-tabbar van-tabbar--fixed">

        <router-link :to="{name:'Authuser'}" class="van-tabbar-item__text"><span data-v-fbb34206=""><i class="fa-light fa-memo-pad"></i>রেকর্ডিং</span></router-link>

        <router-link :to="{name:'Usertask'}" data-v-fbb34206="" class="van-tabbar-item van-tabbar-item--active">
           <div class="van-tabbar-item__icon">
              <img data-v-fbb34206="" src="data:image/png;base64,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" style="width: 50px; height: 50px; box-shadow: rgba(166, 174, 189, 0.6) 10px 10px 30px;"><!---->
           </div>
        </router-link>
        <router-link :to="{name:'Useraccount'}" class="van-tabbar-item__text"><span data-v-fbb34206="">আমি</span></router-link>

     </div>















<!--


<section style="padding: 40px;"></section>
        <section id="menus">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'Authuser'}">
                                <img :src="$asseturl+'frontend/img/home.png?ver=1.0'" alt="Home">
                                <p>Home</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'UserTeam'}">
                                <img :src="$asseturl+'frontend/img/team.png?ver=1.0'" alt="Home">
                                <p>Team</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu" style="position: relative;">
                            <router-link :to="{name:'Usertask'}" style="position: absolute;bottom: -37px;left: 13%;background: white;padding: 6px;border-top-left-radius: 30px;border-top-right-radius: 30px;">
                                <img style="width: 46px;height: 42px;" :src="$asseturl+'frontend/img/Task.png?ver=1.0'" alt="Home">
                                <p>Earn</p>
                            </router-link>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <a :href="$asseturl+'JMY_EARN_MONEY_16135694.apk'">
                                <img :src="$asseturl+'frontend/img/android.png?ver=1.0'" alt="Home">
                                <p>App</p>
                            </a>
                        </div>
                    </div>
                    <div class="col-3 p-0" style="width: 20% !important;">
                        <div class="menu">
                            <router-link :to="{name:'Useraccount'}">
                                <img :src="$asseturl+'frontend/img/profile.png?ver=1.0'" alt="Home">
                                <p>Account</p>
                            </router-link>
                        </div>
                    </div>


                </div>
            </div>
        </section> -->

    </div>
</template>
<script>
  export default {
    created() {
                this.createlink('frontend/css/bootstrap.min.css');
        this.createlink('frontend/style.css');
        this.createlink('frontend/css/font-awesome.min.css');

        this.createscript('frontend/js/bootstrap.bundle.min.js');
        this.createscript('frontend/js/bootstrap.min.js');
    },
    data(){
        return {

        }},
    watch: {
        '$route': {
            handler(newValue, oldValue) {
                window.scrollTo(0,0);
            },
            deep: true
        }
    },
    mounted() {


    },
    methods: {
        createlink(url=''){
            let recaptchaScript = document.createElement('link')
            recaptchaScript.setAttribute('href', this.$asseturl+url)
            recaptchaScript.setAttribute('rel', 'stylesheet')
            document.head.appendChild(recaptchaScript)
        },
        createscript(url=''){
            let recaptchaScript = document.createElement('script')
            recaptchaScript.setAttribute('src', this.$asseturl+url)
            document.body.appendChild(recaptchaScript)
        }
    }
  }
</script>
<style>
.col-6.amount_item span {
  border: 2px solid #e8ba31;
  display: block;
  text-align: center;
  margin: 6px 0px;
  padding: 4px 3px;
  cursor: pointer;
}
</style>

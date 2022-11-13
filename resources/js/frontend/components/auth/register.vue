<template>
    <section id="bigbg">

        <div data-v-7e320bfa="" class="layout-content">


        <div data-v-cd1085ee="" data-v-7e320bfa="" style="padding: 50px 0px; text-align: center;">
           <span data-v-cd1085ee="" class="web-title-name-span">নতুন রেজিস্ট্রেশন করুন</span>
           <div data-v-cd1085ee="" class="cell-group van-cell-group">
              <form data-v-cd1085ee="" @submit.prevent='register' class="van-form">



                 <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                    <label class="inputlabel" for="">

                       <i class="fas fa-users"></i>
                       <span>+880</span>
                    </label>

                    <input type="tel" inputmode="numeric" v-model="form.mobile" placeholder="আপনার ফোন নম্বর পূরণ করুন" class="van-field__control">
                 </div>



                 <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                    <label class="inputlabel" for="">
                 <i class="fas fa-lock"></i>
                   <span>পাসওয়ার্ড</span>
                 </label>
                 <input type="password" v-model="form.password" placeholder="অনুগ্রহ করে আপনার পাসওয়ার্ড পূরণ করুন" class="van-field__control">
                 </div>


                 <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                    <label class="inputlabel" for="">
                 <i class="fas fa-lock"></i>
                   <span>পাসওয়ার্ড যাচাই করুন</span>
                 </label>
                 <input type="password" v-model="form.password_confirmation" placeholder="অনুগ্রহ করে আপনার পাসওয়ার্ড পূরণ করুন" class="van-field__control">
                 </div>


                 <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                    <label class="inputlabel" for="">
                 <i class="fas fa-share-square"></i>
                   <span>আমন্ত্রণ কোড</span>
                 </label>
                 <input type="text" v-model="form.ref_by" placeholder="অনুগ্রহ করে আমন্ত্রণ কোড লিখুন" class="van-field__control">
                 </div>


                 <div data-v-cd1085ee="" style="margin: 16px;">
                    <button data-v-cd1085ee="" type="submit" class="login-btn van-button van-button--info van-button--normal van-button--block van-button--round">
                       <div data-v-cd1085ee="" class="van-button__content"><span data-v-cd1085ee="" class="van-button__text">রেজিস্ট্রেশন</span></div>
                    </button>
                 </div>
                 <span data-v-cd1085ee="">ইতিমধ্যে একটি অ্যাকাউন্ট আছে?</span><router-link :to="{name:'/login'}" data-v-cd1085ee="" style="color: rgb(181, 138, 72);">লগইন?</router-link>
              </form>
           </div>

        </div>
     </div>












    </section>
</template>
<script>

export default {
    created() {
        this.genaratedCaptcha = Math.random().toString(36).substring(2, 6 + 2);
        // if (User.loggedIn()) {
        //     this.$router.push({ name: 'home' })
        // }
        // localStorage.setItem('dmdevice',1)
        // console.log(this.$route.query.ref);
        if (this.$route.query.ref) {
            this.form.ref_by = this.$route.query.ref;
            this.refer = 1
        } else {
            this.form.ref_by = '1234'
            this.refercheck();
        }
        this.form.country = '+880'
        this.countryList();
        this.addcountry()
    },
    data() {
        return {


            btndis: true,
            captcha: '',
            genaratedCaptcha: '',
            mobileCode: null,
            form: {
                country: null,
                name: 'New Customer',
                username: null,
                mobile: null,
                password: null,
                password_confirmation: null,
                withdrawpass: '123456',
                ref_by: null,
            },
            usernameMatch: 1,
            refer: 0,
            errors: {},
            codes: {},
            showPassword: true,
            CshowPassword: true,
            WshowPassword: true,
        }
    },
    methods: {
        // setLang(){
        //     localStorage.setItem('language',this.$i18n.locale)
        // },


        async usernamecheck() {
            if (this.form.username == '') {
                this.usernameMatch = 0;
            } else {
                var res = await this.callApi('get', `/api/count/username/check?username=${this.form.username}`, []);
                if (res.data == 0) {
                    this.usernameMatch = 2
                } else {
                    this.usernameMatch = 1
                }
            }
        },
        async countryList() {
            var res = await this.callApi('get', `${this.$asseturl}CountryCodes.json`, []);
            // console.log(res)
            this.codes = res.data
        },
        async addcountry() {
            // this.form.mobile = this.form.country
            this.mobileCode = this.form.country
        },
        async refercheck() {
            if (this.form.ref_by == '') {
                this.refer = 0;
            } else {
                var res = await this.callApi('get', `/api/count/username/check?username=${this.form.ref_by}`, []);
                if (res.data == 0) {
                    this.refer = 2
                } else {
                    this.refer = 1
                }
            }
        },
        register() {
            // if(localStorage.getItem('dmdevice')){
            //     Notification.customError(`This device has already have an account!`);
            // }else{
            // if (this.genaratedCaptcha === this.captcha) {
                // if(this.usernameMatch!=2){
                //     Notification.customError('please Enter deferent username');
                // }else{
                if (this.refer != 1) {
                    Notification.customError('Opps,Refer code is Invalid');
                } else {
                    if (this.form.password === this.form.password_confirmation) {
                        axios.post('api/auth/register', this.form)
                            .then(res => {
                                if (res.data == 422) {
                                    Notification.customError('This Phone Number Already Exist');
                                } else if (res.data == 444) {
                                    Notification.customError(`This device has already have an account!`);
                                    localStorage.setItem('dmdevice', 1)
                                } else {
                                    // console.log(res)
                                    if (res.status == 201) {
                                        Notification.customSuccess('Registration Success');
                                        localStorage.setItem('dmdevice', 1)
                                        this.$router.push({ name: '/login' })
                                    } else {
                                        Notification.customError('Something want wrong. Please Try again or contact with admin');
                                    }
                                    // User.responseAfterLogin(res)
                                }
                                // console.log(res.data)
                                // User.responseAfterLogin(res)
                            })
                            .catch(error => this.errors = error.response.data.errors)
                    } else {
                        Notification.customError('Password and Confirm password does not match');
                    }
                }
            //     // }
            // } else {
            //     Notification.customError('Captcha does not match!');
            // }
            // }
        }
    }
}
</script>
<style lang="css" scoped>

.languagechange {
    width: 100px;
    float: right;
}
button.button {
    padding: 7px 5px;
}
</style>

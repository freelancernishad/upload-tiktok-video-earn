<template>


    <section id="bigbg">


        <div data-v-7e320bfa="" class="layout-content">
            <div data-v-7e320bfa="" class="van-nav-bar van-nav-bar--fixed">
                <div class="van-nav-bar__content">
                    <div class="van-nav-bar__title van-ellipsis">লগইন</div>
                </div>
            </div>

            <div data-v-413e4dc8="" data-v-7e320bfa="" style="padding: 50px 0px; text-align: center;">
                <span data-v-413e4dc8="" class="web-title-name-span">স্বাগতম</span><span data-v-413e4dc8=""
                    class="web-title-info-span">অনুগ্রহ করে আপনার লগইন তথ্য পূরণ করুন</span>
                <div data-v-413e4dc8="" class="web-logo-img van-image" style="width: 100px; height: 100px;">
                    <img :src="$asseturl+'frontend/img/20221107_174650.png'"
                        class="van-image__img" />
                </div>
                <div data-v-413e4dc8="" class="cell-group van-cell-group">
                    <form data-v-413e4dc8="" @submit.prevent='login' class="van-form">

                        <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                            <label class="inputlabel" for="">

                                <i class="fas fa-users"></i>
                                <span>+880</span>
                            </label>

                            <input type="tel" inputmode="numeric" v-model="form.mobile"
                                placeholder="আপনার ফোন নম্বর পূরণ করুন" class="van-field__control">
                        </div>



                        <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                            <label class="inputlabel" for="">
                                <i class="fas fa-lock"></i>
                                <span>পাসওয়ার্ড</span>
                            </label>
                            <input type="password" v-model="form.password"
                                placeholder="অনুগ্রহ করে আপনার পাসওয়ার্ড পূরণ করুন" class="van-field__control">
                        </div>


                        <div data-v-413e4dc8="" style="margin: 16px;">
                            <button data-v-413e4dc8="" type="submit"
                                class="login-btn van-button van-button--info van-button--normal van-button--block van-button--round">

                                <span data-v-413e4dc8="" class="van-button__text" v-if="loadLogin">{{ $t('Loader.value')
                                }}</span>
                                <span data-v-413e4dc8="" class="van-button__text" v-else>{{ $t('Login.value') }}</span>


                            </button>
                        </div>
                        <span data-v-413e4dc8="">এখনো একাউন্ট নেই?</span>
                        <router-link :to="{name:'register'}" data-v-413e4dc8="" style="color: rgb(181, 138, 72);">নাম নথিভুক্ত করুন</router-link>
                    </form>
                </div>
            </div>
        </div>








    </section>




</template>

<script>
export default {

    created() {

        this.addcountry();
        this.countryList();
    },

    data() {
        return {



            emailLogin: "",
            passwordLogin: "",
            emailReg: "",
            passwordReg: "",
            confirmReg: "",
            emptyFields: false,
            form: {
                mobile: '',
                password: ''
            },
            country: '+880',
            mobileCode: '',
            errors: {},
            codes: {},
            loadLogin: false
        }
    },
    methods: {


        async countryList() {
            var res = await this.callApi('get', `${this.$asseturl}CountryCodes.json`, []);
            // console.log(res)
            this.codes = res.data
        },
        async addcountry() {
            this.mobileCode = this.country
        },

        login() {
            this.loadLogin = true

            if (this.form.mobile == "" || this.form.password == "") {
                this.emptyFields = true;
            } else {

                axios.post('/login', this.form)
                    .then(res => {


                        if (res.data == 0) {
                            Notification.customError('Please Enter Valid Phone Number and Password');
                            this.loadLogin = false
                        } else if (res.data == 422) {
                            Notification.customError('Your Account Has Been Banded!');
                            this.loadLogin = false
                        } else if (res.data == 444) {
                            Notification.customError('You Cant Login Multiple account same device!');
                            this.loadLogin = false
                            localStorage.setItem('dmdevice', 1)
                        } else {




                            localStorage.setItem('dmdevice', 1)
                            User.responseAfterLogin(res)
                            if (res.data.role == 'admin') {
                                window.location.href = '/dashboard/adddmin'
                            } else {
                                window.location.href = '/dashboard/user'
                            }

                            Notification.customSuccess('Signed in successfully Complete');

                            // this.$router.push({name: 'home'})
                            // window.location.href = '/dashboard'

                        }
                    })
                    .catch(error => this.errors = error.response.data.errors)



            }





        },


        blur(id) {
            const child = document.getElementById(id);
            if (this.form[id] == '') {
                child.parentNode.classList.remove("blursuccess");
                child.parentNode.classList.add("blurerror");
            } else {
                child.parentNode.classList.remove("blurerror");
                child.parentNode.classList.add("blursuccess");
            }

        },




    }
}
</script>

<style lang="css" scoped>
.languagechange {
    width: 100px;
    float: right;
}

section.vh-100 {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
}

.blurerror input {
    border: 1px solid red !important;
}

.blurerror label {
    color: red !important;
}

.blursuccess input {
    border: 1px solid green !important;
}

.blursuccess label {
    color: green !important;
}

.divider:after,
.divider:before {
    content: "";
    flex: 1;
    height: 1px;
    background: #eee;
}

*,
*:focus {
    outline: none
}

/* .form{
  width: 500px;
  margin: 0 auto;
  margin-top: 150px;
  font-family: sans-serif;
  background: #fff
} */
.form-item {
    position: relative;
    margin-bottom: 15px
}

.form-item input {
    display: block;
    width: 100%;
    height: 40px;
    background: transparent;
    border: solid 1px #ccc;
    transition: all .3s ease;
    padding: 0 15px
}

.form-item input:focus {
    border-color: blue
}

.form-item label {
    position: absolute;
    cursor: text;
    z-index: 2;
    top: 13px;
    left: 10px;
    font-size: 12px;
    font-weight: bold;
    background: #fff;
    padding: 0 10px;
    color: #999;
    transition: all .3s ease
}

.form-item input:focus+label,
.form-item input:valid+label {
    font-size: 11px;
    top: -5px
}

.form-item input:focus+label {
    color: blue
}
</style>


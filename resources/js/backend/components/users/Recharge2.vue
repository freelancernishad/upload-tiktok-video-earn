<template>
    <div>

        <div class="layout-content">
                    <div class="van-nav-bar van-nav-bar--fixed mb-5">
                        <div class="van-nav-bar__content"><div class="van-nav-bar__title van-ellipsis">রিচার্জ</div></div>
                    </div>


                    <div v-if="step == 1" style="    margin-top: 70px;margin-bottom: 100px;">

                    <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                            <label class="inputlabel" for="">
                            <span>রিচার্জের মাধ্যম  </span>
                            </label>
                            <select class="van-field__control" v-model="payMethods" @change="getMethods" required>
                                <option value="">Select</option>
                                <option v-for="pay in row" :key="'pay' + pay.id" :value="pay.id">{{ pay.name }}
                                </option>
                            </select>
                        </div>



                    <div data-v-cd1085ee="" class="field-box-input van-cell van-field">
                            <label class="inputlabel" for="">
                            <span>রিচার্জের পরিমাণ </span>
                            </label>
                            <input type="text" v-model="amount"
                                placeholder="অনুগ্রহ করে রিচার্জের পরিমাণ পূরণ করুন" class="van-field__control">
                    </div>


                    <div class="row">
                            <div class="col-6 amount_item" @click="amount = 700/rates"><span>{{ 700/rates }}</span> </div>
                            <div class="col-6 amount_item" @click="amount = 1000/rates"><span>{{ 1000/rates }}</span></div>
                            <div class="col-6 amount_item" @click="amount = 2000/rates"><span>{{ 2000/rates }}</span></div>
                            <div class="col-6 amount_item" @click="amount = 5000/rates"><span>{{ 5000/rates }}</span></div>
                            <div class="col-6 amount_item" @click="amount = 10000/rates"><span>{{ 10000/rates }}</span></div>
                            <div class="col-6 amount_item" @click="amount = 20000/rates"><span>{{ 20000/rates }}</span></div>
                            <div class="col-6 amount_item" @click="amount = 25000/rates"><span>{{ 25000/rates }}</span></div>
                        </div>
                        <button class="money-btn" style="padding: 8px 14px;font-size: 23px;color: white;" @click="nextFun(2)">Next</button>
                        <p style="color: red;text-align: center;font-size: 17px;">{{ settings.recharagetext }}</p>
                        </div>

                        <form @submit.stop.prevent="onSubmit" v-else-if="step == 2" style="margin-top: 70px;margin-bottom: 100px;">
                        <h4 class="d-block money-btn text-white p-1 my-3">Payment Info</h4>
                        <p  style="color: red;font-size: 17px;">বিঃদ্রঃ অবশই সেন্ড মানি করবেন এবং রেফারেন্স এ আপনার Username দিবেন ।</p>
                        <div class="patment_info">
                            <ul class="list-unstyled">
                                <li class="li"><span>{{ form.method }} Account</span><span>
                                        <input type="hidden" v-model="copyMessage">
                                        <!-- <input type="button" value="copy" class="copy" @click="copyref"> -->
                                        {{ copyMessage }} <i @click="copyref" class="far fa-copy"></i>
                                        <br>
                                        <img style="width:200px; height: 200px !important;"
                                            v-if="form.method=='USDT (TRC-20)'"
                                            :src="$asseturl+'frontend/img/qrcode.jpeg'" alt="">
                                    </span></li>
                                <li class="li" v-if="form.method=='USDT'"><span>Amount</span><span>{{ amount }} USD = {{
                                amount*rates }} BDT</span></li>
                                <li class="li" v-else><span>Amount</span><span>{{ amount*rates }} BDT</span></li>
                            </ul>
                        </div>
                        <h4 class="d-block money-btn text-white p-1 my-3">Recharge Info</h4>
                        <div class="form-group" v-if="form.method=='USDT'">
                            <label for="">Screenshot</label>
                            <input class="form-control form-control-lg" id="formFileLg"
                                @change="FileSelected($event, 'screenshot')" type="file">
                            <img class="img-thumbnail" :src="form.screenshot" alt="">
                        </div>
                        <div class="form-group">
                            <label for="">Sender Number</label>
                            <input type="tel" class="form-control" v-model="form.sender" required>
                        </div>
                        <div class="form-group mb-3">
                            <label for="">Transition Id</label>
                            <input type="text" class="form-control" v-model="form.trx" required>
                        </div>
                        <button class="btn btn-secondary" @click="nextFun(1)">Previous</button>
                        <button class="money-btn" style="padding: 8px 14px;font-size: 23px;color: white;" type="button" disabled v-if="con">Wait...</button>
                        <button class="money-btn" style="padding: 8px 14px;font-size: 23px;color: white;" type="submit" v-else>Submit</button>
                    </form>

        </div>





        <div class="copyPopup" v-if="popup">
            <span> Number copied success</span>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            popup: false,
            form: {
                method: '',
                amount: '',
                sender: '',
                screenshot: '',
                trx: '',
            },
            row: {},
            settings: {},
            payMethods: '',
            amount: 0,
            step: 1,
            copyMessage: '',
            rates: '',
            con: false,
        }
    },
    methods: {
        async getMethods() {
            var res = await this.callApi('get', `/api/admin/withdraw/gateway/${this.payMethods}`, []);
            // console.log(res);
            this.copyMessage = res.data.number;
            this.form.method = res.data.name;
            this.rates = res.data.rate;
        },
        copyref() {
            navigator.clipboard.writeText(this.copyMessage);
            this.popup = true
            setTimeout(() => {
                this.popup = false
            }, 1000);
        },
        FileSelected($event, parent_index) {
            let file = $event.target.files[0];
            if (file.size > 5048576) {
                Notification.image_validation();
            } else {
                let reader = new FileReader;
                reader.onload = event => {
                    this.form[parent_index] = event.target.result
                    // console.log(event.target.result);
                };
                reader.readAsDataURL(file)
            }
            //   console.log($event.target.result);
        },
        async setting() {
            var resN = await this.callApi('get', `/api/admin/setting`, [])
            this.settings = resN.data
        },
        async getData() {
            var res = await this.callApi('get', `/api/admin/withdraw/gateway`, []);
            this.row = res.data;
        },
        nextFun(step) {
            if (step == 2) {
                if (!this.form.method) {
                    Notification.customError('Method is required');
                } else {
                    if (!this.amount) {
                        Notification.customError('Amount is required');
                    } else {
                        if (this.settings.min_deposit > Number(this.amount)) {
                            Notification.customError(`Minimum deposit amount ${this.settings.min_deposit}`);
                        } else {
                            this.step = step;
                        }
                    }
                }
            } else {
                this.step = step;
            }
        },
        async onSubmit() {
            this.con = true
            if (this.settings.min_deposit > Number(this.amount)) {
                Notification.customError(`Minimum deposit amount ${this.settings.min_deposit}`);
            } else {
                // this.step = step;
                this.form.amount = this.amount * this.rates;
                var id = localStorage.getItem('userid');
                this.form['user_id'] = id;
                var res = await this.callApi('post', `/api/admin/deposit`, this.form);
                Notification.customSuccess(`Recharge Successfuly Complete`);
                this.$router.push({ name: 'rechargeHistory' });
            }
        }
    },
    mounted() {
        this.getData();
        this.setting();
    },
}
</script>
<style>
.mainitem {
    display: flex !important;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
}
</style>

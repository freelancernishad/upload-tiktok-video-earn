<template>
    <div>


        <div class="layout-content" style="margin-bottom: 100px;">
            <div class="van-nav-bar van-nav-bar--fixed mb-5">
                <div class="van-nav-bar__content"><div class="van-nav-bar__title van-ellipsis">প্রত্যাহার ইতিহাস </div></div>
            </div>





        <section id="listmenus" style="margin-top: 60px;">



            <div role="feed" class="van-list row" aria-busy="true">
                <div class="recordDiv col-md-6" v-for="rech in row" :key="'rech'+rech.id">


                    <div class="card text-white"  style="background: #464d55;font-size: 16px;margin: 17px;margin-bottom: 20px">
                        <div class="card-body">
                            <p>{{ dateformatglobal(rech.created_at)[6] }}</p>
                            <p>ট্রান্সিশন নম্বর : {{ rech.trx }}</p>
                            <p>পরিমাণ : {{ rech.amount }}</p>
                            <p>অবস্থা :  {{ rech.status }}</p>
                        </div>
                    </div>



                </div>
            </div>


        </section>

    </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
              row: {},

        }
    },
    methods: {

        generator() {
            return '#' + (Math.random() * 0xFFFFFF << 0).toString(16);
        },

          async getData() {
   var id = localStorage.getItem('userid');
            var res = await this.callApi('get', `/api/admin/withdrawal?id=${id}`, []);
            this.row = res.data;

        },

    copyURL() {
      var Url = this.$refs.mylink;
      Url.innerHTML = window.location.href;
      console.log(Url.innerHTML)
      Url.select();
      document.execCommand("copy");
    }

    },
    mounted() {
            this.getData();

    },
}
</script>

<template>
    <div :style="'background:#EAEFF5'">
       <div class="px-5 py-3" :style="'background:#FFF'" v-if="shrimp">
            <b-row>
                <b-col>
                    <h6 class="text-primary">{{shrimp.region.province_name}}</h6>
                    <h6 class="text-secondary">{{shrimp.region.name}}</h6>
                </b-col>
                <b-col class="text-right">
                    <nuxt-link :to="`/`" class="btn btn-sm btn-success">Kembali</nuxt-link>
                </b-col>
            </b-row>
       </div>
       <b-container fluid class="py-3">
           <b-row class="text-left">
               <b-col cols="7">
                   <b-card>
                        <h6>Detail Harga Udang</h6>
                        <hr>
                        <b-row>
                            <b-col cols="7">
                                <p>
                                    {{$moment(shrimp.date).format('DD MMMM YYYY')}}
                                </p>
                                <b>Udang Vannamei (Penaeus Vannamei)</b>
                            </b-col>
                            <b-col>
                                <p>
                                    Supplier :
                                </p>
                                <b>{{shrimp.creator.name}}</b>
                            </b-col>
                            <b-col>
                                <p>
                                    Kontak :
                                </p>
                                <p>
                                    {{ shrimp.creator.phone }}
                                </p>
                                <a href="#" @click="copySomething(shrimp.creator.phone)">Salin Kontak</a>
                            </b-col>
                        </b-row>
                        <table class="table mt-3">
                            <tbody>
                                <tr>
                                    <td><b>Size 20</b></td>
                                    <td>{{ rupiah(shrimp.size_20) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 30</b></td>
                                    <td>{{ rupiah(shrimp.size_30) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 40</b></td>
                                    <td>{{ rupiah(shrimp.size_40) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 50</b></td>
                                    <td>{{ rupiah(shrimp.size_50) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 60</b></td>
                                    <td>{{ rupiah(shrimp.size_60) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 70</b></td>
                                    <td>{{ rupiah(shrimp.size_70) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 80</b></td>
                                    <td>{{ rupiah(shrimp.size_80) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 90</b></td>
                                    <td>{{ rupiah(shrimp.size_90) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 100</b></td>
                                    <td>{{ rupiah(shrimp.size_100) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 110</b></td>
                                    <td>{{ rupiah(shrimp.size_110) }}</td>
                                </tr>
                                <tr>
                                    <td><b>Size 120</b></td>
                                    <td>{{ rupiah(shrimp.size_120) }}</td>
                                </tr>
                            </tbody>
                        </table>
                        <b-row>
                            <b-col>
                                <b>Catatan</b>
                                <p>{{shrimp.creator.company}} ({{ shrimp.creator.company_address }})</p>
                                <br>
                                <p>{{shrimp.remark}}</p>
                            </b-col>
                            <b-col>
                                <b-card class="w-50 text-center float-right">
                                    <b-button variant="primary" class="btn-sm rounded-circle" :style="'background:#4267B2'">
                                        <b-img src="/sosmed/facebook.svg" class="p-1"></b-img>
                                        </b-button>
                                        <b-button variant="success" class="btn-sm rounded-circle" :style="'background:#25d366'">
                                        <b-img src="/sosmed/whatsapp.svg" class="p-1"></b-img>
                                        </b-button>
                                        <b-button variant="info" class="btn-sm rounded-circle" :style="'background:#55acee'">
                                        <b-img src="/sosmed/twitter.svg" class="p-1"></b-img>
                                        </b-button>
                                </b-card>
                            </b-col>
                        </b-row>
                   </b-card>
               </b-col>
               <b-col>
                    <b-card>
                        <h6>Riwayat Harga Di Daerah {{shrimp.region.province_name}}</h6>
                        <hr>
                        <div>
                            <b-tabs content-class="mt-3" pills  align="center">
                                <b-tab title="Riwayat" active>
                                    <b-card-text>
                                        <b-alert show variant="warning">
                                            <h6 class="alert-link">Informasi</h6>
                                            <p>
                                                Perhitungan trend berdasarkan jumlah data supplier di satu area untuk mendapatkan nilai rata-rata di setiap area.
                                            </p>
                                        </b-alert>
                                    </b-card-text>
                                </b-tab>
                                <b-tab title="Prediksi">
                                    <b-card-text>
                                        <b>Prediksi seminggu kedepan</b>
                                        <table class="table mt-3 text-center">
                                            <thead class="text-primary">
                                              <tr>
                                                <th scope="col">Size</th>
                                                <th scope="col">Harga Min</th>
                                                <th scope="col">Harga Max</th>
                                              </tr>
                                            </thead>
                                            <tbody>
                                                <tr>
                                                    <td><b>Size 40</b></td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.min_size_40)}}</td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.max_size_40)}}</td>
                                                </tr>
                                                <tr>
                                                    <td><b>Size 70</b></td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.min_size_70)}}</td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.max_size_70)}}</td>
                                                </tr>
                                                <tr>
                                                    <td><b>Size 100</b></td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.min_size_100)}}</td>
                                                    <td>{{rupiah(shrimp.shrimp_price_per_week_region_id.max_size_100)}}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                        <b-alert show variant="warning">
                                            <h6 class="alert-link">Informasi</h6>
                                            <p>
                                                Hasil diatas merupakan sebuah prediksi dari berdasarkan data yang telah tercatat di Jala. Prediksi harga udang ini <b>hanya sebagai referensi</b> , bukan sebuah rujukan yang harus diikuti. <b>Jala tidak bertanggung jawab</b> atas kerugian yang ditimbulkan karena menggunakan prediksi harga udang
                                            </p>
                                        </b-alert>
                                    </b-card-text>
                                </b-tab>
                            </b-tabs>
                        </div>
                        <div class="mt-3">
                            <a href="#">Lihat detail trend</a>
                        </div>
                        <div>
                            <b-row>
                                <b-col class="text-center">
                                    <p class="text-secondary">Tertarik untuk berbagi info harga udang?</p>
                                    <b-button variant="primary">TAMBAH HARGA DI DAERAH SAYA</b-button>
                                </b-col>
                            </b-row>
                        </div>
                    </b-card>
               </b-col>
           </b-row>
       </b-container>
       <b-container fluid class="py-3">
           <Banner1></Banner1>
            <div class="my-3">
                <b-row>
                    <b-col>
                        <b-card>
                            <h6>Harga Lainnya</h6>
                            <hr>
                            <div>
                                <b-card-group deck>
                                  <b-card v-for="related in relateds" :key="related.id" bg-variant="light" header-text-variant="white" class="w-25" :style="'max-width:25%'">
                                    <b-row>
                                        <b-col class="text-left">
                                            <h5 class="text-primary">{{related.region.province_name}}</h5>
                                            <p class="text-primary">{{related.region.name}}</p>
                                            <p class="text-secondary">Size 100</p>
                                            <h5>{{rupiah(related.size_100)}}</h5>
                                        </b-col>
                                        <b-col class="text-right">
                                            <p class="text-secondary">{{$moment(related.date).format('DD MMMM YYYY')}}</p>
                                            <p class="text-secondary">Supplier :</p>
                                            <p> {{related.creator.name}}</p>
                                            <p class="mt-1">{{related.creator.phone}}</p>
                                        </b-col>
                                    </b-row>
                                    <b-row>
                                        <b-col class="text-center">
                                            <nuxt-link :to="`/detail/${related.id}`" class="btn btn-primary">Lihat Detail</nuxt-link>
                                        </b-col>
                                        <b-col class="text-center">
                                            <b-button variant="outline-primary" @click="copySomething(related.creator.phone)">Salin Kontak</b-button>
                                        </b-col>
                                    </b-row>
                                    <b-row class="mt-4">
                                        <b-col class="text-center">
                                            <p>
                                                Bagikan : 
                                                <b-button variant="primary" class="btn-sm rounded-circle" :style="'background:#4267B2'">
                                                    <b-img src="/sosmed/facebook.svg" class="p-1"></b-img>
                                                </b-button>
                                                <b-button variant="success" class="btn-sm rounded-circle" :style="'background:#25d366'">
                                                <b-img src="/sosmed/whatsapp.svg" class="p-1"></b-img>
                                                </b-button>
                                                <b-button variant="info" class="btn-sm rounded-circle" :style="'background:#55acee'">
                                                <b-img src="/sosmed/twitter.svg" class="p-1"></b-img>
                                                </b-button>
                                            </p>
                                        </b-col>
                                    </b-row>
                                  </b-card>
                                </b-card-group>
                              </div>
                        </b-card>
                    </b-col>
                </b-row>
            </div>
            <Banner2></Banner2>
       </b-container>
    </div>
</template>

<script>
export default{
  async asyncData({$axios, params}) {
    let shrimps = await $axios.$get('http://localhost:3000/data/shrimp_prices.json');
    let shrimpData = shrimps.data;
    let foundID = shrimpData.findIndex(function(post, index) {
        if(post.id == params.id)
            return true;
    });
    
    let dataProvince = [];
    if(foundID){
        shrimpData.findIndex(function(post, index) {
            if(post.province_id == shrimpData[foundID].province_id && post.id != params.id && dataProvince.length < 4){
                dataProvince.push(post)
            }
                
        });
    }

    return {
        shrimp:shrimpData[foundID],
        relateds:dataProvince ? dataProvince : null
    }
  },
  methods: {
    rupiah: function (number) {
      return new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR"
      }).format(number);
    },
    async copySomething(text) {
        try {
            await this.$copyText(text);
        } catch (e) {
            console.error(e);
        }
    },
  }
}
</script>
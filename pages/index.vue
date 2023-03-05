<template>
  <div :style="'background:#EAEFF5'" class="pt-3">
    <Banner1/>
    <b-container fluid class="my-4">
      <b-row class="text-left">
        <b-col cols="7">
          <b-card>
            <h6>Persebaran Harga Udang Size 100</h6>
            <div id="map-wrap" style="height: 40vh">
              <client-only>
                <l-map :zoom=7 :center="[-7.150975,110.140259]">
                  <l-tile-layer url="http://{s}.tile.osm.org/{z}/{x}/{y}.png"></l-tile-layer>
                  <l-marker v-for="shrimp in shrimps.data" :key="shrimp.id" 
                  :lat-lng="[shrimp.region.latitude,shrimp.region.longitude]" @click="markerClick(shrimp.id)">
                    <l-tooltip>{{rupiah(shrimp.size_100)}}</l-tooltip>
                  </l-marker>
                </l-map>
              </client-only>
             </div>
          </b-card>
        </b-col>
        <b-col>
          <h6>Trend harga di berbagai daerah</h6>
          <b-row>
            <b-col>
              <b-card class="my-2">
                  <h6>LAMPUNG</h6>
                  <h6>Rp. 56.000 <b-badge class="ml-1" pill variant="success">+ Rp.1000</b-badge></h6>
                  <p class="text-muted">19 Feb - 26 Feb</p>
              </b-card>
              <b-card class="my-2">
                <h6>JAWA TIMUR</h6>
                <h6>Rp. 54.000 <b-badge class="ml-1" pill variant="danger">- Rp.1000</b-badge></h6>
                <p class="text-muted">26 Feb - 05 Mar</p>
            </b-card>
            </b-col>
            <b-col>
              <b-card class="my-2">
                <h6>JAWA TENGAH</h6>
                <h6>Rp. 54.000 <b-badge class="ml-1" pill variant="success">+ Rp.1000</b-badge></h6>
                <p class="text-muted">26 Feb - 05 Mar</p>
            </b-card>
            <b-card class="my-2">
              <h6>BANTEN</h6>
              <h6>Rp. 52.000 <b-badge class="ml-1" pill variant="success">+ Rp 0</b-badge></h6>
              <p class="text-muted">19 Feb - 26 Feb</p>
          </b-card>
            </b-col>
          </b-row>
        </b-col>
      </b-row>
    </b-container>
    <Banner2/>
    <b-container fluid class="my-4">
      <b-card>
        <b-row>
          <b-col>
            <h6>Persebaran Harga Udang Size 100</h6>
          </b-col>
          <b-col class="text-right">
            <b-button variant="primary" class="btn-sm">Tambah Harga</b-button>
          </b-col>
        </b-row>
        <table class="table mt-3">
          <thead>
            <tr>
              <th scope="col">Tanggal</th>
              <th scope="col">Lokasi</th>
              <th scope="col">Supplier</th>
              <th scope="col">Harga Size 100</th>
              <th></th>
              <th></th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="shrimp in shrimps.data" :key="shrimp.id">
              <td>{{$moment(shrimp.date).format('DD MMMM YYYY')}}</td>
              <td>{{shrimp.region.name}}</td>
              <td>{{shrimp.creator.name}}</td>
              <td>{{rupiah(shrimp.size_100)}}</td>
              <td>
                <nuxt-link :to="`/detail/${shrimp.id}`" class="btn btn-primary">Lihat Detail</nuxt-link>
              </td>
              <td>
                <b-button variant="primary" class="btn-sm rounded-circle" :style="'background:#4267B2'">
                  <b-img src="/sosmed/facebook.svg" class="p-1"></b-img>
                </b-button>
                <b-button variant="success" class="btn-sm rounded-circle" :style="'background:#25d366'">
                  <b-img src="/sosmed/whatsapp.svg" class="p-1"></b-img>
                </b-button>
                <b-button variant="info" class="btn-sm rounded-circle" :style="'background:#55acee'">
                  <b-img src="/sosmed/twitter.svg" class="p-1"></b-img>
                </b-button>
              </td>
            </tr>
          </tbody>
        </table>
      </b-card>
    </b-container>
  </div>
</template>

<script>
export default{
  async asyncData({$axios}) {
      const shrimps = await $axios.$get('http://localhost:3000/data/shrimp_prices.json');
      return {shrimps}
  },
  methods: {
    rupiah: function (number) {
      return new Intl.NumberFormat("id-ID", {
        style: "currency",
        currency: "IDR"
      }).format(number);
    },
    markerClick: function(id){
      this.$nuxt.$options.router.push('detail/'+id);
    }
  }
}
</script>

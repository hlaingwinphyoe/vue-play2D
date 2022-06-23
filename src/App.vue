<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h4 class="text-center my-3">Manage 2D Players</h4>
        <div class="border p-3 mb-3 rounded">
          <div class="row justify-content-between align-items-center">
            <div class="col-lg-4">
              <form action="" @submit.prevent="openVoucher">
                <div class="row g-2">
                  <div class="col">
                    <input type="text" v-model="playerName" class="form-control" placeholder="ထိုးသားအမည်" required>
                  </div>
                  <div class="col">
                    <button class="btn btn-primary">ဘောင်ချာဖွင့်ရန်</button>
                  </div>
                </div>
              </form>
            </div>
            <div class="col-lg-4">
              Something Here
            </div>
          </div>
        </div>

        <div class="player-vouchers">
          <Voucher v-for="voucher in vouchers" :key="voucher.id" :voucher-detail="voucher" />
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import Voucher from "@/components/Voucher";
export default {
  components: {Voucher},

  data() {
    return {
      playerName: "",
      voucherStart : 1,
      vouchers : []
    }
  },
  computed: {
    currentTime() {
      let d = new Date();
      return d.getHours()+":"+d.getMinutes();
    }
  },
  methods: {
    openVoucher() {
      let newVoucher = {
        id : this.voucherStart,
        name : this.playerName,
        time : this.currentTime,
        digits : []
      }
      // this.vouchers.push(newVoucher);

      // spread operator နဲ့လည်း data ပေးလို့ရတယ်

      this.vouchers = [...this.vouchers,newVoucher];
      this.voucherStart++;
      // console.log(this.vouchers)
      this.playerName = ''
    }
  },
}
</script>

<style>
  @import "bootstrap/dist/css/bootstrap.min.css";
  @import "@fortawesome/fontawesome-free/css/all.min.css";

  .player-vouchers{
    columns: 4 300px;
  }

  .voucher-time{
    font-size: 11px;
    line-height: 24px;
  }


</style>
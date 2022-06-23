<template>
  <div class="voucher border rounded d-inline-block p-3 mb-3 w-100">
    <div class="">
      <div class="d-flex justify-content-between align-content-center">
        <p class="fw-bold text-capitalize mb-0">{{ voucherDetail.name }}</p>
        <p class="voucher-time mb-0">
          <i class="fa-regular fa-clock me-1"></i>{{ voucherDetail.time }}
        </p>
      </div>
      <hr class="my-2">
      <form action="" @submit.prevent="saveDigit">
        <div class="row g-1">
          <div class="col-5">
            <input type="number" class="form-control" v-model="inputHtoeKwet" placeholder="ထိုးကွက်" max="99" required>
          </div>
          <div class="col-5">
            <input type="number" class="form-control" v-model="inputHtoeKyay" placeholder="ထိုးကြေး" min="50" required>
          </div>
          <div class="col-2">
            <button class="btn btn-primary w-100"><i class="fa-solid fa-save"></i></button>
          </div>
        </div>
      </form>
      <table class="table mt-2">
        <thead>
          <tr>
            <th>#</th>
            <th>ထိုးကွက်</th>
            <th>ထိုးကြေး</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td v-if="voucherDetail.digits.length === 0" class="text-center" colspan="3">ထိုးကွက်မရှိပါ။</td>
          </tr>
          <tr v-for="digit in voucherDetail.digits" :key="digit.id">
            <td>{{ digit.id }}</td>
            <td>{{ digit.htoeKwet }}</td>
            <td>{{ digit.htoeKyay }}</td>
          </tr>
        </tbody>
        <tfoot v-if="voucherDetail.digits.length > 0">
          <tr>
            <td colspan="2">စုစုပေါင်းထိုးကြေး</td>
            <td>{{ totalHtoeKyay }}</td>
          </tr>
        </tfoot>
      </table>

    </div>
  </div>
</template>

<script>
export default {
  name: "Voucher",
  props: {
    voucherDetail: Object
  },
  data() {
    return {
      inputHtoeKwet: null,
      inputHtoeKyay: null,
      digitStart : 1
    }
  },
  methods: {
    saveDigit() {
      let newDigit = {
        id : this.digitStart,
        htoeKwet : this.inputHtoeKwet,
        htoeKyay : this.inputHtoeKyay,
      }

      this.voucherDetail.digits = [...this.voucherDetail.digits,newDigit];
      this.inputHtoeKyay = this.inputHtoeKwet = null;
      this.digitStart++;

    }
  },
  computed: {
    totalHtoeKyay() {
      return this.voucherDetail.digits.reduce((pv,cv)=>pv+cv.htoeKyay,0)
    }
  },
}
</script>

<style scoped>

</style>
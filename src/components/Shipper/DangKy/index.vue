<template>
     <div class="container py-5"
       style="background: url('/images/bg-shipper-register.jpg') no-repeat center center / cover; min-height: 100vh;">
    <div class="text-center mb-4">
      <h3 style="color: #FF9900; font-weight: bold;">Đăng ký trở thành người giao hàng</h3>
    </div>

    <div class="bg-white rounded shadow p-4 mx-auto" style="max-width: 900px;">
      <form class="row g-3">
        <!-- Họ và tên + Email -->
        <div class="col-md-6">
          <label>👤 Họ Và Tên:</label>
          <input v-model="them_shipper.ho_va_ten" type="text" class="form-control" />
        </div>
        <div class="col-md-6">
          <label>✉️ E-mail:</label>
          <input v-model="them_shipper.email" type="email" class="form-control" />
        </div>

        <!-- SĐT + CCCD -->
        <div class="col-md-6">
          <label>📱 Số điện thoại:</label>
          <input v-model="them_shipper.so_dien_thoai" type="text" class="form-control" />
        </div>
        <div class="col-md-6">
          <label>🪪 CCCD:</label>
          <input v-model="them_shipper.cccd" type="text" class="form-control" />
        </div>

        <!-- Mật khẩu + nhập lại -->
        <div class="col-md-6">
          <label>🔐 Mật khẩu:</label>
          <input v-model="them_shipper.password" type="password" class="form-control" />
        </div>
        <div class="col-md-6">
          <label>🔁 Nhập lại mật khẩu:</label>
          <input v-model="them_shipper.re_password" type="password" class="form-control" />
        </div>
        <!-- Nút đăng ký -->
        <div class="col-12">
          <button type="button"
                  v-on:click="dangKyShipper()"
                  class="btn w-100"
                  style="background-color: #FF9900; color: white; font-weight: bold;">
            Đăng ký
          </button>
        </div>

        <!-- Quay lại -->
        <div class="col-12 text-center">
          <p class="mt-3 mb-0">
            Bạn đã có tài khoản?
            <router-link to="/shipper/dang-nhap">
              <span style="color: green; font-weight: bold;">Đăng nhập</span>
            </router-link>
          </p>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from 'axios';

export default {
    data() {
        return {
            list_quan_huyen: [],
            list_tinh_thanh: [],
            them_shipper: {}
        }
    },

    mounted() {
        this.loadDataTinhThanh();
        this.loadDataQuanHuyen();
    },

    methods: {
        loadDataTinhThanh() {
            axios
                .get('http://127.0.0.1:8000/api/admin/tinh-thanh/data-open')
                .then((res) => {
                    this.list_tinh_thanh = res.data.data;
                })
        },
        loadDataQuanHuyen() {
            axios
                .get('http://127.0.0.1:8000/api/admin/quan-huyen/data-open')
                .then((res) => {
                    this.list_quan_huyen = res.data.data;
                })
        },
        dangKyShipper() {
            axios
                .post("http://127.0.0.1:8000/api/shipper/dang-ky", this.them_shipper)
                .then((res) => {
                    if (res.data.status) {
                        this.$toast.success(res.data.message);
                        this.them_shipper = {}
                    }
                })
                .catch((res) => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                })
        }
    },
};
</script>
<style></style>

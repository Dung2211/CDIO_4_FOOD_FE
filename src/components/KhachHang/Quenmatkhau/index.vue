<template>
  <div class="container">
    <div class="row justify-content-center align-items-center min-vh-100">
      <div class="col-md-6 col-lg-4">
        <div class="card border-0 shadow">
          <div class="card-body p-4">
            <div class="text-center mb-4">
              <h3 class="fw-bold">Quên mật khẩu</h3>
              <p class="text-muted small">Chào mừng đến với K-food</p>
            </div>
            <div>
              <input
                v-model="payload.email"
                type="email"
                class="form-control mb-3"
                placeholder="Nhập email tài khoản của bạn"
              />

              <input
                v-model="payload.password"
                type="password"
                class="form-control mb-3"
                placeholder="Nhập mật khẩu mới"
              />

              <div class="d-flex justify-content-center mt-4">
                <button
                  v-on:click="guiYeuCau()"
                  type="button"
                  class="btn btn-danger w-100"
                >
                  Đổi Mật Khẩu
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      payload: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    guiYeuCau() {
      // Gửi cục payload (gồm email và mật khẩu mới) lên Backend
      axios
        .post(
          "http://127.0.0.1:8000/api/khach-hang/quen-mat-khau",
          this.payload,
        )
        .then((res) => {
          if (res.data.status) {
            this.$toast.success(res.data.message);
            // Chuyển hướng người dùng về trang đăng nhập sau khi đổi thành công
            this.$router.push("/khach-hang/dang-nhap");
          } else {
            this.$toast.error(res.data.message); // Báo lỗi nếu sai email
          }
        })
        .catch((res) => {
          this.$toast.error("Có lỗi xảy ra, vui lòng kiểm tra lại!");
        });
    },
  },
};
</script>

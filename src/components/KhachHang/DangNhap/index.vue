<template>
  <div class="d-flex min-vh-100">
    <!-- Cột trái: Hình ảnh -->
    <div class="col-md-6 d-none d-md-flex justify-content-center align-items-center" style="background-color: #FF8C00;">
      <img src="/src/assets/images/login/burger.png" alt="Burger" class="img-fluid" style="max-height: 90%">
    </div>

    <!-- Cột phải: Form đăng nhập -->
    <div class="col-md-6 d-flex justify-content-center align-items-center" style="background-color: #FFE4C4;">
      <div class="card border-0 shadow w-100 mx-4" style="max-width: 400px;">
        <div class="card-body p-4">
          <div class="text-center mb-4">
            <h3 class="fw-bold">Đăng Nhập</h3>
            <p class="text-muted small">Chào mừng đến với K-FOODS</p>
          </div>
          <form @submit.prevent="Login">
            <div class="mb-3">
              <label for="email" class="form-label">Email</label>
              <input v-model="user.email" type="email" class="form-control" id="email" placeholder="Nhập email">
            </div>
            <div class="mb-4">
              <label for="password" class="form-label">Mật khẩu</label>
              <input v-model="user.password" type="password" class="form-control" id="password" placeholder="Nhập mật khẩu">
            </div>
            <div class="mb-4">
              <label for="password" class="form-label">Recaptcha</label>
              <div class="g-recaptcha" data-sitekey="6LftzRorAAAAAFqAWCXc2BGMp7XM-RgWuryT0v7d"></div>
            </div>
            <button type="submit" class="btn btn-primary w-100 mb-3">Đăng Nhập</button>
            <div class="text-center">
              <router-link to="/khach-hang/quen-mat-khau" class="text-decoration-none small me-2">
                Quên mật khẩu?
              </router-link>
              <span class="text-muted">|</span>
              <router-link to="/khach-hang/dang-ky" class="text-decoration-none small ms-2">
                Đăng ký tài khoản
              </router-link>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from 'axios';
export default {
    data() {
        return {
            user: {
                email: '',
                password: ''
            }
        }
    },
    mounted() {
        const recaptchaScript = document.createElement('script')
        recaptchaScript.setAttribute('src', 'https://www.google.com/recaptcha/api.js')
        recaptchaScript.onerror = () => {
            this.$toast.error("Không thể tải Recaptcha. Vui lòng thử lại sau.")
        }
        document.head.appendChild(recaptchaScript)
    },
    methods: {
        Login() {
            var code = grecaptcha.getResponse();
            if (code.length === 0) {
                this.$toast.error("Vui lòng xác minh Recaptcha.");
                return;
            }
            this.user.code = code;
            axios
                .post("http://127.0.0.1:8000/api/khach-hang/dang-nhap", this.user)
                .then((res) => {
                    if (res.data.status) {
                        this.$toast.success(res.data.message);
                        localStorage.setItem('khach_hang_login', res.data.token);
                        this.$router.push('/khach-hang/profile');
                    } else {
                        this.$toast.error(res.data.message);
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
}
</script>

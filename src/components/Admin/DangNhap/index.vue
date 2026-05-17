<template>
  <div
    style="
      min-height: 100vh;
      background: linear-gradient(to bottom, #062242, #0a0a0a);
      padding: 40px 20px;
    "
  >
    <div
      class="container d-flex flex-column justify-content-center align-items-center h-100"
    >
      <!-- Phần giới thiệu bên trái -->
      <div class="text-white mb-4 text-start w-100" style="max-width: 600px">
        <h2 style="color: #4cc9f0; font-weight: bold">Đăng nhập</h2>
        <p style="font-size: 1.1rem">dành cho quản trị viên hệ thống</p>
        <hr style="border-top: 2px dashed #4cc9f0; width: 150px" />
      </div>

      <!-- Form đăng nhập -->
      <div
        class="bg-white rounded shadow p-4 w-100 position-relative"
        style="max-width: 600px"
      >
        <!-- K-FOODS ở giữa đầu form, to và nổi bật -->
        <div class="text-center mb-4">
          <span style="font-size: 28px; font-weight: bold; color: #ff6600"
            >K-FOODS</span
          >
        </div>

        <div class="mb-3">
          <input
            v-model="user.email"
            @keyup.enter="Login()"
            type="email"
            class="form-control text-center"
            placeholder="E-mail"
            style="background-color: #e6f4ff"
          />
        </div>
        <div class="mb-3">
          <input
            v-model="user.password"
            @keyup.enter="Login()"
            type="password"
            class="form-control text-center"
            placeholder="Mật khẩu"
            style="background-color: #e6f4ff"
          />
        </div>
        <div class="mb-3 d-flex align-items-center">
          <div
            class="g-recaptcha"
            data-sitekey="6Le7bK0sAAAAALXPIKkI_N8PmbHlN6fdlDklJsbN"
          ></div>
        </div>
        <div class="d-grid">
          <button
            v-on:click="Login()"
            class="btn"
            style="background-color: #133b5c; color: white"
          >
            Đăng nhập
          </button>
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
      user: {
        email: "",
        password: "",
      },
    };
  },
  mounted() {
    const recaptchaScript = document.createElement("script");
    recaptchaScript.setAttribute(
      "src",
      "https://www.google.com/recaptcha/api.js",
    );
    recaptchaScript.onerror = () => {
      this.$toast.error("Không thể tải Recaptcha. Vui lòng thử lại sau.");
    };
    document.head.appendChild(recaptchaScript);
  },
  methods: {
    Login() {
      axios
        .post("http://127.0.0.1:8000/api/admin/dang-nhap", this.user)
        .then((res) => {
          if (res.data.status) {
            localStorage.setItem("nhan_vien_login", res.data.token);
            this.$toast.success(res.data.message);
            this.$router.push("/admin/quan-an");
          } else {
            this.$toast.error(res.data.message);
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
    },
  },
};
</script>

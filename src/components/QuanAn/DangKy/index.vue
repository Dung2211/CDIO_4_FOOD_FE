<template>
   <div class="container py-5" style="background-color: #f8f8f8; min-height: 100vh;">
    <div class="text-center mb-4">
      <h3 style="color: #ff6600; font-weight: bold;">Đăng ký trở thành nhà bán hàng</h3>
    </div>

    <div class="bg-white rounded shadow p-4 mx-auto" style="max-width: 900px;">
      <form class="row g-3">
        <!-- Cột trái -->
        <div class="col-md-6">
          <label><i class="fa-regular fa-user me-1"></i> Tên quán ăn:</label>
          <input v-model="quan_an_create.ten_quan_an" type="text" class="form-control mb-3" placeholder="Nhập tên quán ăn">

          <label><i class="fa-regular fa-envelope me-1"></i> E-mail:</label>
          <input v-model="quan_an_create.email" type="email" class="form-control mb-3" placeholder="Nhập email">

          <label><i class="fa-solid fa-phone me-1"></i> Số điện thoại:</label>
          <input v-model="quan_an_create.so_dien_thoai" type="text" class="form-control mb-3" placeholder="Nhập số điện thoại">

          <label><i class="fa-solid fa-location-dot me-1"></i> Địa chỉ:</label>
          <input v-model="quan_an_create.dia_chi" type="text" class="form-control mb-3" placeholder="Nhập địa chỉ">

          <label>Quận huyện:</label>
          <select v-model="quan_an_create.id_quan_huyen" class="form-control mb-3">
            <option v-for="item in quan_huyen" :key="item.id" :value="item.id">{{ item.ten_quan_huyen }}</option>
          </select>
        </div>

        <!-- Cột phải -->
        <div class="col-md-6">
          <label><i class="fa-solid fa-lock me-1"></i> Mật khẩu:</label>
          <input v-model="quan_an_create.password" type="password" class="form-control mb-3" placeholder="Nhập mật khẩu">

          <label><i class="fa-solid fa-lock me-1"></i> Nhập lại mật khẩu:</label>
          <input v-model="quan_an_create.re_password" type="password" class="form-control mb-3" placeholder="Nhập lại mật khẩu">

          <label><i class="fa-solid fa-id-card me-1"></i> Mã số thuế:</label>
          <input v-model="quan_an_create.ma_so_thue" type="text" class="form-control mb-3" placeholder="Nhập mã số thuế">

          <label><i class="fa-regular fa-clock me-1"></i> Giờ mở cửa:</label>
          <input v-model="quan_an_create.gio_mo_cua" type="time" class="form-control mb-3">

          <label><i class="fa-regular fa-clock me-1"></i> Giờ đóng cửa:</label>
          <input v-model="quan_an_create.gio_dong_cua" type="time" class="form-control mb-3">
        </div>

        <!-- Nút Đăng ký -->
        <div class="col-12 text-center mt-2">
          <button type="button" @click="dangKyQuanAn" class="btn" style="background-color: #ff6600; color: white; padding: 10px 40px; font-weight: bold;">
            Đăng ký
          </button>
          <p class="mt-3">Bạn đã có tài khoản?
            <router-link to="/quan-an/dang-nhap">
              <span style="color: limegreen; cursor: pointer;">Đăng nhập</span>
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
            quan_an_create: {
                'email': "",
                'password': "",
                're_password': "",
                'ma_so_thue': "",
                'ten_quan_an': "",
                'so_dien_thoai': "",
                'gio_mo_cua': "",
                'gio_dong_cua': "",
                'dia_chi': "",
                'id_quan_huyen': "",
                'is_active' : "",
                'tinh_trang' : ""
            },
            quan_huyen: [],
        }

    },
    mounted() {
        this.getQuanHuyen();
    },
    methods: {
        dangKyQuanAn() {
            axios
                .post('http://127.0.0.1:8000/api/quan-an/dang-ky', this.quan_an_create)
                .then(res => {
                    this.quan_an_create = {};
                    this.$toast.success(res.data.message);
                })
                .catch(res => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                });
        },
        getQuanHuyen() {
            axios.get('http://127.0.0.1:8000/api/admin/quan-huyen/data-open')
                .then(res => {
                    this.quan_huyen = res.data.data;
                })
                .catch(res => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                });
        },
    },
}
</script>
<style></style>
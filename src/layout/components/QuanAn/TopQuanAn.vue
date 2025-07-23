<template>
  <div class="topbar d-flex align-items-center px-3" style="background-color: black; height: 60px;">
    <!-- Logo -->
    <div class="d-flex align-items-center me-auto">
      <h4 class="mb-0 fw-bold">
        <span style="color: orange;">K</span><span class="text-white">-FOODS</span>
      </h4>
    </div>

    <!-- Icon setting + logout -->
    <div class="d-flex align-items-center gap-3 me-3 border-black">
      <button class="btn btn-sm text-white" @click="goToSettings" title="Cài đặt">
        <i class="fas fa-cog fa-lg"></i>
      </button>
      <button class="btn btn-sm text-white" @click="logout" title="Đăng xuất">
        <i class="fas fa-sign-out-alt fa-lg"></i>
      </button>
    </div>

    <!-- Avatar người dùng -->
    <div class="user-box dropdown border-black">
      <a class="d-flex align-items-center nav-link dropdown-toggle" href="#" data-bs-toggle="dropdown">
        <img :src="hinh_anh" class="user-img rounded-circle" alt="avatar" style="width: 40px; height: 40px;" />
        <div class="user-info ps-2 text-start">
          <p class="user-name mb-0 fw-bold text-white">{{ ten_quan_an }}</p>
          <p class="designattion mb-0 text-white">Quán ăn</p>
        </div>
      </a>
      <ul class="dropdown-menu dropdown-menu-end">
        <li>
          <router-link class="dropdown-item" to="/quan-an/profile">
            <i class="bx bx-user"></i><span>Profile</span>
          </router-link>
        </li>
        <li>
          <a @click.prevent="logout" class="dropdown-item" href="#">
            <i class="bx bx-log-out-circle"></i><span>Logout</span>
          </a>
        </li>
        <li>
          <a @click.prevent="logoutAll" class="dropdown-item" href="#">
            <i class="bx bx-log-out-circle"></i><span>Logout All</span>
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>


<script>
import axios from 'axios';

export default {
	data() {
		return {
			ten_quan_an: localStorage.getItem('ten_quan_an'),
			hinh_anh: localStorage.getItem('hinh_anh')
		}
	},
	methods: {
		logout() {
			axios.get('http://127.0.0.1:8000/api/quan-an/dang-xuat', {
				headers: {
					Authorization: "Bearer " + localStorage.getItem("quan_an_login"),
				},
			})
				.then(res => {
					if (res.data.status) {
						this.$toast.success(res.data.message);
						localStorage.removeItem('quan_an_login');
						this.$router.push('/quan-an/dang-nhap');
					} else {
						this.$toast.error(res.data.message);
					}
				})
				.catch(res => {
					const list = Object.values(res.res.data.errors);
					list.forEach((v, i) => {
						this.$toast.error(v[0]);
					});
				});
		},
		logoutAll() {
			axios.get('http://127.0.0.1:8000/api/quan-an/dang-xuat-tat-ca', {
				headers: {
					Authorization: "Bearer " + localStorage.getItem("quan_an_login"),
				},
			})
				.then(res => {
					if (res.data.status) {
						this.$toast.success(res.data.message);
						localStorage.removeItem('quan_an_login');
						this.$router.push('/quan-an/dang-nhap');
					} else {
						this.$toast.error(res.data.message);
					}
				})
				.catch(res => {
					const list = Object.values(res.res.data.errors);
					list.forEach((v, i) => {
						this.$toast.error(v[0]);
					});
				});
		},

		//bỏ cấu hình ở dưới menu lên 
		goToSettings() {
			this.$router.push('/quan-an/cau-hinh');
		}
	}
}
</script>
<style></style>
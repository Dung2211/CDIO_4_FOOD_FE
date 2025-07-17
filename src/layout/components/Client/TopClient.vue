<template>
	<div class="topbar bg-white py-2 shadow-sm border-bottom">
		<div class="container-fluid px-5">
			<div class="d-flex justify-content-between align-items-center flex-wrap">
				<!-- Logo -->
				<div class="d-flex align-items-center gap-2 mb-2 mb-md-0 ms-5">
					<i class="fa-solid fa-truck-fast fa-2x text-dark"></i>
					<h4 class="mb-0 fw-bold text-dark">K-FOODS</h4>
				</div>
				<!-- Menu giữa -->
				<div class="d-flex align-items-center gap-4 flex-wrap text-center mb-2 mb-md-0 fs-6">
					<router-link to="/khach-hang/trang-chu" class="menu-link"><b>Trang chủ</b></router-link>
					<router-link to="/khach-hang/mon-an" class="menu-link"><b>Món ăn</b></router-link>
					<router-link to="/khach-hang/list-quan-an" class="menu-link"><b>Quán ăn</b></router-link>
					<router-link to="/khach-hang/don-hang" class="menu-link"><b>Đơn hàng</b></router-link>
				</div>

				<!-- Menu phải -->
				<div class="d-flex align-items-center gap-3">
					<a href="#" class="text-black text-decoration-none">
						<i class="fa-regular fa-bell me-1"></i>Thông Báo
					</a>
					<a href="#" class="text-black text-decoration-none">
						<i class="fa-regular fa-circle-question me-1"></i>Hỗ Trợ
					</a>
					<a href="#" class="text-black text-decoration-none">
						<i class="fa-solid fa-globe me-1"></i>Tiếng Việt
					</a>
					<!-- Dropdown user -->
					<div class="dropdown">
						<a class="d-flex align-items-center nav-link dropdown-toggle dropdown-toggle-nocaret" href="#"
							role="button" data-bs-toggle="dropdown" aria-expanded="false">
							<img :src="avatar || 'https://cdn.iconscout.com/icon/free/png-256/free-avatar-icon-download-in-svg-png-gif-file-formats--user-boy-avatars-flat-icons-pack-people-456322.png'"
								class="user-img rounded-circle" alt="user avatar" style="width: 32px; height: 32px;">
							<div class="ps-2 d-none d-md-block">
								<p class="mb-0 fw-bold">{{ ho_ten }}</p>
								<small>Khách hàng</small>
							</div>
						</a>
						<ul class="dropdown-menu dropdown-menu-end">
							<li>
								<router-link to="/khach-hang/profile" class="dropdown-item">
									<i class="bx bx-user me-1"></i>Profile
								</router-link>
							</li>
							<li>
								<a @click="logout" class="dropdown-item" href="javascript:;"><i
										class="bx bx-log-out-circle me-1"></i>Logout</a>
							</li>
							<li>
								<a @click="logoutAll" class="dropdown-item" href="javascript:;"><i
										class="bx bx-log-out-circle me-1"></i>Logout All</a>
							</li>
						</ul>
					</div>
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
			ho_ten: localStorage.getItem('ho_ten_khach_hang'),
			avatar: localStorage.getItem('avatar'),
			noi_dung_tim: '',

		}
	},
	methods: {
		timKiem() {
			this.$router.push({
				name: 'name_tim_kiem',
				params: {
					thong_tin: this.noi_dung_tim,
				}
			});
		},
		logout() {
			axios.get('http://127.0.0.1:8000/api/khach-hang/dang-xuat', {
				headers: {
					Authorization: "Bearer " + localStorage.getItem("khach_hang_login"),
				},
			})
				.then(res => {
					if (res.data.status) {
						this.$toast.success(res.data.message);
						localStorage.removeItem('khach_hang_login');
						this.$router.push('/khach-hang/dang-nhap');
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
			axios.get('http://127.0.0.1:8000/api/khach-hang/dang-xuat-tat-ca', {
				headers: {
					Authorization: "Bearer " + localStorage.getItem("khach_hang_login"),
				},
			})
				.then(res => {
					if (res.data.status) {
						this.$toast.success(res.data.message);
						localStorage.removeItem('khach_hang_login');
						this.$router.push('/khach-hang/dang-nhap');
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
	}
}
</script>
<style>
.menu-link {
  display: flex;
  align-items: center;
  height: 100%;
  color: black;
  text-decoration: none;
  padding-bottom: 4px;
  border-bottom: 2px solid transparent;
  transition: all 0.2s ease;
}


/* Khi trỏ chuột vào */
.menu-link:hover {
  color: #f45b3e; /* Màu cam */
  border-bottom: 2px solid #f45b3e;
  font-weight: bold;
}
</style>
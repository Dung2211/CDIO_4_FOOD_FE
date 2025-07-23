<template>
	<div class="topbar d-flex align-items-center bg-white border-white px-3 py-2 text-black">
		<nav class="navbar navbar-expand w-100">
			<div class="container-fluid px-0 d-flex justify-content-center">
					<!-- Logo K-FOODS -->
					<div class="topbar-logo-header border-white">
						<div class="">
							<i class="fa-solid fa-truck-fast fa-3x"></i>
						</div>
						<div class="">
							<h2 class="logo-text text-black">K-FOODS</h2>
						</div>
					</div>
				<div class="d-flex justify-content-between align-items-center w-100" style="max-width: 1200px;">			
					<!-- Bên trái: Kênh người bán + MXH -->
					<div class="d-flex align-items-center gap-2">
						<router-link to="/quan-an/dang-nhap" class="text-decoration-none text-black">Kênh người
							bán</router-link>
						<span class="text-black">|</span>
						<router-link to="/quan-an/dang-ky" class="text-decoration-none text-black">Trở thành người
							bán</router-link>
						<span class="text-black">|</span>
					    <router-link to="/shipper/dang-nhap" class="text-decoration-none text-black">Shipper cùng chúng tôi
						</router-link>	
					</div>

					<!-- Bên phải: Thông báo / Hỗ trợ / Ngôn ngữ / Đăng nhập -->
					<div class="d-flex align-items-center gap-3 ms-3">
						<a href="#" class="text-black text-decoration-none">
							<i class="fa-regular fa-bell me-1"></i>Thông Báo
						</a>
						<a href="#" class="text-black text-decoration-none">
							<i class="fa-regular fa-circle-question me-1"></i>Hỗ Trợ
						</a>
						<a href="#" class="text-black text-decoration-none">
							<i class="fa-solid fa-globe me-1"></i>Tiếng Việt
						</a>
						<router-link to="/khach-hang/dang-nhap" class="text-black text-decoration-none">Đăng
							Nhập</router-link>
						<span class="text-black">|</span>
						<router-link to="/khach-hang/dang-ky" class="text-black text-decoration-none">Đăng
							Ký</router-link>
					</div>
				</div>
			</div>
		</nav>
	</div>
</template>
<script>
export default {
	data() {
		return {
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

	}
}
</script>
<style></style>
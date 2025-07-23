<!-- <template>
	<div class="nav-container primary-menu">
		<div class="mobile-topbar-header">
			<div>
				<img src="../../../assets/images/logo-icon.png" class="logo-icon" alt="logo icon">
			</div>
			<div>
				<h4 class="logo-text">Rukada</h4>
			</div>
			<div class="toggle-icon ms-auto"><i class='bx bx-arrow-to-left'></i>
			</div>
		</div>
		<nav class="navbar navbar-expand-xl w-100">
			<ul class="navbar-nav justify-content-start flex-grow-1 gap-1">
				<li class="nav-item">
					<router-link to="/quan-an/danh-muc">
						<a class="nav-link" href="/quan-an/danh-muc">
							<div class="parent-icon"><i class="fa-solid fa-list"></i>
							</div>
							<div class="menu-title">Danh Mục</div>
						</a>
					</router-link>
				</li>
				<li class="nav-item">
					<router-link to="/quan-an/mon-an">
						<a class="nav-link" href="/quan-an/mon-an">
							<div class="parent-icon"><i class="fa-solid fa-utensils"></i>
							</div>
							<div class="menu-title"> Món Ăn</div>
						</a>
					</router-link>
				</li>
				<li class="nav-item">
					<router-link to="/quan-an/voucher">
						<a class="nav-link" href="/quan-an/voucher">
							<div class="parent-icon"><i class="fa-solid fa-ticket"></i>
							</div>
							<div class="menu-title"> Voucher</div>
						</a>
					</router-link>
				</li>
					<li class="nav-item">
					<router-link to="/quan-an/don-hang">
						<a class="nav-link" href="/quan-an/don-hang">
							<div class="parent-icon"><i class="fa-solid fa-ticket"></i>
							</div>
							<div class="menu-title">Đơn Hàng</div>
						</a>
					</router-link>
				</li>
				<li class="nav-item dropdown">
					<a href="javascript:;" class="nav-link dropdown-toggle dropdown-toggle-nocaret"
						data-bs-toggle="dropdown">
						<div class="parent-icon"><i class="fa-solid fa-chart-simple"></i>
						</div>
						<div class="menu-title">Thống Kê</div>
					</a>
					<ul class="dropdown-menu">
						<router-link to="/quan-an/thong-ke-mon-an">
							<li>
								<a class="dropdown-item" href=""><i class="fa-solid fa-utensils"></i>Món Ăn</a>
							</li>
						</router-link>
						<router-link to="/quan-an/thong-ke-doanh-thu">
							<li>
								<a class="dropdown-item" href=""><i class="fa-solid fa-money-bill-trend-up"></i>Doanh
									Thu</a>
							</li>
						</router-link>
					</ul>
				</li>
				<li class="nav-item">
					<router-link to="/quan-an/cau-hinh">
						<a class="nav-link" href="/quan-an/cau-hinh">
							<div class="parent-icon"><i class="fa-solid fa-gears"></i>
							</div>
							<div class="menu-title"> Cấu Hình</div>
						</a>
					</router-link>
				</li>
			</ul>
		</nav>
	</div>
</template> -->

<template>
	<div class="nav-container primary-menu">
		<nav class="navbar navbar-expand-xl w-100">
			<ul class="navbar-nav w-100 d-flex text-center">
				<li class="nav-item flex-fill">
					<router-link to="/quan-an/danh-muc" class="nav-link"
						:class="{ active: $route.path === '/quan-an/danh-muc' }">
						<i class="fa-solid fa-list"></i>
						<span>Danh Mục</span>
					</router-link>
				</li>

				<li class="nav-item flex-fill">
					<router-link to="/quan-an/mon-an" class="nav-link"
						:class="{ active: $route.path === '/quan-an/mon-an' }">
						<i class="fa-solid fa-utensils"></i>
						<span>Món Ăn</span>
					</router-link>
				</li>
				<li class="nav-item flex-fill">
					<router-link to="/quan-an/voucher" class="nav-link"
						:class="{ active: $route.path === '/quan-an/voucher' }">
						<i class="fa-solid fa-ticket"></i>
						<span>Voucher</span>
					</router-link>
				</li>
				<li class="nav-item flex-fill">
					<router-link to="/quan-an/don-hang" class="nav-link"
						:class="{ active: $route.path === '/quan-an/don-hang' }">
						<i class="fa-solid fa-bag-shopping"></i>
						<span>Đơn Hàng</span>
					</router-link>
				</li>

				<li class="nav-item flex-fill dropdown">
					<a href="#" class="nav-link dropdown-toggle" data-bs-toggle="dropdown">
						<i class="fa-solid fa-chart-simple"></i>
						<span>Thống Kê</span>
					</a>
					<ul class="dropdown-menu w-100 text-start">
						<li>
							<router-link to="/quan-an/thong-ke-mon-an" class="dropdown-item"
								:class="{ active: $route.path === '/quan-an/thong-ke-mon-an' }">
								<i class="fa-solid fa-utensils"></i> Món Ăn
							</router-link>
						</li>
						<li>
							<router-link to="/quan-an/thong-ke-doanh-thu" class="dropdown-item"
								:class="{ active: $route.path === '/quan-an/thong-ke-doanh-thu' }">
								<i class="fa-solid fa-money-bill-trend-up"></i> Doanh Thu
							</router-link>
						</li>
					</ul>
				</li>
			</ul>
		</nav>
	</div>
</template>
<script>
export default {

}
</script>
<style scoped>
/* Link cơ bản */
.nav-link {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 8px;
	/* Khoảng cách giữa icon và text */
	padding: 10px 0;
	height: 100%;
	color: #333;
	text-decoration: none;
	transition: 0.3s;
	border-radius: 6px;
}

/* Hover và active */
.nav-link.active,
.nav-link:hover {
	background-color: #f59210;
	color: white !important;
}

/* Dropdown item trong menu con */
.dropdown-menu .dropdown-item.active,
.dropdown-menu .dropdown-item:hover {
	background-color: #f59210;
	color: white !important;
	border-radius: 4px;
}
</style>
<style></style>
<template>
  <div class="nav-container primary-menu">
    <nav class="navbar navbar-expand-xl w-100">
      <ul class="navbar-nav w-100 d-flex text-center">
        <li class="nav-item flex-fill">
          <router-link
            to="/quan-an/danh-muc"
            class="nav-link"
            :class="{ active: $route.path === '/quan-an/danh-muc' }"
          >
            <i class="fa-solid fa-list"></i>
            <span>Danh Mục</span>
          </router-link>
        </li>

        <li class="nav-item flex-fill">
          <router-link
            to="/quan-an/mon-an"
            class="nav-link"
            :class="{ active: $route.path === '/quan-an/mon-an' }"
          >
            <i class="fa-solid fa-utensils"></i>
            <span>Món Ăn</span>
          </router-link>
        </li>
        <li class="nav-item flex-fill">
          <router-link
            to="/quan-an/voucher"
            class="nav-link"
            :class="{ active: $route.path === '/quan-an/voucher' }"
          >
            <i class="fa-solid fa-ticket"></i>
            <span>Voucher</span>
          </router-link>
        </li>
        <li class="nav-item flex-fill">
          <router-link
            to="/quan-an/don-hang"
            class="nav-link"
            :class="{ active: $route.path === '/quan-an/don-hang' }"
          >
            <i class="fa-solid fa-bag-shopping"></i>
            <span>Đơn Hàng</span>
          </router-link>
        </li>

        <li class="nav-item flex-fill">
          <router-link
            to="/quan-an/danh-gia-khach-hang"
            class="nav-link"
            :class="{ active: $route.path === '/quan-an/danh-gia-khach-hang' }"
          >
            <i class="fa-solid fa-star"></i>
            <span>Đánh Giá</span>
          </router-link>
        </li>

        <li class="nav-item flex-fill dropdown">
          <a
            href="#"
            class="nav-link dropdown-toggle"
            data-bs-toggle="dropdown"
          >
            <i class="fa-solid fa-chart-simple"></i>
            <span>Thống Kê</span>
          </a>
          <ul class="dropdown-menu w-100 text-start">
            <li>
              <router-link
                to="/quan-an/thong-ke-mon-an"
                class="dropdown-item"
                :class="{ active: $route.path === '/quan-an/thong-ke-mon-an' }"
              >
                <i class="fa-solid fa-utensils"></i> Món Ăn
              </router-link>
            </li>
            <li>
              <router-link
                to="/quan-an/thong-ke-doanh-thu"
                class="dropdown-item"
                :class="{
                  active: $route.path === '/quan-an/thong-ke-doanh-thu',
                }"
              >
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
export default {};
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

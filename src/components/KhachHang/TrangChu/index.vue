<template>
    <div class="rounded-4 mb-4" style="background-color: #111111;">
        <div class="row">
            <div class="col-6 d-flex align-items-center">
                <div class="container ms-5">
                    <h2 class="text-white mb-4">Món ngon đến tay bạn chỉ trong vài phút!
                        <i class="fa-brands fa-square-web-awesome-stroke text-warning"></i>
                    </h2>
                    <span class="text-white">
                        FoodZone cam kết giao đồ ăn nóng hổi, tươi ngon, đúng giờ đến tận cửa nhà bạn.
                        Thỏa mãn cơn đói bất kỳ lúc nào, ở bất kỳ đâu!
                    </span>
                    <p class="mt-4"><button class="btn btn-outline-light rounded-4"><b>TRẢI NGHIỆM NGAY</b></button></p>
                </div>
            </div>
            <div class="col-6">
                <img src="https://png.pngtree.com/png-clipart/20241112/original/pngtree-food-delivery-by-scooters-free-download-png-image_16940462.png"
                    class="d-block w-100 rounded-4" alt="..." style="height: 500px; object-fit: cover;">
                <!-- ICON overlay góc trên phải -->
                <button class="position-absolute p-3 bg-light text-dark rounded-circle shadow border-0"
                    style="top: 15px; right: 90px; cursor: pointer;" @click="onCartIconClick">
                    <i class="fa-solid fa-cart-shopping fa-2x"></i>
                </button>
            </div>
        </div>
    </div>
    <!-- // Danh sách món ăn -->
    <div class="row mt-4">
        <div class="col-lg-12">
            <div class="card">
                <div class="card-header">
                    <div class="row">
                        <div class="col-lg-8">
                            <h5 class="mt-2" style="color: #FF7B00;">
                                Danh Mục Các Món Ăn <i class="fa-solid fa-bowl-food ms-1"></i>
                            </h5>
                        </div>
                        <div class="col-lg-2">
                            <div class="dropdown">
                                <button class="btn dropdown-toggle w-100" type="button" id="dropdownDanhMuc"
                                    data-bs-toggle="dropdown" aria-expanded="false"
                                    style="background-color: #FF7B00; color: white;">
                                    Danh Mục Món Ăn
                                </button>
                                <ul class="dropdown-menu" style="max-height: 250px; overflow-y: auto;"
                                    aria-labelledby="dropdownDanhMuc">
                                    <li v-for="(v, k) in phanLoai" :key="k">
                                        <a class="dropdown-item" href="#" @click.prevent="chonDanhMuc(v.id)">
                                            {{ v.ten_danh_muc }}
                                        </a>
                                    </li>
                                </ul>
                            </div>
                        </div>
                        <div class="col-lg-2">
                            <div class="btn-group w-100" role="group">
                                <button type="button" class="btn w-100"
                                    style="background-color: #FF7B00; color: white;">Chọn Mức Giá</button>
                                <div class="btn-group" role="group">
                                    <button id="btnGroupDrop1" type="button"
                                        class="btn dropdown-toggle dropdown-toggle-nocaret px-1"
                                        data-bs-toggle="dropdown" aria-expanded="false"
                                        style="background-color: #FF7B00; color: white;">
                                        <i class="bx bx-slider ms-1"></i>
                                    </button>
                                    <ul class="dropdown-menu dropdown-menu-start" aria-labelledby="btnGroupDrop1">
                                        <li><a class="dropdown-item" href="#"
                                                @click.prevent="filterByPrice('under50')">Dưới 50.000 VNĐ</a></li>
                                        <li><a class="dropdown-item" href="#"
                                                @click.prevent="filterByPrice('50to100')">50.000 - 100.000 VNĐ</a>
                                        </li>
                                        <li><a class="dropdown-item" href="#"
                                                @click.prevent="filterByPrice('100to200')">100.000 - 200.000
                                                VNĐ</a></li>
                                        <li><a class="dropdown-item" href="#"
                                                @click.prevent="filterByPrice('200to300')">200.000 - 300.000
                                                VNĐ</a></li>
                                        <li><a class="dropdown-item" href="#"
                                                @click.prevent="filterByPrice('above300')">Trên 300.000 VNĐ</a>
                                        </li>
                                    </ul>
                                </div>
                            </div>

                        </div>
                    </div>
                </div>
                <div class="card-body">
                    <div class="row product-grid">
                        <template v-for="(v, k) in monAnHienThi" :key="k">
                            <div class="col-lg-2 d-flex">
                                <div class="card flex-fill">
                                    <router-link :to="'/khach-hang/quan-an/' + v.id_quan_an">
                                        <img :src="v.hinh_anh" class="card-img-top"
                                            style="height: 200px; width: 100%;" />
                                        <div class="card-body">
                                            <h6 class="card-title cursor-pointer">
                                                {{ v.ten_mon_an }}
                                            </h6>
                                            <div class="clearfix">
                                                <p class="mb-0 float-start text-success">{{ v.ten_quan_an }}</p>
                                            </div>
                                            <p class="mt-2 text-danger">
                                                <del>{{ v.gia_ban }}đ</del>
                                                <strong class="ms-2">{{ v.gia_khuyen_mai }}đ</strong>
                                            </p>
                                            <div class="d-flex align-items-center mt-auto">
                                                <button class="btn ms-auto "
                                                    style="background-color: #FF9933; color: white;">Mua Ngay</button>
                                            </div>
                                        </div>
                                    </router-link>
                                </div>
                            </div>
                        </template>
                        <div class="col-lg-12 text-center">
                            <button v-on:click="xemThemMonAn()" type="button" class="btn btn-lg" style="width: 30%;"><i
                                    class="fa-regular fa-hand-point-up"></i>Xem
                                Thêm</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="row mt-4">
        <div class="card">
            <div class="card-header">
                <div class="row">
                    <div class="col-lg-6">
                        <h5 class="mt-2" style="color: #FF7B00;">
                            QUÁN ĂN ĐƯỢC YÊU THÍCH <i class="fa-solid fa-bowl-food ms-1"></i>
                        </h5>
                    </div>
                    <div class="col-lg-6">
                        <h6 class="mt-3 text-end" style="color: #FF7B00;">Xem tất cả <i
                                class="fa-solid fa-arrow-right"></i>
                        </h6>
                    </div>
                </div>
            </div>
            <div class="card-body">
                <div class="row product-grid">
                    <template v-for="(v, k) in quanAn" :key="k">
                        <div class="col-xl-4 col-lg-6 col-md-6 col-12 d-flex" v-if="k < 6">
                            <div class="card flex-fill">
                                <router-link :to="'/khach-hang/quan-an/' + v.id">
                                    <div class="card-body">
                                        <div class="row g-0">
                                            <div class="col-md-5">
                                                <img v-bind:src="v.hinh_anh" class="img-fluid rounded-start" alt="..."
                                                    style="width: 100%;height: 100%;">
                                            </div>
                                            <div class="col-md-7">
                                                <div class="card-body">
                                                    <h5 class="card-title"><b>
                                                            {{ v.ten_quan_an }}</b></h5>
                                                    <p>{{ v.dia_chi }}
                                                    </p>
                                                    <p><i class="fa-solid fa-tags me-1"></i> Tối thiểu {{
                                                        v.toi_thieu }} <i
                                                            class="fa-solid fa-circle-dollar-to-slot ms-3 me-1"></i>
                                                        Giá
                                                        {{ v.gia }}</p>
                                                    <div class="d-flex align-items-center mt-3">
                                                        <i class="fa-solid fa-tag text-danger me-2"></i> <span
                                                            class="text-primary"><b>Giảm hết {{ v.giam_gia
                                                            }}</b></span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </router-link>
                            </div>
                        </div>
                    </template>                  
                </div>
            </div>
        </div>
    </div>
    <div class="row mt-4">
        <div class="col-lg-12">
            <div class="card">
                <div class="card-header" style="background-color: #8B0000;">
                    <div class="row">
                        <div class="col-lg-6">
                            <h5 class="mt-3"><b class="text-uppercase text-white"> VOUCHER HẤP DẪN KHI ĐẶT MÓN</b></h5>
                        </div>
                        <div class="col-lg-6">
                            <h6 class="text-white mt-3 text-end">Xem tất cả <i class="fa-solid fa-arrow-right"
                                    style="color: #ffffff;"></i></h6>
                        </div>
                    </div>
                </div>
                <div class="card-body" style="background-color:#8B0000; border: none; box-shadow: none;">
                    <div class="row product-grid">
                        <template v-for="(v, k) in list_voucher" :key="k">
                            <div class="col-lg-3 d-flex">
                                <div class="card flex-fill border-0 shadow-none">
                                    <img :src="getImageUrl(v.hinh_anh)" class="card-img-top">
                                    <div class="card-body">
                                        <h6 class="card-title cursor-pointer">{{ v.ten_voucher }}</h6>
                                        <div class="clearfix">
                                            <p class="mb-0 float-start text-danger">{{ v.ten_quan_an }}</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </template>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- giao diện giỏ hàng tổng  -->
    <div v-if="showCart" class="position-fixed top-0 end-0 bg-white shadow-lg p-4"
        style="z-index: 1050; width: 400px; height: 100vh; overflow-y: auto;">
        <div class="d-flex justify-content-between align-items-center mb-3">
            <h5 class="mb-0">🛒 Giỏ Hàng Tổng</h5>
            <button class="btn btn-sm btn-danger" @click="toggleCart">Đóng</button>
        </div>
        <p>Hiển thị nội dung giỏ hàng tổng ở đây...</p>
        <!-- Ví dụ: danh sách món, tên quán, tổng tiền, nút đặt hàng,... -->
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data() {
        return {
            phanLoai: [],
            quanAn: [],
            monAnData: [],
            originalMonAnData: [],
            list_voucher: [],
            showCart: false,
            soluonghienthi: 12
        };
    },
    created() {
        this.loadData();
    },
    computed: {
        monAnHienThi() {
            return this.monAnData.slice(0, this.soluonghienthi);
        }
    },
    methods: {
        getImageUrl(path) {
            return `http://localhost:8000/${path}`;
        },           
        loadData() {
            axios
                .get('http://127.0.0.1:8000/api/khach-hang/trang-chu/data')
                .then((res) => {
                    this.monAnData = res.data.mon_an;
                    this.originalMonAnData = res.data.mon_an;
                    this.quanAn = res.data.quan_an_yeu_thich;
                    this.list_voucher = res.data.voucher;
                    this.phanLoai = res.data.phan_loai;
                })
                .catch((res) => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                })
        },
        xemThemMonAn() {
            this.soluonghienthi += 12;
        },
        filterByPrice(range) {
            switch (range) {
                case "under50":
                    this.monAnData = this.originalMonAnData.filter(
                        (item) => item.gia_khuyen_mai < 50000
                    );
                    break;
                case "50to100":
                    this.monAnData = this.originalMonAnData.filter(
                        (item) => item.gia_khuyen_mai >= 50000 && item.gia_khuyen_mai <= 100000
                    );
                    break;
                case "100to200":
                    this.monAnData = this.originalMonAnData.filter(
                        (item) => item.gia_khuyen_mai > 100000 && item.gia_khuyen_mai <= 200000
                    );
                    break;
                case "200to300":
                    this.monAnData = this.originalMonAnData.filter(
                        (item) => item.gia_khuyen_mai > 200000 && item.gia_khuyen_mai <= 300000
                    );
                    break;
                case "above300":
                    this.monAnData = this.originalMonAnData.filter(
                        (item) => item.gia_khuyen_mai > 300000
                    );
                    break;
                default:
                    this.monAnData = this.originalMonAnData; // Hiển thị tất cả nếu không có bộ lọc
                    break;
            }
        }
    },

};
</script>
<style>
.dropdown-menu {
    max-height: 250px;
    width: 100%;
    overflow-y: auto;
}

.page-content {
    margin-top: 0 !important;
    padding-top: 0 !important;
}
</style>

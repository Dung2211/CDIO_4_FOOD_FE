<template>
    <div class="row">
        <div class="col-lg-12">
            <div class="card">
                <div class="card-header" style="background-color: #CCCCCC;">
                    <div class="row">
                        <div class="col-lg-7">
                            <h5 class="mt-2 text-black">
                                Danh Mục Các Món Ăn <i class="fa-solid fa-bowl-food ms-1"></i>
                            </h5>
                        </div>
                        <div class="col-lg-5">
                            <div class="dropdown text-end">
                                <button class="btn mt-2 dropdown-toggle w-80" type="button" id="dropdownDanhMuc"
                                    data-bs-toggle="dropdown" aria-expanded="false">
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

                    </div>
                </div>
                <div class="card-body" style="background-color: #CCCCCC; border: none; box-shadow: none;">
                    <div class="row product-grid">
                        <template v-for="(v, k) in monAnHienThi" :key="k">
                            <div class="col-lg-2 d-flex">
                                <div class="card flex-fill border-0 shadow-none">
                                    <router-link :to="'/khach-hang/quan-an/' + v.id_quan_an">
                                        <img :src="v.hinh_anh" class="card-img-top"
                                            style="height: 200px; width: 100%;" />
                                        <div class="card-body">
                                            <h6 class="card-title cursor-pointer">
                                                {{ v.ten_mon_an }}
                                            </h6>
                                            <div class="clearfix">
                                                <p class="mb-0 float-start">{{ v.ten_quan_an }}</p>
                                            </div>
                                            <p class="mt-2">
                                                <del>{{ v.gia_ban }}đ</del>
                                                <strong class="ms-2">{{ v.gia_khuyen_mai }}đ</strong>
                                            </p>
                                            <div class="d-flex align-items-center mt-auto">
                                                <i class="fa-solid fa-tag text-danger me-2"></i>
                                                <span class="text-primary">-30%</span>
                                                <button class="btn ms-auto "
                                                    style="background-color: #FF9933; color: white;">Mua Ngay</button>
                                            </div>
                                        </div>
                                    </router-link>
                                </div>
                            </div>
                        </template>
                        <div class="col-lg-12 text-center">
                            <button class="btn btn-lg" style="width: 30%;" v-on:click="xemThemMonAn">
                                <i class="fa-solid fa-arrow-down"></i>Xem Thêm</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <div class="row mt-4">
        <div class="col-lg-12 text-center">
            <div class="d-inline-block">
                <h4><b>QUÁN ĂN ĐƯỢC YÊU THÍCH NHIỀU NHẤT</b></h4>
                <div class="text-center">
                    <hr class="bg-primary my-2" style="width: 100%; height: 3px; border: none; border-radius: 5px" />
                </div>
            </div>
        </div>
        <div class="card" style="background-color: #CCCCCC; border: none; box-shadow: none;">
            <div class="card-body">
                <div class="row product-grid">
                    <template v-for="(v, k) in quanAn" :key="k">
                        <div class="col-xl-4 col-lg-6 col-md-6 col-12 d-flex" v-if="k < 6">
                            <div class="card flex-fill border-0 shadow-none">
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
                                                        {{ v.gia }} </p>
                                                    <div class="d-flex align-items-center mt-3">
                                                        <i class="fa-solid fa-tag text-danger me-2"></i>
                                                        <span class="text-primary"><b>Giảm hết {{ v.giam_gia }}</b>
                                                        </span>
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
                            <span v-on:click="xemThemVoucher" class="text-white cursor-pointer">
                                <h6 class="text-white mt-3 text-end">Xem tất cả <i class="fa-solid fa-arrow-right"
                                        style="color: #ffffff;"></i></h6>
                            </span>
                        </div>
                    </div>
                </div>
                <div class="card-body" style="background-color:#8B0000; border: none; box-shadow: none;">
                    <div class="row product-grid">
                        <template v-for="(v, k) in voucherHienThi" :key="k">
                            <div class="col-lg-3 d-flex mb-0">
                                <div class="card flex-fill shadow-none">
                                    <img :src="getImageUrl(v.hinh_anh)" class="card-img-top">
                                    <div class="card-body">
                                        <h6 class="card-title cursor-pointer">{{ v.ten_voucher }}</h6>
                                        <div>
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
            soLuongHienThi: 12, // số món hiện tại đang hiển thị
            soLuongVoucher: 4 // số voucher hiện tại đang hiển thị
        };
    },
    created() {
        this.loadData();
    },
    computed: {
        monAnHienThi() {
            return this.monAnData.slice(0, this.soLuongHienThi);
        },
        voucherHienThi() {
            return this.list_voucher.slice(0, this.soLuongVoucher);
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
        chonDanhMuc(id_danh_muc) {
            if (id_danh_muc === 0) {
                // Nếu là "Tất cả" chẳng hạn
                this.monAnData = this.originalMonAnData;
            } else {
                this.monAnData = this.originalMonAnData.filter(mon => mon.id_danh_muc === id_danh_muc);
            }
            this.soLuongHienThi = 12; // reset lại số lượng hiển thị
        },
        xemThemMonAn() {
            this.soLuongHienThi += 12;
        },
        xemThemVoucher() {
            this.soLuongVoucher += 4;
        }
    },

};
</script>
<style></style>

<template>
    <!-- Tiêu đề + nút sắp xếp -->
    <div class="card border-0 shadow-sm mb-4">
        <div class="card-body">
            <div class="d-flex justify-content-between align-items-center">
                <div class="d-flex align-items-center">
                    <h2 class="card-title mb-0 fw-bold">Danh Sách Các Món Ăn</h2>
                </div>
                <div class="btn-group">
                    <button v-on:click="sapXepTangDan()" class="btn btn-sm rounded px-3"
                        style="background-color: #FF9933; color: white;">
                        <i class="fas fa-sort-amount-down-alt me-1"></i>
                        Giảm dần
                    </button>
                    <button v-on:click="sapXepGiamDan()" class="btn btn-sm rounded px-3 ms-2"
                        style="background-color: #FF9933; color: white;">
                        <i class="fas fa-sort-amount-up-alt me-1"></i>
                        Tăng dần
                    </button>
                </div>
            </div>
        </div>
    </div>
    <!-- Danh sách món ăn dạng ngang, 3 cột -->
    <div class="row">
        <template v-for="(value, index) in monAnHienThi" :key="index">
            <div class="col-xl-4 col-lg-4 col-md-4 col-sm-6 mb-3">
                <div class="card shadow-sm p-2 d-flex flex-row align-items-start h-100">
                    <img :src="value.hinh_anh" class="rounded"
                        style="width: 100px; height: 100px; object-fit: cover;" />
                    <router-link :to="'/khach-hang/quan-an/' + value.id_quan_an"
                        class="flex-grow-1 ms-3 text-decoration-none text-dark">
                        <div class="d-flex flex-column h-100 justify-content-between">
                            <div>
                                <p class="mb-1 fw-bold text-truncate">📍 {{ value.ten_quan_an }}</p>
                                <p class="mb-1 small text-muted">{{ value.ten_mon_an }}</p>
                            </div>
                            <div class="d-flex justify-content-between align-items-center">
                                <span class="text-success fw-bold">
                                    {{ formatVND(value.gia_khuyen_mai > 0 ? value.gia_khuyen_mai : value.gia_ban) }}
                                </span>
                                <button class="btn btn-sm btn-danger px-2 py-1" @click.stop>
                                    <i class="fas fa-plus"></i>
                                </button>
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
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            list_mon_an: [],
            soluonghienthi: 12, // Số lượng món ăn hiển thị ban đầu
        }
    },
    computed: {
        // Tính toán danh sách món ăn hiển thị dựa trên số lượng hiện tại
        monAnHienThi() {
            return this.list_mon_an.slice(0, this.soluonghienthi);
        }
    },
    mounted() {
        this.loadMonAn()
    },
    methods: {

        formatVND(number) {
            return new Intl.NumberFormat('vi-VI', { style: 'currency', currency: 'VND' }).format(number,)
        },
        loadMonAn() {
            axios
                .get('http://127.0.0.1:8000/api/khach-hang/data-mon-an', {
                    headers: {
                        Authorization: "Bearer " + localStorage.getItem("khach_hang_login"),
                    },
                })
                .then((res) => {
                    this.list_mon_an = res.data.data;
                })
                .catch(res => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                });
        },
        xemThemMonAn() {
            this.soluonghienthi += 12;
        },
        sapXepTangDan() {
            this.list_mon_an = this.list_mon_an.slice().sort((a, b) => {
                const giaA = (a.gia_khuyen_mai && a.gia_khuyen_mai > 0) ? a.gia_khuyen_mai : a.gia_ban;
                const giaB = (b.gia_khuyen_mai && b.gia_khuyen_mai > 0) ? b.gia_khuyen_mai : b.gia_ban;
                return giaA - giaB;
            });
        },
        sapXepGiamDan() {
            this.list_mon_an = this.list_mon_an.slice().sort((a, b) => {
                const giaA = (a.gia_khuyen_mai && a.gia_khuyen_mai > 0) ? a.gia_khuyen_mai : a.gia_ban;
                const giaB = (b.gia_khuyen_mai && b.gia_khuyen_mai > 0) ? b.gia_khuyen_mai : b.gia_ban;
                return giaB - giaA;
            });
        }
    }
}
</script>

<style scoped>
/* Nền xám nhạt cho toàn bộ danh sách món ăn */
.row {
    background-color: #CCCCCC;
    /* Màu xám nhẹ */
    padding: 20px;
    border-radius: 10px;
}

/* Giới hạn tên quán 1 dòng */
.text-truncate {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

/* Đổ bóng cho card rõ ràng hơn */
.card.shadow-sm {
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    border-radius: 10px;
}
</style>
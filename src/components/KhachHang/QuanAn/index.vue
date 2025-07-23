<template>
 <div class="row product-grid">
<!-- Thanh tab tượng trưng -->
<div class="d-flex justify-content-around border-bottom mb-3 fw-bold">
  <div class="tab-item text-center py-2 flex-fill tab-active">
    <span class="text-muted me-1"></span>Gần tôi
  </div>
  <div class="tab-item text-center py-2 flex-fill">
    <span class="text-muted me-1"></span>Bán chạy
  </div>
  <div class="tab-item text-center py-2 flex-fill">
    <span class="text-muted me-1"></span>Đánh giá tốt
  </div>
</div>
    <template v-for="(v, k) in list_quan_an" :key="k">
      <div class="col-xl-4 col-lg-6 col-md-6 col-12 d-flex">
        <div class="card flex-fill shadow-sm border-0 bg-white rounded">
          <router-link :to="'/khach-hang/quan-an/' + v.id" class="text-decoration-none text-dark">
            <div class="card-body">
              <div class="d-flex">
                <!-- Ảnh quán -->
                <img :src="v.hinh_anh" class="rounded" style="width: 100px; height: 100px; object-fit: cover;" />

                <!-- Nội dung quán -->
                <div class="ms-3 flex-grow-1 d-flex flex-column justify-content-between">
                  <div>
                    <h6 class="fw-bold mb-1 text-truncate">📍 {{ v.ten_quan_an }}</h6>
                    <p class="mb-1 small text-muted">{{ v.dia_chi }}</p>

                    <!-- Khoảng cách + thời gian -->
                    <div class="d-flex align-items-center text-muted small mb-2">
                      <i class="fas fa-star text-warning me-1"></i>
                      4.5
                      <span class="mx-2">|</span>
                      3,2KM
                      <span class="mx-2">|</span>
                      31 phút
                    </div>
                    <!-- Mã giảm -->
                    <div>
                      <span class="badge border border-danger text-danger bg-light px-3 py-2">
                        Mã giảm {{ v.giam_gia || '10%' }}
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
</template>
<script>
import axios from 'axios';

export default {
    data() {
        return {
            list_quan_an: [],
        }
    },
    mounted() {
        this.loadData();
    },
    methods: {
        formatVND(number) {
            return new Intl.NumberFormat('vi-VI', { style: 'currency', currency: 'VND' }).format(number,)
        },
        loadData() {
            axios
                .get('http://127.0.0.1:8000/api/khach-hang/quan-an/data', {
                    headers: {
                        Authorization: "Bearer " + localStorage.getItem("khach_hang_login"),
                    },
                })
                .then((res) => {
                    this.list_quan_an = res.data.data;
                })
                .catch((res) => {
                    const list = Object.values(res.response.data.errors);
                    list.forEach((v, i) => {
                        this.$toast.error(v[0]);
                    });
                })
        },
    },
}
</script>
<style scoped>
.tab-item {
  cursor: default;
  color: #000;
  border-bottom: 2px solid transparent;
  transition: 0.2s;
}

.tab-active {
  color: #FF6600; /* Cam nổi bật */
  border-bottom: 3px solid #FF6600;
}</style>
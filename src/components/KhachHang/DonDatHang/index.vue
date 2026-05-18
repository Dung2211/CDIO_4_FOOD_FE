<template>
  <div class="card shadow-sm mb-4">
    <div class="row g-0">
      <div class="col-md-4">
        <img
          :src="tt_quan_an.hinh_anh"
          style="width: 100%; height: 350px; object-fit: cover"
          class="img-fluid rounded-start"
          alt="Restaurant Image"
        />
      </div>
      <div class="col-md-8">
        <div class="card-body">
          <h4 class="card-title fw-bold">{{ tt_quan_an.ten_quan_an }}</h4>
          <div class="text-muted">
            <i class="fas fa-location-dot me-2 text-danger"></i>
            {{ tt_quan_an.dia_chi }}
          </div>
          <div class="d-flex gap-3 py-3">
            <div class="cursor-pointer">
              <i class="bx bxs-star text-warning"></i>
              <i class="bx bxs-star text-warning"></i>
              <i class="bx bxs-star text-warning"></i>
              <i class="bx bxs-star text-warning"></i>
              <i class="bx bxs-star text-secondary"></i>
            </div>
            <div>999+ đánh giá</div>
            <div class="text-success">
              <i class="fa-solid fa-circle fa-2xs"></i> Mở cửa
            </div>
          </div>
          <div class="mb-3">
            <p>
              <i class="fa-regular fa-clock"></i> {{ tt_quan_an.gio_mo_cua }} -
              {{ tt_quan_an.gio_dong_cua }}
            </p>
            <p>
              <i class="fa-solid fa-circle-dollar-to-slot"></i> 20.000 - 100.000
            </p>
          </div>
          <hr />
          <div
            class="row row-cols-auto row-cols-1 row-cols-md-3 align-items-center"
          >
            <div class="col">
              <div class="row">
                <div class="col-lg-5">
                  <h6 class="form-label">PHÍ DỊCH VỤ</h6>
                  <h6 class="text-danger">0.0%</h6>
                </div>
                |
                <div class="col-lg-5">
                  <h6 class="form-label">DỊCH VỤ BỞI</h6>
                  <h6 class="text-danger">K-FOODS</h6>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div class="container-fluid mt-4">
    <h3 class="mb-4">
      <i class="fas fa-utensils me-2"></i><b class="text-danger">THỰC ĐƠN</b>
    </h3>
    <div class="row">
      <div class="col-md-6">
        <div class="card shadow-sm">
          <div class="card-body">
            <div
              class="alert alert-warning border-start border-warning border-4"
            >
              <div class="d-flex align-items-center">
                <i class="fas fa-ticket-alt text-danger fa-2x"></i>
                <div class="ms-3">
                  <span class="fs-5 fw-semibold"
                    >HOME CREDIT giảm 50k cho đơn từ 100k</span
                  >
                </div>
              </div>
            </div>

            <div class="position-relative mb-4">
              <input
                type="text"
                class="form-control form-control-lg ps-5"
                placeholder="Tìm kiếm món ăn..."
              />
              <i
                class="fas fa-search position-absolute top-50 start-0 translate-middle-y ms-3 text-muted"
              ></i>
            </div>

            <h5 class="mb-3 fw-bold">Danh Sách Món Ăn</h5>
            <template v-for="(v, k) in monAnData" :key="k">
              <div class="card mb-3 hover-shadow">
                <div class="d-flex align-items-center p-3">
                  <img
                    :src="v.hinh_anh"
                    class="me-3 rounded"
                    style="width: 120px; height: 90px; object-fit: cover"
                  />
                  <div class="flex-grow-1">
                    <h5 class="mb-1 fw-bold">{{ v.ten_mon_an }}</h5>
                    <p class="mb-0">
                      <del class="text-muted"
                        >{{ v.gia_ban.toLocaleString() }}đ</del
                      >
                      <strong class="text-danger ms-2"
                        >{{ v.gia_khuyen_mai.toLocaleString() }}đ</strong
                      >
                    </p>
                  </div>
                  <button
                    v-on:click="themGioHang(v.id)"
                    class="btn btn-outline-primary"
                  >
                    +
                  </button>
                </div>
              </div>
            </template>
          </div>
        </div>
      </div>

      <div class="col-md-6">
        <div class="card shadow-sm">
          <div class="card-header bg-success py-3">
            <h5 class="mb-0 text-white">
              <i class="fas fa-shopping-cart me-2"></i>Đơn Hàng Đang Đặt
            </h5>
          </div>
          <div class="card-body">
            <div class="table-responsive">
              <table class="table table-bordered table-hover">
                <thead>
                  <tr class="text-center table-secondary">
                    <th class="align-middle">Tên món</th>
                    <th class="align-middle">Số lượng</th>
                    <th class="align-middle">Đơn giá</th>
                    <th class="align-middle">Ghi chú</th>
                    <th class="align-middle">Thành Tiền</th>
                    <th class="align-middle">Action</th>
                  </tr>
                </thead>
                <tbody>
                  <template v-if="list_gio_hang && list_gio_hang.length > 0">
                    <template v-for="(v, k) in list_gio_hang" :key="k">
                      <tr class="align-middle">
                        <td>{{ v.ten_mon_an }}</td>
                        <td style="width: 100px">
                          <input
                            v-on:blur="updateGioHang(v)"
                            v-model="v.so_luong"
                            type="number"
                            class="form-control text-center"
                            placeholder="1"
                          />
                        </td>
                        <td class="text-end">{{ formatVND(v.don_gia) }}</td>
                        <td>
                          <input
                            v-on:change="updateGioHang(v)"
                            v-model="v.ghi_chu"
                            type="text"
                            class="form-control"
                            placeholder="Ghi chú"
                          />
                        </td>
                        <td class="text-end">{{ formatVND(v.thanh_tien) }}</td>
                        <td class="align-middle text-center">
                          <button
                            v-on:click="xoaGioHang(v)"
                            class="btn btn-danger"
                          >
                            Hủy
                          </button>
                        </td>
                      </tr>
                    </template>
                    <tr class="align-middle">
                      <th>Chọn địa chỉ nhận hàng</th>
                      <th colspan="3">
                        <select
                          v-model="dia_chi.id_dia_chi_khach"
                          v-on:change="tinhPhiShip()"
                          class="form-control"
                        >
                          <template
                            v-for="(value, index) in list_dia_chi"
                            :key="index"
                          >
                            <option :value="value.id">
                              {{ value.dia_chi }} - {{ value.ten_nguoi_nhan }} -
                              {{ value.so_dien_thoai }}
                            </option>
                          </template>
                        </select>
                      </th>
                      <td colspan="2">
                        <span class="d-flex justify-content-between"
                          ><b>Phí Ship: </b>{{ formatVND(phi_ship) }}</span
                        >
                      </td>
                    </tr>
                    <tr class="align-middle">
                      <th>Chọn hình thức thanh toán</th>
                      <td colspan="5">
                        <select
                          v-model="hinh_thuc_thanh_toan"
                          class="form-control"
                        >
                          <option value="cod">
                            Thanh toán khi nhận hàng (COD)
                          </option>
                          <option value="momo">Ví điện tử Momo</option>
                        </select>
                      </td>
                    </tr>
                    <tr
                      class="align-middle"
                      v-show="hinh_thuc_thanh_toan == 'momo'"
                    >
                      <td colspan="6" class="text-center bg-light py-3">
                        <h5 class="text-danger fw-bold">
                          <i class="fa-solid fa-qrcode me-2"></i>Quét mã Momo để
                          thanh toán
                        </h5>
                        <img
                          src="/public/img/qr-momo.jpg"
                          alt="Momo QR"
                          width="150"
                          class="img-fluid border rounded shadow-sm mb-2"
                        />
                        <p class="mb-0 text-muted small">
                          Vui lòng ghi nội dung chuyển khoản là SĐT của bạn.
                        </p>
                      </td>
                    </tr>
                    <tr>
                      <th colspan="4">Tổng tiền cần thanh toán:</th>
                      <td colspan="2" class="text-end align-middle text-danger">
                        <b>{{ formatVND(tong_tien + phi_ship) }}</b>
                      </td>
                    </tr>
                  </template>

                  <template v-else>
                    <tr>
                      <td colspan="6" class="text-center text-danger py-4">
                        <h5>
                          <i class="fa-solid fa-cart-arrow-down me-2"></i> Giỏ
                          hàng đang trống! Vui lòng chọn món ăn.
                        </h5>
                      </td>
                    </tr>
                  </template>
                </tbody>
              </table>

              <button
                v-if="
                  trang_thai == 0 || list_gio_hang.length == 0 || is_loi_dia_chi
                "
                disabled
                class="btn btn-danger w-100 mt-2"
              >
                Đặt Món Ăn
              </button>

              <button
                v-else
                v-on:click="xacNhan()"
                class="btn btn-success w-100 mt-2"
              >
                Đặt Món Ăn
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  props: ["id_quan"],
  data() {
    return {
      id_quan_an: this.$route.params.id_quan,
      tt_quan_an: {},
      monAnData: [],
      list_gio_hang: [],
      tong_tien: 0,
      trang_thai: 0,
      dia_chi: {
        id_quan_an: this.$route.params.id_quan,
        id_dia_chi_khach: 0,
      },
      phi_ship: 0,
      list_dia_chi: [],
      hinh_thuc_thanh_toan: "cod", // 🚀 ĐÃ KHAI BÁO BIẾN MOMO Ở ĐÂY
      is_loi_dia_chi: false,
    };
  },
  mounted() {
    this.loadData();
  },
  methods: {
    xacNhan() {
      this.trang_thai = 0;

      var url =
        "http://127.0.0.1:8000/api/khach-hang/xac-nhan-dat-hang/" +
        this.id_quan_an +
        "/" +
        this.dia_chi.id_dia_chi_khach +
        "?thanh_toan=" +
        this.hinh_thuc_thanh_toan;
      axios
        .get(url, {
          headers: {
            Authorization: "Bearer " + localStorage.getItem("khach_hang_login"),
          },
        })
        .then((res) => {
          if (res.data.status) {
            this.$toast.success(res.data.message);
            this.trang_thai = 1;
            this.loadData();
          } else {
            this.$toast.error("Hệ thống bị lỗi, vui lòng thử lại sau!");
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
    },
    formatVND(number) {
      return new Intl.NumberFormat("vi-VI", {
        style: "currency",
        currency: "VND",
      }).format(number);
    },
    loadData() {
      axios
        .get(
          "http://127.0.0.1:8000/api/khach-hang/don-dat-hang/" +
            this.id_quan_an,
          {
            headers: {
              Authorization:
                "Bearer " + localStorage.getItem("khach_hang_login"),
            },
          },
        )
        .then((res) => {
          if (res.data.status) {
            this.tt_quan_an = res.data.quan_an;
            this.monAnData = res.data.mon_an;
            this.list_gio_hang = res.data.gio_hang;
            this.tong_tien = res.data.tong_tien;
            this.list_dia_chi = res.data.dia_chi_khach;

            // Nếu giỏ hàng trống thì clear phí ship cho an toàn
            if (this.list_gio_hang.length === 0) {
              this.phi_ship = 0;
              this.trang_thai = 0;
            } else if (
              this.list_dia_chi.length > 0 &&
              this.dia_chi.id_dia_chi_khach == 0
            ) {
              // Tự động gán địa chỉ đầu tiên và tính phí ship luôn
              this.dia_chi.id_dia_chi_khach = this.list_dia_chi[0].id;
              this.tinhPhiShip();
            }
          } else {
            this.$router.push("/khach-hang/quan-an");
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
    },
    themGioHang(id_mon_an) {
      var payload = {
        id: id_mon_an,
      };
      axios
        .post(
          "http://127.0.0.1:8000/api/khach-hang/don-dat-hang/create",
          payload,
          {
            headers: {
              Authorization:
                "Bearer " + localStorage.getItem("khach_hang_login"),
            },
          },
        )
        .then((res) => {
          if (res.data.status) {
            this.$toast.success(res.data.message);
            this.loadData();
          } else {
            this.$toast.error(res.data.message);
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
    },
    updateGioHang(value) {
      axios
        .post(
          "http://127.0.0.1:8000/api/khach-hang/don-dat-hang/update",
          value,
          {
            headers: {
              Authorization:
                "Bearer " + localStorage.getItem("khach_hang_login"),
            },
          },
        )
        .then((res) => {
          if (res.data.status) {
            this.$toast.success(res.data.message);
          } else {
            this.$toast.error(res.data.message);
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
      this.loadData();
    },
    xoaGioHang(value) {
      axios
        .post(
          "http://127.0.0.1:8000/api/khach-hang/don-dat-hang/delete",
          value,
          {
            headers: {
              Authorization:
                "Bearer " + localStorage.getItem("khach_hang_login"),
            },
          },
        )
        .then((res) => {
          if (res.data.status) {
            this.$toast.success(res.data.message);
            this.loadData();
          } else {
            this.$toast.error(res.data.message);
          }
        })
        .catch((res) => {
          const list = Object.values(res.response.data.errors);
          list.forEach((v, i) => {
            this.$toast.error(v[0]);
          });
        });
    },
    tinhPhiShip() {
      this.trang_thai = 0;
      this.is_loi_dia_chi = false; // Reset lại trạng thái lỗi mỗi lần tính phí

      axios
        .post(
          "http://127.0.0.1:8000/api/khach-hang/don-dat-hang/phi-ship",
          this.dia_chi,
          {
            headers: {
              Authorization:
                "Bearer " + localStorage.getItem("khach_hang_login"),
            },
          },
        )
        .then((res) => {
          if (res.data.status) {
            // Trường hợp 1: Địa chỉ hợp lệ, tính được phí ship
            this.phi_ship = res.data.phi_ship;
            this.trang_thai = 1;
            this.is_loi_dia_chi = false; // Mở khóa nút đặt hàng
          } else {
            // 🚀 Trường hợp 2: Bị văng do quá 20km hoặc khác Đà Nẵng
            this.$toast.error(res.data.message); // In câu báo lỗi từ Backend ra
            this.phi_ship = 0; // Đưa phí ship về 0
            this.trang_thai = 0;
            this.is_loi_dia_chi = true; // Khóa nút đặt hàng lại!
          }
        })
        .catch((res) => {
          // Lỗi Validation hoặc lỗi Server
          if (res.response && res.response.data && res.response.data.errors) {
            const list = Object.values(res.response.data.errors);
            list.forEach((v, i) => {
              this.$toast.error(v[0]);
            });
          } else {
            this.$toast.error("Lỗi hệ thống khi tính phí ship!");
          }
          this.is_loi_dia_chi = true; // Lỗi thì cũng khóa nút luôn cho an toàn
        });
    },
  },
};
</script>

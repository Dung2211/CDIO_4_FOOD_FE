<template>
  <div class="row">
    <div class="col-lg-12">
      <div class="card">
        <div class="card-header bg-warning">
          <h5 class="mt-2 text-dark">
            <i class="fa-solid fa-star me-2"></i>ĐÁNH GIÁ TỪ KHÁCH HÀNG
          </h5>
        </div>
        <div class="card-body">
          <div class="table-responsive">
            <table
              class="table table-bordered table-hover align-middle text-center"
            >
              <thead class="table-secondary">
                <tr>
                  <th>Mã Đơn Hàng</th>
                  <th>Khách Hàng</th>
                  <th>Mức Độ Hài Lòng</th>
                  <th>Nội Dung Đánh Giá</th>
                  <th>Thời Gian</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(value, index) in list_danh_gia" :key="index">
                  <td class="fw-bold text-danger">{{ value.ma_don_hang }}</td>
                  <td>{{ value.ten_khach_hang }}</td>
                  <td class="text-warning fs-5">
                    <i
                      v-for="n in value.so_sao"
                      :key="'sao' + n"
                      class="fa-solid fa-star"
                    ></i>
                    <i
                      v-for="n in 5 - value.so_sao"
                      :key="'saotrong' + n"
                      class="fa-regular fa-star text-muted"
                    ></i>
                  </td>
                  <td class="text-start">
                    {{ value.noi_dung ? value.noi_dung : "Không có bình luận" }}
                  </td>
                  <td>{{ formatTime(value.created_at) }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      list_danh_gia: [],
    };
  },
  mounted() {
    this.loadDanhGia();
  },
  methods: {
    loadDanhGia() {
      // Nhớ kiểm tra lại tên biến localStorage lưu token của Quán Ăn nhé (ở đây mình giả định là quan_an_login)
      var token = localStorage.getItem("quan_an_login");
      axios
        .get("http://127.0.0.1:8000/api/quan-an/danh-gia/data", {
          headers: {
            Authorization: "Bearer " + token,
          },
        })
        .then((res) => {
          if (res.data.status) {
            this.list_danh_gia = res.data.data;
          }
        })
        .catch((res) => {
          this.$toast.error("Lỗi hệ thống, không tải được đánh giá!");
        });
    },
    formatTime(datetime) {
      if (!datetime) return "";

      // Ép chuỗi về chuẩn ISO bằng cách thay dấu cách thành 'T' và thêm 'Z' ở cuối
      // Chữ 'Z' báo cho Javascript biết đây là giờ UTC, nó sẽ TỰ ĐỘNG cộng thêm 7 tiếng cho Việt Nam
      let fixedTime = datetime;
      if (typeof fixedTime === "string" && !fixedTime.includes("T")) {
        fixedTime = fixedTime.replace(" ", "T") + "Z";
      }

      const date = new Date(fixedTime);
      return date.toLocaleString("vi-VN");
    },
  },
};
</script>

<style></style>

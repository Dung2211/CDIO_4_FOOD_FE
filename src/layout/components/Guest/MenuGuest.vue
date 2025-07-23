<template>
   
    <div id="carouselExampleControls" class="carousel slide pointer-event" data-bs-ride="carousel">
        <ol class="carousel-indicators">
            <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class=""></li>
            <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1" class=""></li>
            <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2" class="active" aria-current="true">
            </li>
        </ol>
        <div class="carousel-inner">
            <div class="carousel-item rounded-4" data-bs-interval="2000" style="background-color: #111111;">
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
                            <p class="mt-4"><button class="btn btn-outline-light rounded-4"> <b>TRẢI NGHIỆM
                                        NGAY</b> </button></p>
                        </div>
                    </div>
                    <div class="col-6">
                        <img src="https://png.pngtree.com/png-clipart/20241112/original/pngtree-food-delivery-by-scooters-free-download-png-image_16940462.png"
                            class="d-block w-100 rounded-4" alt="..."
                            style="width: 400px; height: 500px; object-fit: cover;">
                    </div>
                </div>
            </div>
            <div class="carousel-item active rounded-4" data-bs-interval="10000" style="background-color: #111111;">
                <div class="row">
                    <div class="col-6 d-flex align-items-center">
                        <div class="container ms-5">
                            <h2 class="text-white mb-4">Ưu đãi hấp dẫn - Đặt ngay hôm nay!
                                <i class="fa-brands fa-square-web-awesome-stroke text-warning"></i>
                            </h2>
                            <span class="text-white">
                                Giảm đến 50% cho lần đặt hàng đầu tiên. Hàng ngàn món ăn ngon đang chờ bạn khám
                                phá! Nhanh tay đặt ngay để không bỏ lỡ!
                            </span>
                            <p class="mt-4"><button class="btn btn-outline-light rounded-4"> <b>ĐẶT HÀNG
                                        NGAY</b> </button></p>
                        </div>
                    </div>
                    <div class="col-6">
                        <img src="https://alltop.vn/backend/media/images/posts/695/Dominos_Pizza-196049.jpg"
                            class="d-block w-100 rounded-4" alt="..."
                            style="width: 450px; height: 500px; object-fit: cover;">
                    </div>
                </div>
            </div>
            <div class="carousel-item rounded-4" style="background-color: #111111;">
                <div class="row">
                    <div class="col-6 d-flex align-items-center">
                        <div class="container ms-5">
                            <h2 class="text-white mb-4">Khám phá thế giới ẩm thực ngay tại nhà!
                            </h2>
                            <span class="text-white">
                                Hàng ngàn món ăn từ Việt Nam, Âu, Á, Fusion đang sẵn sàng phục vụ bạn. Chỉ cần vài
                                cú nhấp chuột, tất cả ẩm thực sẽ đến ngay trước cửa nhà!
                            </span>
                            <p class="mt-4"><button class="btn btn-outline-light rounded-4"> <b>THỬ NGAY</b>
                                </button></p>
                        </div>
                    </div>
                    <div class="col-6">
                        <img src="https://vj-prod-website-cms.s3.ap-southeast-1.amazonaws.com/shutterstock371955106huge-1675245432977.jpg"
                            class="d-block w-100 rounded-4" alt="..."
                            style="width: 450px; height: 500px; object-fit: cover;">
                    </div>
                </div>
            </div>

        </div>
        <a class="carousel-control-prev" href="#carouselExampleControls" role="button" data-bs-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Previous</span>
        </a>
        <a class="carousel-control-next" href="#carouselExampleControls" role="button" data-bs-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="visually-hidden">Next</span>
        </a>
    </div>
</template>
<script>
export default {
    data() {
        return {
            noi_dung_timm: '',

        }
    },
    methods: {
        timKiem() {
            this.$router.push({
                name: 'name_tim_kiem',
                params: {
                    thong_tin: this.noi_dung_timm,
                }
            });
        },

    }
}
</script>
<style></style>
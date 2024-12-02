<template>
    <main class="mt-3">
        <div class="container">
            <div class="row">
                <div class="col-md-5">
                    <div id="carouselExampleIndicators" class="carousel slide" data-bs-ride="carousel">
                    <ol class="carousel-indicators">
                        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></li>
                        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="1"  aria-label="Slide 2"></li>
                        <li data-bs-target="#carouselExampleIndicators" data-bs-slide-to="2" aria-label="Slide 3"></li>
                    </ol>
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img src="../download/images/keyboard.jpg" class="d-block w-100" alt="...">
                        </div>
                        <div class="carousel-item">
                            <img src="../download/images/keyboard.jpg" class="d-block w-100" alt="...">
                        </div>
                        <div class="carousel-item">
                            <img src="../download/images/keyboard.jpg" class="d-block w-100" alt="...">
                        </div>
                    </div>
                    <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-bs-slide="prev">
                        <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                        <span class="visually-hidden">Previous</span>
                    </a>
                    <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-bs-slide="next">
                        <span class="carousel-control-next-icon" aria-hidden="true"></span>
                        <span class="visually-hidden">Next</span>
                    </a>
                    </div>
                </div>
                <div class="col-md-7">
                    <div class="card shadow-sm">
                        <div class="card-body">
                            <h5 class="card-title">키보드</h5>
                            <h5 class="card-tile py-3 border-top">5000원</h5>
                            <p class="card-text border-top pt-3">
                                <span class="badge bg-dark me-1">전자제품</span>
                                <span class="badge bg-dark me-1">컴퓨터</span>
                                <span class="badge bg-dark">악세사리</span>
                            </p>
                            <p class="card-text pd-3">
                                배송비 3000원 | 도서산간(제주도) 배송비 추가 5000원 | 택배배송 | 3일 이내 출고 (주말, 공휴일 제외)
                            </p>
                            <div class="card-text border-top pd-3">
                                <div class="row my-3">
                                    <div class="col-auto">
                                        <label class="col-form-label">구매수량</label>
                                    </div>
                                    <div class="col-auto">
                                        <div class="input-group">
                                            <span class="input-group-text" style="cursur:pointer;" @click="calculatePrice(-1);">-</span>
                                            <input type="text" class="form-control" style="width:40px;" v-model="total">
                                            <span class="input-group-text" style="cursur:pointer;" @click="calculatePrice(1);">+</span>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="row py-3 border-top">
                                <div class="col-6">
                                    <h3>총 상품금액</h3>
                                </div>
                                <div class="col-6" style="text-align:right;">
                                    <h3>5000원</h3>
                                </div>
                            </div>
                            <div class="d-flex justify-content-between align-items-center">
                                <div class="col-6 d-grid p-1">
                                    <button type="button" class="btn btn-lg btn-dark">장바구니 담기</button>
                                </div>
                                <div class="col-6 d-grid p-1">
                                    <button type="button" class="btn btn-lg btn-danger">주문하기</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-12">
                    <img src="../download/images/keyboard.jpg" alt="" class="img-fluid">
                </div>
            </div>
        </div>
    </main>
</template>

<script>
    export default {
        data(){
            return{
                productId:0,
                productDetail:{},
                productImage:[],
                total:1,
                totalPrice:0
            };
        },
        created(){
            this.productId = this.$route.query.product_id;
            this.getProductDetail();
            this.getProductImage();
        },
        methods:{
             calculatePrice(cnt){
                let total = this.total + cnt;
                if(total < 1) total = 1;
                this.total = total;
                this.totalPrice = this.productDetail.product_price * this.total;
             },
             getCurrencyFormat(value){
                return this.$currencyFormat(value);
             },
             async getProductDetail(){
                let productDetail = await this.$api("/api/productDetail",{param:[this.productId]});
                if(productDetail.length > 0){
                    this.productDetail = productDetail[0];
                    this.totalPrice = this.totalPrice = this.productDetail.product_price * this.total;
                }
                console.log(this.productDetail);
             },
             async getProductImage(){
                this.productImage = await this.$api("/api/productMainImages",{param:[this.productId]});
                console.log('this.productImage',this.productImage)
             }
        }
    }
</script>

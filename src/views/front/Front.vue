<template>
  <div>
    <Navbar @openModal="openDelModal" @openAddModal="addtoCartModal" />
    <main role="main">
      <router-view></router-view>
    </main>
    <Subscribe />
    <Footer />
    <!--刪除購物車商品 Modal-->
    <div class="modal fade" id="delProductModal" tabindex="-1" role="dialog"
     aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog modal-sm" role="document">
        <div class="modal-content">
          <div class="modal-header bg-danger">
            <h5 class="modal-title text-light" >刪除商品</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
          <div class="modal-body">
            是否自購物車刪除商品(刪除後將無法恢復)？
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-outline-secondary" data-dismiss="modal">取消</button>
            <button type="button" class="btn btn-danger" @click="removeCart">確認刪除</button>
          </div>
        </div>
      </div>
    </div>

    <!-- 成功加入購物車 Modal -->
    <div class="modal fade" id="addtoCartModal" tabindex="-1" role="dialog"
     aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog modal-sm" role="document">
        <div class="modal-content">
          <div class="modal-body">
            成功加入購物車！
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';
import Navbar from '../../components/Navbar.vue';
import Subscribe from '../../components/Subscribe.vue';
import Footer from '../../components/Footer.vue';

export default {
  components: {
    Navbar,
    Subscribe,
    Footer,
  },
  data() {
    return {
      tempProduct: {},
    };
  },
  methods: {
    openDelModal(item) {
      // 將所點選的產品資料帶入
      this.tempProduct = item;
      // 開啟刪除產品 modal
      $('#delProductModal').modal('show');
    },
    removeCart() {
      this.$store.dispatch('removeCart', this.tempProduct.id);
      $('#delProductModal').modal('hide');
    },
    getCart() {
      this.$store.dispatch('getCart');
    },
    addtoCartModal() {
      window.setTimeout(() => {
        $('#addtoCartModal').modal('show');
      }, 2500);
      window.setTimeout(() => {
        $('#addtoCartModal').modal('hide');
      }, 4000);
    },
  },
  created() {
    this.getCart();
  },
};
</script>

<script>
export default {
  name: "Show",
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  computed: {
    _imageStyle() {
      return {
        width: "200px",
        height: "200px",
        objectFit: "cover",
      };
    },
  },
};
</script>

<template>
  <div class="container mt-3">
    <div class="row">
      <div class="col-12">
        <h4 class="text-success">Detail produk</h4>
        <small class="text-success">
          Informasi Detail Produk
        </small>
        <hr />
      </div>
    </div>
    <div class="row">
      <div class="col-lg-6 col-md-12 col-sm-6">
        <table class="table">
          <tbody>
            <tr>
              <td>Kode Produk</td>
              <td>{{ product.sku }}</td>
            </tr>
            <tr>
              <td>Nama roduk</td>
              <td>{{ product.nama }}</td>
            </tr>
            <tr>
              <td>Deskripsi</td>
              <td>{{ product.deskripsi ? product.deskripsi : "Tidak ada deskripsi" }}</td>
            </tr>
            <tr>
              <td>Foto</td>
              <td>
                <img 
                  v-if="product.foto" 
                  :src="'/storage/' + product.foto" 
                  :alt="product.nama" 
                  :style="_imageStyle" 
                />
                <span v-else>Tidak ada foto</span>
              </td>
            </tr>
            <tr>
              <td>Stok</td>
              <td>{{ product.stok }}</td>
            </tr>
            <tr>
              <td></td>
              <td>
                <router-link class="btn btn-primary btn-sm" to="/products">
                  Kembali ke beranda
                </router-link>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

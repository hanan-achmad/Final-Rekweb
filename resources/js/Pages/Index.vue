<template>
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h2 class="text-center text-primary">Data produk</h2>
          <hr />
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <!-- menampilkan pesan flash jika ada -->
          <div
            v-if="flash.msg"
            class="alert alert-success alert-dismissible fade show"
            role="alert"
          >
            <span class="text-center">{{ flash.msg }}</span>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="alert"
              aria-label="Close"
            ></button>
          </div>
          <router-link to="/products/create" class="btn btn-primary btn-sm mb-3">
            + Tambah produk
          </router-link>
  
          <table class="table">
            <thead>
              <tr>
                <th>No</th>
                <th>Kode Produk</th>
                <th>Nama Produk</th>
                <th>Aksi</th>
              </tr>
            </thead>
            <tbody>
              <tr v-if="products.length === 0">
                <td colspan="4" class="text-center text-danger">
                  Tidak ada data
                </td>
              </tr>
              <tr v-else v-for="(product, index) in products" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ product.sku }}</td>
                <td>{{ product.nama }}</td>
                <td>
                  <router-link
                    :to="`/products/${product.sku}`"
                    class="btn btn-primary btn-sm me-1"
                  >
                    Lihat
                  </router-link>
                  <router-link
                    :to="`/products/${product.sku}/edit`"
                    class="btn btn-warning btn-sm me-1"
                  >
                    Edit
                  </router-link>
                  <button
                    :id="product.sku"
                    @click="handleDelete(product.sku)"
                    class="btn btn-danger btn-sm"
                  >
                    Hapus
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Swal from "sweetalert2";
  import { usePage, router } from "@inertiajs/vue3";
  
  export default {
    name: "Index",
    props: {
      products: {
        type: Array,
        required: true,
      },
    },
    setup() {
      const { flash } = usePage().props;
  
      const handleDelete = (sku) => {
        Swal.fire({
          title: "Are you sure?",
          text: "You won't be able to revert this!",
          icon: "warning",
          showCancelButton: true,
          confirmButtonColor: "#3085d6",
          cancelButtonColor: "#d33",
          confirmButtonText: "Yes, delete it!",
        }).then((result) => {
          if (result.isConfirmed) {
            router.delete(`/products/${sku}`);
          }
        });
      };
  
      return {
        flash,
        handleDelete,
      };
    },
  };
  </script>
  
<script>
import { reactive } from "vue";
import { router, usePage } from "@inertiajs/vue3";
</script>

<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h4 class="mt-3 text-primary">Edit Produk</h4>
        <hr />
      </div>
      <div class="col-12">
        <router-link to="/products" class="btn btn-primary btn-sm my-3">
          Kembali
        </router-link>
        <div class="card">
          <div class="card-body">
            <form @submit.prevent="handleFormSubmit" enctype="multipart/form-data">
              <div class="mb-3">
                <label for="sku" class="form-label">Kode Produk</label>
                <input
                  type="text"
                  :class="errors.sku ? 'form-control is-invalid' : 'form-control'"
                  id="sku"
                  v-model="input.sku"
                />
                <div v-if="errors.sku" class="invalid-feedback">
                  {{ errors.sku }}
                </div>
              </div>
              <div class="mb-3">
                <label for="nama" class="form-label">Nama produk</label>
                <input
                  type="text"
                  :class="errors.nama ? 'form-control is-invalid' : 'form-control'"
                  id="nama"
                  v-model="input.nama"
                />
                <div v-if="errors.nama" class="invalid-feedback">
                  {{ errors.nama }}
                </div>
              </div>
              <div class="mb-3">
                <label for="deskripsi" class="form-label">Deskripsi produk</label>
                <textarea
                  :class="errors.deskripsi ? 'form-control is-invalid' : 'form-control'"
                  id="deskripsi"
                  rows="3"
                  v-model="input.deskripsi"
                ></textarea>
                <div v-if="errors.deskripsi" class="invalid-feedback">
                  {{ errors.deskripsi }}
                </div>
              </div>
              <div class="mb-3">
                <label for="foto" class="form-label">Foto produk</label>
                <input
                  type="file"
                  class="form-control"
                  id="foto"
                  @change="handleFileChange"
                />
                <div v-if="errors.foto" class="invalid-feedback">
                  {{ errors.foto }}
                </div>
              </div>
              <div class="mb-3">
                <label for="stok" class="form-label">Stok</label>
                <input
                  type="number"
                  :class="errors.stok ? 'form-control is-invalid' : 'form-control'"
                  id="stok"
                  min="0"
                  v-model="input.stok"
                />
                <div v-if="errors.stok" class="invalid-feedback">
                  {{ errors.stok }}
                </div>
              </div>
              <button type="submit" class="btn btn-primary">Update</button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Create",
  props: {
    errors: {
      type: Object,
      required: true,
    },
    product: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    const input = reactive({
      sku: props.product.sku,
      nama: props.product.nama,
      deskripsi: props.product.deskripsi || "",
      foto: null,
      stok: props.product.stok,
    });

    const handleFormSubmit = () => {
      router.post(`/products/${props.product.sku}`, {
        _method: "put",
        ...input,
      });
    };

    const handleFileChange = (e) => {
      input.foto = e.target.files[0];
    };

    return {
      input,
      handleFormSubmit,
      handleFileChange,
    };
  },
};
</script>

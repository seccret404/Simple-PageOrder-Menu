<template>
    <div class="keranjang">
        <Navbar :updateKeranjang="keranjang" />
        <!--mengoper nilai kembali kepada keranjang-->
        <div class="container">
            <div class="row mt-3">
                <div class="col">
                    <nav aria-label="breadcrumb">
                        <ol class="breadcrumb">
                            <li class="breadcrumb-item">
                                <router-link to="/">Home</router-link>
                            </li>
                            <li class="breadcrumb-item">
                                <router-link to="/food">Food</router-link>
                            </li>
                            <li class="breadcrumb-item active" aria-current="page">Keranjang <strong>Saya</strong></li>
                        </ol>
                    </nav>
                </div>
            </div>
            <div class="row">
                <div class="col">
                    <h5>
                        <b-icon-cart></b-icon-cart> Keranjang <strong>Saya</strong>
                    </h5>
                    <div class="table-responsive mt-3">
                        <table class="table table-hover">
                            <thead>
                                <tr>
                                    <th>No</th>
                                    <th>Gambar</th>
                                    <th>Nama</th>
                                    <th>Keterangan</th>
                                    <th>Jumlah </th>
                                    <th>Harga</th>
                                    <th>Total Harga</th>
                                    <th>Hapus</th>
                                </tr>
                            </thead>

                            <tr v-for="(keranjang, index) in keranjang " :key="keranjang.id">
                                <!--melakukan foreach-->
                                <th>{{ index+1 }}</th>
                                <td>
                                    <img :src=" '../assets/image/' + keranjang.products.gambar"
                                        class="card-img-top shadow mb-4 shadow" alt="..." id="image">
                                </td>
                                <td>
                                    <strong>{{ keranjang.products.nama }}</strong>
                                </td>
                                <td>{{ keranjang.keterangan ? keranjang.keterangan : "-" }}</td>
                                <td>
                                    <strong>{{ keranjang.jumlah_pemesanan }}</strong>
                                </td>


                                <td>Rp.{{ keranjang.products.harga }}</td>
                                <td><strong>Rp.{{ keranjang.products.harga*keranjang.jumlah_pemesanan }}</strong> </td>
                                <td align="center" class="text-danger">
                                    <b-icon-trash @click="hapusKeranjang(keranjang.id)"></b-icon-trash>
                                </td>
                            </tr>
                            <tr>
                                <td colspan="6" align="right"><strong>Total Harga :</strong></td>
                                <td>
                                    <strong>Rp.{{ totalHarga }}</strong>
                                </td>
                            </tr>
                        </table>


                    </div>
                </div>
            </div>
            <!--checkout-->
            <div class="row justify-content-end">
                <div class="col-md-4">
                    <form action="" v-on:submit.prevent>
                        <div class="form-group">
                            <label for="nama">Nama : </label>
                            <input type="text" class="form-control" min="1" placeholder="Nama Pemesan"
                                v-model="pesan.nama">
                        </div>
                        <div class="form-group">
                            <label for="noMeja">Nomor Meja : </label>
                            <input type="text" class="form-control" min="1" placeholder="Nomor meja contoh: 2"
                                v-model="pesan.noMeja">
                        </div>


                        <button type="submit" class="btn btn-success mb-2 float-right" @click="checkout">
                            <b-icon-cart></b-icon-cart>Pesan
                        </button>

                    </form>
                </div>
            </div>
        </div>

        <!--end breadcumb-->

    </div>
</template>

<script>
    import Navbar from '@/components/Navbar.vue'
    import axios from 'axios'
    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Keranjang',
        components: {
            Navbar,
        },
        data() {
            return {
                keranjang: [], //untuk menghubungkan dengen model
                pesan: {}
            }
        },
        methods: {
            setKeranjang(data) {
                this.keranjang = data;
            },
            hapusKeranjang(id) {
                axios
                    .delete("http://localhost:3000/keranjang/" + id) //
                    .then(() => {
                        this.$toast.error('Pesanan Berhasil Di Hapus!', {
                            type: 'error',
                            position: 'top-right',
                            duration: 3000,
                            dismissible: true
                        });
                        //update data keranjang
                        axios
                            .get("http://localhost:3000/keranjang") //
                            .then((response) => this.setKeranjang(response.data))
                            .catch((error) => console.log("Gagal", error))
                    })

                    .catch((error) => console.log("Gagal", error))
            },
            checkout() {
                if (this.pesan.nama && this.pesan.noMeja) {

                    this.pesan.keranjang = this.keranjang;

                    axios
                        .post("http://localhost:3000/pesanan", this.pesan)
                        .then(() => {
                            this.keranjang.map(function(item){
                                return axios
                    .delete("http://localhost:3000/keranjang/" + item.id) //hapus semua keranjang setelah selesai melakukan checkout
                    .catch((error) => console.log("Gagal", error))
                                
                            })
                            this.$router.push({
                                path: "/pesanan-sukses"
                            }) //untuk mengarahkan ke halaman keranjang
                            // eslint-disable-next-line no-undef
                            this.$toast.success('Berhasil di Pesan! ', { //dari vue toast notification 
                                type: 'success',
                                position: 'top-right',
                                duration: 3000,
                                dismissible: true
                            });
                        })
                        
                        .catch((error) => console.log("gagal", error))

                            } else {
                                this.$toast.error('Nama dan No.Meja Harus di isi!!', {
                                    type: 'error',
                                    position: 'top-right',
                                    duration: 3000,
                                    dismissible: true
                                });
                            }
                        }
                },
                mounted() {
                        axios
                            .get("http://localhost:3000/keranjang") //
                            .then((response) => this.setKeranjang(response.data))
                            .catch((error) => console.log("Gagal", error))
                    },
                    computed: {
                        totalHarga() {
                            return this.keranjang.reduce(function (items, data) {
                                return items + (data.products.harga * data.jumlah_pemesanan)
                            }, 0)
                        }
                    }

            }
</script>

<style>

</style>
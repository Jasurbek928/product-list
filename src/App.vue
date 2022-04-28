<template>
  <div id="app">
    <h3>Products</h3>
    <div class="card">
      <div class="container product_list">Add a new project</div>
     <div class="input-section d-flex m-auto p-4 m-4">
        ID <input class="form-control" type="text" v-model="id">
        Name <input class="form-control" type="text" v-model="name">
        Price <input class="form-control" type="text" v-model="price">
        <button @click="add" class="btn btn-primary ">Add</button>
     </div>

    </div>
    <div class="container product_list">Product list</div>
     <table class="container ">
      <thead>
        <tr>
          <th>Product ID</th>
          <th>Product Name</th>
          <th>Product Price</th>
          <th>Action</th>
        </tr>
      </thead>
  <tbody class="table-hover">
    <tr v-for="(product,id) in products " :key="id">
      <th>{{product.id}}</th>
      <td>{{product.name}}</td>
      <td>{{product.price}}</td>
      <td>
        <a href="#"><img @click="del(id)" src="./assets/icon/icons8-delete-24.png" alt=""></a>
        <a href="#"><img @click="update(id)" src="./assets/icon/icons8-edit-24.png" alt=""></a>
        <a href="#"><img @click="Modal" src="./assets/icon/icons8-eye-24.png" alt=""></a>
      </td>
    </tr>
  </tbody>
    </table>
    <Modal v-if="showModal"/>

  </div>
</template>

<script>
import Modal from "./components/modal.vue";
export default {
  name: "App",
  components: {
    Modal,
  },
  data() {
    return {
      products: [],
      id: "",
      name: "",
      price: "",
      showModal: false,
    };
  },
  methods: {
    add() {
      if (this.id == "" || this.name == "" || this.price == "") {
        alert("Please fill all the fields");
      } else {
        this.products.push({
          id: this.id,
          name: this.name,
          price: this.price,
        });
        this.id = "";
        this.name = "";
        this.price = "";
      }
    },
    del(id) {
      this.products.splice(id, 1);
    },
    update(id) {
      this.id = this.products[id].id;
      this.name = this.products[id].name;
      this.price = this.products[id].price;
    },
    Modal() {
      this.showModal = !this.showModal;
    },
  },
};
</script>

<style>
h3 {
  font-family: "Gilroy-Bold", sans-serif;
  margin: auto;
  display: flex;
  width: 147px;
  height: 44px;
  font-weight: 700;
  font-size: 36px;
}
thead th {
  border-bottom: 1px solid #e0e0e0;
}
input {
  width: 147px;
  height: 33px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-family: "Gilroy-Regular", sans-serif;
  font-size: 16px;
  margin: 0 20px;
}
.product_list {
  height: 62px;
  margin-top: 40px;
  margin-bottom: 20px;
  font-family: "Gilroy-Regular", sans-serif;
  font-size: 16px;
  border-radius: 4px;
  padding: 10px;
  color: #000;
  background-color: rgba(22, 114, 213, 0.03);
  line-height: 40px;
}
table a {
  font-family: "Gilroy-Regular", sans-serif;
  margin: 0 20px;
  outline: none;
  cursor: pointer;
}
a img {
  width: 20px;
}
table tr td:last-child {
  white-space: nowrap;
}
table th,
td {
  text-align: left;
}
</style>

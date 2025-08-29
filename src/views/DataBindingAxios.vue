<template>
  <div>
    <strong>{{ msg }}</strong>
  </div>

  <table border="1" class="add">
    <tr>
      <th>상품명</th>
      <td><input type="text" v-model="prod_name" /></td>
    </tr>
    <tr>
      <th>가격</th>
      <td><input type="number" v-model.number="prod_price" /></td>
    </tr>
    <tr>
      <button v-on:click="registerProd">등록</button>
    </tr>
  </table>

  <table border="1" class="list">
    <thead>
      <tr>
        <th>상품번호</th>
        <th>상품명</th>
        <th>가격</th>
        <th>카테고리</th>
      </tr>
    </thead>
    <tbody>
      <tr v-bind:key="i" v-for="(prod, i) in prodList">
        <td>{{ prod.id }}</td>
        <td>{{ prod.product_name }}</td>
        <td>{{ prod.product_price }}</td>
        <td>{{ prod.category1 }}/{{ prod.category2 }}/{{ prod.category3 }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      msg: "Axios 수업",
      prod_name: "",
      prod_price: 0,
      prodList: [],
    };
  },
  methods: {
    async getProdList() {
      let response = await axios.post(
        "http://localhost:3000/api/productList",
        []
      );
      return response.data; // Promise로 변환 (axios가..)
    },
    async registerProd() {
      let product = {
        product_name: this.prod_name,
        product_price: this.prod_price,
        seller_id: 1,
        category_id: 1,
      };
      let response = await axios.post(
        "http://localhost:3000/api/productInsert",
        { param: [product] }
      ); //
      response = await this.getProdList();
      console.log(response);
      this.prodList = response;
    },
  },
  mounted() {
    // this.prodList = this.getProdList();
    // console.log(this.prodList);

    this.getProdList() //
      .then((list) => {
        this.prodList = list;
      });
  },
};
</script>

<style>
table.add {
  margin: 0 auto;
  text-align: center;
  margin-bottom: 10px;
  margin-top: 10px;
}

table.list {
  margin: 0 auto;
  text-align: center;
}
</style>

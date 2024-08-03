<template>
  <h1>老頂了</h1>
  <div>
    <h1>2024 vue week1</h1>
    <table>
      <thead>
        <tr>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col">價格</th>
          <th scope="col">庫存</th>
          <th scope="col">編輯</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">
          <td>{{ product.name }}</td>
          <td><small>{{ product.description }}</small></td>
          <td>{{ product.price }}</td>
          <td v-if="edit2">
            <button type="button" @click="subStock(product)" :style="{ opacity: product.stock == 0 ? '0.4' : '1' }">-</button>{{
              product.stock }}
            <button type="button" @click="addStock(product)">+</button>
          </td>
          <td>
            <button type="button" @click="editProduct(product)">修改品項</button>
          </td>
        </tr>
      </tbody>
      <br>

    </table>

    <div class=" row" v-if="edit">
      <h1>編輯品項</h1>
      <div>
        <div class="col-12">
          <label class="mx-2" for="name">品項名稱</label>
          <input type="text" id="name" class="my-2" v-model="tempProduct.name">
        </div>
        <div class="col-12"><label class="mx-2" for="description">描述</label>
          <input type="text" id="description" class="my-2" v-model="tempProduct.description">
        </div>
        <div class="col-12"><label class="mx-2" for="price">價格</label>
          <input type="number" id="price" class="my-2" v-model="tempProduct.price">
        </div>
        <div class="col-12"><label class="mx-2" for="stock">庫存</label>
          <input type="number" id="stock" class="my-2" v-model="tempProduct.stock">
        </div>
        <button type="button" @click="updateProduct(tempProduct)"> 確認 </button>
        <button type="button" @click="canel(tempProduct)"> 取消 </button>
      </div>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue';

const products = ref([
  {
    id: 1,
    name: "珍珠奶茶",
    description: "香濃奶茶搭配QQ珍珠",
    price: 50,
    stock: 20
  },
  {
    id: 2,
    name: "冬瓜檸檬",
    description: "清新冬瓜配上新鮮檸檬",
    price: 45,
    stock: 18
  },
  {
    id: 3,
    name: "翡翠檸檬",
    description: "綠茶與檸檬的完美結合",
    price: 55,
    stock: 34
  },
  {
    id: 4,
    name: "四季春茶",
    description: "香醇四季春茶，回甘無比",
    price: 45,
    stock: 10
  },
  {
    id: 5,
    name: "阿薩姆奶茶",
    description: "阿薩姆紅茶搭配香醇鮮奶",
    price: 50,
    stock: 25
  },
  {
    id: 6,
    name: "檸檬冰茶",
    description: "檸檬與冰茶的清新組合",
    price: 45,
    stock: 20
  },
  {
    id: 7,
    name: "芒果綠茶",
    description: "芒果與綠茶的獨特風味",
    price: 55,
    stock: 18
  },
  {
    id: 8,
    name: "抹茶拿鐵",
    description: "抹茶與鮮奶的絕配",
    price: 60,
    stock: 20
  },
]);
const tempProduct = ref({})
let edit = ref(false)
let edit2 = ref(true)
const addStock = (product) => {
  product.stock++;
}
const subStock = (product) => {
  if (product.stock > 0) {
    product.stock--;
  }

}
const editProduct = (product) => {
  edit.value = true
  edit2.value = false
  tempProduct.value = { ...product };
  // console.table(tempProduct.value);
}

const updateProduct = (product) => {
  edit.value = false
  edit2.value = true
  products.value = products.value.map((p) => {
    if (p.id === product.id) {
      return product
    }
    return p
  })
}

const canel = (products) => {
  edit.value = false
  edit2.value = true
  return products;

}

</script>
<style scoped></style>

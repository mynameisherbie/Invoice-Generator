<template>
  <div>
    <h1>VonderLinden Farms Invoice Form</h1>

    <p>Shipping Information:</p>
    <form>
      <label for="fname">First name:</label>
      <input type="text" id="fname" name="fname" v-model="first_name" />
      <label for="lname">Last name:</label>
      <input type="text" id="lname" name="lname" v-model="last_name" /><br />
      <label for="street">Street:</label>
      <input type="text" id="street" name="street" v-model="address" /><br />
      <label for="appt">Appt #:</label>
      <input type="text" id="appt" name="appt" v-model="address2" /><br />
      <label for="city">City:</label>
      <input type="text" id="city" name="city" v-model="city" />
      <label for="state">State:</label>
      <input type="text" id="state" name="state" v-model="state" />
      <label for="zip">Zip:</label>
      <input type="text" id="zip" name="zip" v-model="zip" /><br /><br />
      <label for="payment">Payment Type:</label>
      <input type="text" id="payment" name="payment" v-model="payment_type" /><br />
      <br />
      Product Type:
      <select name="type" id="type" v-model="product_type">
        <option :value="null">Select product type</option>
        <option
          v-for="productType in productTypes"
          :value="productType.id"
          :key="productType.id"
        >
          {{ productType.name }}
        </option>
      </select>
      <br />
      Product:
      <select name="product" id="product" v-model="product">
        <option :value="null">Select product</option>
        <option
          v-for="product in products"
          :value="product.id"
          :key="product.id"
        >
          {{ product.name }}
        </option>
      </select>
      <br />
      Quantity:
      <select name="quantity" id="quantity" v-model="product_quantity">
        <option :value="null">Quantity</option>
        <option
          v-for="quantity in quantities"
          :value="quantity"
          :key="quantity"
        >
          {{ quantity }}
        </option>
      </select>
      <br /><br />
      Subtotal: {{subTotal}}
      <!-- <input type="text" id="subtotal" v-model="subtotal"> -->
      <br /><br />
      Total: {{total}}
      <!-- <input type="text" id="total" name="total" v-model="total"> -->
    </form>
  </div>
</template>

<script>
export default {
  name: "InvoiceForm",
  data() {
    return {
      first_name: null,
      last_name: null,
      address: null,
      address2: null,
      city: null,
      state: null,
      zip: null,
      payment_type: null,
      product: null,
      product_type: null,
      product_quantity: null,

      product_types: [
        {
          id: 1,
          name: "10cc Liquid Culture Syringe",
          products: [
            {
              id: 1,
              name: "Blue Oyster(Commercial)",
              quantities: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
              price: 25.00,
            },
            {
              id: 2,
              name: "Golden Oyster",
              quantities: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
              price: 15.00,
            },
            {
              id: 3,
              name: "Pink Oyster",
              quantities: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
              price: 15.00,
            },
          ],
        },
        {
          id: 2,
          name: "Modified Mason Jar Lids",
          products: [
            {
              id: 4,
              name: "Wide Mouth LC Lid",
              quantities: [6, 12],
              price: 7.00,
            },
            {
              id: 5,
              name: "Normal Mouth LC Lid",
              quantities: [6, 12],
              price: 6.00,
            },
            {
              id: 6,
              name: "Wide Mouth Grain Spawn Lid",
              quantities: [6, 12],
              price: 7.00,
            },
            {
              id: 7,
              name: "Normal Mouth Grain Spawn Lid",
              quantities: [6, 12],
              price: 7.00,
            },
          ],
        },
        {
          id: 3,
          name: "Pre-poured Agar Plates",
          products: [
            {
              id: 8,
              name: "Malt Extract Agar",
              quantities: [10, 25],
              price: 2.50,
            },
            {
              id: 9,
              name: "Potato Flake Agar",
              quantities: [10, 25],
              price: 2.50,
            },
            {
              id: 10,
              name: "Oatmeal Agar",
              quantities: [10, 25],
              price: 2.50,
            },
          ],
        },
      ],
    };
  },
  computed: {
      productTypes(){return this.product_types},
      products(){
          let filteredProducts = this.productTypes.filter( item => item.id == this.product_type)
          if(filteredProducts.length == 1){
            return filteredProducts[0].products
          }
          return []
      },
       quantities(){
          let filteredProduct = this.products.filter( item => item.id == this.product)
          if(filteredProduct.length == 1){
            return filteredProduct[0].quantities
          }
          return []
      },
      currentProduct(){
        return this.products.filter(item => this.product == item.id)[0]
      },
      total(){return 0},
      subTotal(){
        if(!this.product) return 0;
        let price = this.currentProduct.price
        let quantity = this.product_quantity ?? 0
        return price * quantity
      }
  }
};
</script>

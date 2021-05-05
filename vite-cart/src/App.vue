<template>
  <main>
    <header>
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container-fluid">
          <a class="navbar-brand" href="/"><i class="fas fa-gem"></i> 賺很大商店</a>
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav">
              <li class="nav-item">
                <a class="nav-link active" aria-current="page" href="#">商品</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="#">當日特價</a>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>

    <section class="container mt-4">
      <div class="items row">

        <div class="col-sm-2" v-for="(item, idx) in itemList" >

          <div class="card" :data-product-id="item.id">

            <img :src="`images/${item.cover}`" class="card-img-top" alt="">
            
            <div class="card-body">
              <h5 class="card-title fs-6 fw-light">{{ item.name }}</h5>
              <p class="price"> NT${{ item.price }}</p>
              <button class="btn btn-sm btn-warning fw-light"><i class="fas fa-cat"></i></button>
            </div>
          </div>
        </div>
      </div>
      <hr>
      <pre>{{item}}</pre>
      <section class="cart">
        <h2>購物車</h2>
        <table class="table cart-item-table">
          <thead>
            <tr>
              <th scope="col">項目</th>
              <th scope="col">數量</th>
              <th scope="col">單價</th>
              <th scope="col">小計</th>
              <th scope="col"></th>
            </tr>
          </thead>
          <tbody>
          <!-- <tr>
            <td>{{ item.name }}</td>
            <td> <input type="number" class="quantity" min= "1" value= "1"> </td>
            <td> NT${{item.price}}</td>
            <td> NT${{item.price}}</td>
            <td>
              <button class="remove-item-btn btn btn-danger btn-sm">
                <i class="fas fa-trash-alt"></i></button>
            </td>
          </tr> -->
          </tbody>
          <tfoot>
            <tr>
              <td colspan="2"></td>
              <td>總價</td>
              <td><span class="total-price">$0</span></td>
              <td></td>
            </tr>
          </tfoot>
        </table>
        <button class="btn btn-lg btn-success empty-cart"><i class="fas fa-baby-carriage"></i> 清空購物車</button>
      </section>
    </section>
  </main>
</template>

<script>
import { ref } from 'vue'; 

export default {
    setup() {
    const itemList = ref([ ]); 
    const cart = ref([]);
    const addCart = item => { 
      const idx = cart.value.findIndex(d => item.d === d.id); 
      if ( idx > -1 ) {
        cart.value[idx].qty++; 
      }
      else{
        cart.value.push({
          ...item,
          qty: 1
        }); 

      }
    }; 

  //    const {ref, computed, createApp}

  // createApp({
  //   setup(){
  //     const names = ['Jack', 'John', 'Mike'];
  //     const checkedName = ref('');

  //     return {
  //       names,
  //       checkedName,
  //     }
  //   }


  // const {ref, computed, createApp}

  // createApp({
  //   setup(){
  //     const sum = 

  //   }
  // })


    fetch ("./item.json")
    .then ((response) => response.json()) 
    .then((d) => (itemList.value = d)); 

    return {
      itemList, 
      cart, 
      addCart
    }; 

    }
}
</script>

<template>
    <div>
      <div class="form-group">
        <input type="text" v-model="q" class="form-control" placeholder="Search on posts"><br><hr>
      </div>
        <table class="table">
          <thead>
            <tr>
              <th>ID</th>
              <th>CURRENT STATUS</th>
              <th>INFO</th>
            </tr>
          </thead>
          <tbody v-for="(order, index) in orders">
                <tr>
                  <td class="col-md-3">{{order.random}}</td>
                  <td>{{order.status}}</td>
                  <td>
                    <ul class="navbar-nav mr-auto mt-md-0">
                        <!-- This is  -->
                        <li class="nav-item"> <a class="nav-link nav-toggler hidden-md-up text-muted  " href="javascript:void(0)"><i class="mdi mdi-menu"></i></a> </li>
                        <li class="nav-item m-l-10"> <a class="nav-link sidebartoggler hidden-sm-down text-muted  " href="javascript:void(0)"><i class="ti-menu"></i></a> </li>
                        <!-- Messages -->
                        <li class="nav-item dropdown mega-dropdown"> <a class="nav-link dropdown-toggle text-muted  " href="#" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"><i class="fa fa-th-large"></i></a>
                            <div class="dropdown-menu animated zoomIn">
                                <ul class="mega-dropdown-menu row">
                                    <li class="col-lg-12 col-xlg-12 m-b-30">
                                      <h1>{{order.random}}</h1>
                                      <table class="table">
                                        <thead>
                                          <tr>
                                            <th>Title</th>
                                            <th>Image</th>
                                            <th>Quantity</th>
                                            <th>Price</th>
                                          </tr>
                                        </thead>
                                        <tbody  v-for="product in order.products">
                                          <tr>
                                            <td>{{product.title}}</td>
                                            <td>{{product.featureimage.featureimage}}</td>
                                            <td>{{product.pivot.quantity}}</td>
                                            <td>{{product.price}}</td>
                                          </tr>
                                        </tbody>
                                      </table>
                                    </li>
                                </ul>
                            </div>
                        </li>
                      </ul>
                  </td>
                </tr>
          </tbody>
        </table>
    </div>
</template>

<script>

import Toaster from 'v-toaster'
import 'v-toaster/dist/v-toaster.css'

Vue.use(Toaster, {timeout: 10000})

export default {

  props: ['results'],
    data() {
        return {
            q: '',
            orders: this.results,
            updates:null,
            order_id:null,
            status: 'sent',
        };
    },


    watch: {
        q(after, before) {
            this.fetch();
        }
    },

    methods: {
        fetch() {
            axios.get('/admin/orders/sent', { params: {q: this.q } })
                  .then((res) => {
                  this.orders = res.data.orders
                  })
                .catch(error => {});
        },
    }
}

</script>

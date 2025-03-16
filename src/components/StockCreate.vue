<template>
    <div class="container-fluid">
      <div class="row align-items-center justify-content-center">
        <div class="col col-12 col-sm-10 col-md-10 col-lg-6">
          <div class="card">
            <div class="card-header">Enter Stock Information</div>
            <div class="card-body">
              <form ref="form" v-on:submit.prevent="handleSubmit">
                <div class="container-fluid">
                  <div class="row justify-content-around py-2">
                    <label class="col-4">Customer</label>
                    <div class="col col-8">
                      <select v-model="stock.customer" class="form-select form-select-sm">
                        <option v-for="customer in customers" :value="customer.id" :key="customer.id">
                          {{ customer.cust_number }} - {{ customer.name }}
                        </option>
                      </select>
                    </div>
                  </div>
                  <div class="form-group row justify-content-around py-2">
                    <label class="col-4">Symbol</label>
                    <div class="col col-8">
                      <input v-model="stock.symbol" type="text" class="form-control form-control-sm" />
                    </div>
                  </div>
                  <div class="form-group row justify-content-around py-2">
                    <label class="col-4">Name</label>
                    <div class="col col-8">
                      <input v-model="stock.name" type="text" class="form-control form-control-sm" />
                    </div>
                  </div>
                  <div class="form-group row justify-content-around py-2">
                    <label class="col-4">Shares</label>
                    <div class="col col-8">
                      <input v-model="stock.shares" type="number" step="0.1" class="form-control form-control-sm" />
                    </div>
                  </div>
                  <div class="form-group row justify-content-around py-2">
                    <label class="col-4">Purchase Price</label>
                    <div class="col col-8">
                      <input v-model="stock.purchase_price" type="number" step="0.01" class="form-control form-control-sm" />
                    </div>
                  </div>
                  <div class="form-group row justify-content-around py-2">
                    <label class="col-4">Purchase Date</label>
                    <div class="col col-8">
                      <input v-model="stock.purchase_date" type="date" class="form-control form-control-sm" />
                    </div>
                  </div>
                  <button type="submit" class="btn btn-primary">Submit</button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        stock: {
          customer: null,
          symbol: '',
          name: '',
          shares: 0,
          purchase_price: 0,
          purchase_date: new Date().toISOString().slice(0, 10), // Default to today's date
        },
        customers: [], // Will be populated with customer data
      };
    },
    mounted() {
      // Fetch customer data from your API here
      this.fetchCustomers();
    },
    methods: {
      async fetchCustomers() {
        // Replace with your API endpoint to fetch customers
        try {
          const response = await fetch('/api/customers/'); // Example API endpoint
          this.customers = await response.json();
        } catch (error) {
          console.error('Error fetching customers:', error);
        }
      },
      handleSubmit() {
        // Handle form submission logic here
        console.log(this.stock);
        // You would typically send this.stock data to your Django API
      },
    },
  };
  </script>
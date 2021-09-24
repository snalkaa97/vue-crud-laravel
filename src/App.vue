<template>
	<div id="app">
		<div class="container">
			<h1 class="mb-4">Daftar Pelanggan</h1>
			<hr />
			<p>
				<button
					class="btn btn-primary"
					type="button"
					data-bs-toggle="collapse"
					data-bs-target="#collapseExample"
					aria-expanded="false"
					aria-controls="collapseExample"
				>
					Tambah Pelanggan
				</button>
			</p>
			<customer-table
				v-bind:customers="customers"
				@edit-customer="editCustomer"
				@delete-customer="deleteCustomer"
			/>

			<div class="collapse" id="collapseExample">
				<div class="card card-body">
					<h2>Input Data Pelanggan</h2>
					<hr />
					<customer-form @add-customer="addCustomer" />
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import axios from "axios";
import CustomerTable from "@/components/CustomerTable.vue";
import CustomerForm from "@/components/CustomerForm.vue";

export default {
	name: "App",
	components: {
		CustomerTable,
		CustomerForm,
	},
	data() {
		return {
			customers: [],
			// customers: [
			// 	{
			// 		id: 1,
			// 		name: "Bambang",
			// 		email: "bambang@mail.com",
			// 		address: "Jl.Kenanga",
			// 	},
			// 	{
			// 		id: 2,
			// 		name: "Dika",
			// 		email: "dika@mail.com",
			// 		address: "Jl.Mangga",
			// 	},
			// 	{
			// 		id: 3,
			// 		name: "Agus",
			// 		email: "agus@mail.com",
			// 		address: "Jl.Mataram",
			// 	},
			// ],
		};
	},
	created() {
		axios.get(`http://vue-laravel.local/api/customers`).then((response) => {
			this.customers = response.data.data;
		});
	},
	methods: {
		addCustomer(customer) {
			axios
				.post("http://vue-laravel.local/api/customers", customer)
				.then((response) => {
					console.log(response);
					this.customers = [...this.customers, response.data.data];
				});
		},

		editCustomer(id, data) {
			axios
				.put(`http://vue-laravel.local/api/customers/${id}`, data)
				.then((response) => {
					console.log(response.data.data);
					this.customers = this.customers.map((customer) =>
						customer.id === id ? data : customer
					);
				});
		},

		deleteCustomer(id) {
			axios.delete(`http://vue-laravel.local/api/customers/${id}`).then(() => {
				const customerId = this.customers.indexOf(id);
				this.customers.splice(customerId, 1);
			});
		},
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: left;
	color: #2c3e50;
	margin-top: 60px;
}
</style>

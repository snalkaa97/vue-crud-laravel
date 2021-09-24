<template>
	<table class="table">
		<thead class="thead-light">
			<tr>
				<th scope="col">Nama</th>
				<th scope="col">Email</th>
				<th scope="col">Alamat</th>
			</tr>
		</thead>
		<tbody>
			<tr v-for="customer in customers" :key="customer.id">
				<template v-if="customerId === customer.id">
					<td>
						<label for="name" class="font-weight-bold">Nama:</label>
						<div>
							<input type="text" v-model="customer.name" class="form-control" />
						</div>
					</td>
					<td>
						<label for="email" class="font-weight-bold">Email:</label>
						<div>
							<input
								type="text"
								v-model="customer.email"
								class="form-control"
							/>
						</div>
					</td>
					<td>
						<label for="address" class="font-weight-bold">Address:</label>
						<div>
							<input
								type="text"
								v-model="customer.address"
								class="form-control"
							/>
						</div>
					</td>
					<td>
						<button class="btn btn-success m-2" @click="saveEdit(customer)">
							Save
						</button>
						<button class="btn btn-danger" @click="cancelEdit(customer)">
							Cancel
						</button>
					</td>
				</template>
				<template v-else>
					<td>{{ customer.name }}</td>
					<td>{{ customer.email }}</td>
					<td>{{ customer.address }}</td>
					<td>
						<button class="btn btn-primary" @click="editCustomer(customer)">
							Edit
						</button>
						<button class="btn btn-danger" @click="deleteCustomer(customer.id)">
							Hapus
						</button>
					</td>
				</template>
			</tr>
		</tbody>
	</table>
</template>

<script>
export default {
	name: "customer-table",
	props: ["customers"],
	data() {
		return {
			customerId: null,
		};
	},
	methods: {
		editCustomer(customer) {
			this.data = customer;
			this.customerId = customer.id;
		},
		saveEdit(customer) {
			let id = this.data.id;
			this.$emit("edit-customer", id, customer); //ini ngirim 2 parameter yaitu id, dan customer
			this.customerId = null;
		},
		cancelEdit(customer) {
			Object.assign(customer, this.data);
			this.customerId = null;
			// console.log(this.customerId);
		},
		deleteCustomer(id) {
			this.$emit("delete-customer", id);
		},
	},
};
</script>

<style scoped></style>

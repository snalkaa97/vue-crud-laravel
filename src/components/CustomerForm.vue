<template>
	<div class="customer-form">
		<form @submit.prevent="submit">
			<div class="form-group">
				<label for="name">Nama</label>
				<input
					type="text"
					class="form-control"
					v-model="customer.name"
					placeholder="Masukan nama pelanggan"
				/>
			</div>
			<div class="form-group">
				<label for="email">Email</label>
				<input
					type="text"
					class="form-control"
					v-model="customer.email"
					placeholder="Masukan email pelanggan"
				/>
			</div>
			<div class="form-group">
				<label for="address">Alamat</label>
				<textarea
					type="text"
					class="form-control"
					v-model="customer.address"
					placeholder="Masukan alamat pelanggan"
				>
				</textarea>
			</div>
			<button type="submit" class="btn btn-primary">Submit</button>
		</form>
	</div>
</template>

<script>
export default {
	name: "customer-form",
	data() {
		return {
			customer: {
				name: "",
				email: "",
				address: "",
			},
		};
	},
	methods: {
		submit() {
			this.$emit("add-customer", this.customer); //ini satu parameter yaitu customer
			this.customer = {
				name: "",
				email: "",
				address: "",
			};
		},
	},
};
</script>

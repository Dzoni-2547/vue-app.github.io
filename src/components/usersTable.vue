<template>

	<div>
		<table class="table table-bordered">
			<thead>
				<tr>
					<th>ID</th>
					<th>Name</th>
					<th>Username</th>
					<th>Email</th>
					<th>Address</th>
					<th>Phone</th>
					<th>Website</th>
					<th>Company</th> 
				</tr>
			</thead>
			<tbody>
				<tr v-for="user in users" :key="user.id">
					<td>{{ user.id }}</td> 
					<td>{{ user.name }}</td>
					<td>{{ user.username }}</td>
					<td>{{ user.email }}</td>

					<td>
						<div class="row text-left" v-for="(address, key) in user.address" :key="key">
							<div class="col-md-4">
								{{ key = key[0].toUpperCase() + key.slice(1) }} 
							</div> 
							
							<div class="col-md-8">
								{{ address }}    
							</div>
						</div>  
					</td>

					<td>{{ user.phone }}</td>
					<td>{{ user.website }}</td>

					<td>
						<div class="row text-left" v-for="(company, key) in user.company" :key="key">
							<div class="col-md-5">
								{{ key = key[0].toUpperCase() + key.slice(1) }}
							</div> 
							<div class="col-md-7">
								{{ company }}  
							</div>  
						</div>  
					</td>
				</tr> 
			</tbody>
		</table>
	</div>

</template>

<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<script>    
// import resources from '../../resources.json'

export default {
	name: 'usersTable',
	data: function() {
		return {  
			users: [], 
		}
	},
	components: {},
	mounted () {
		axios
		.get('https://jsonplaceholder.typicode.com/users')
		.then(response => {
			this.users = response.data 
		})
		.catch(error => {
			console.log(error)
			this.errored = true
		})  
	}
}


</script>


<style scoped>



</style>

<template>
	<div id="app">
		<v-app>
			<v-main>
				<v-container fluid>
					<v-row>
						<v-col cols="6">
							<v-text-field v-model="search" prepend-inner-icon="mdi-magnify" label="Buscar..." outlined></v-text-field>
						</v-col>
					</v-row>
					<v-row>
						<v-col>
							<v-data-table :search="search" :headers="headers" :items="items" :loading="loading">
								<template v-slot:[`item.operaciones`]="{ item }">
								
								<v-row v-for="(el, key) in item.operaciones" :key="key">
									<v-col cols="12" v-for="(i, key) in el" :key="key">
										<strong>{{ key }}:</strong>
										<br>
										{{i }}
									</v-col>
								</v-row>

								</template>

								<template  v-slot:[`item.otorgantes`]="{ item }">
								
								<v-row v-for="(el, key) in item.otorgantes" :key="key">
									<v-col cols="12" v-for="(i, key) in el" :key="key">
										<strong>{{ key }}:</strong>
										<br>
										{{i }}
									</v-col>
								</v-row>

								</template>

								<template  v-slot:[`item.bienes`]="{ item }">
								
								<v-row v-for="(el, key) in item.bienes" :key="key">
									<v-col cols="12" v-for="(i, key) in el" :key="key">
										<strong>{{ key }}:</strong>
										<br>
										{{i }}
									</v-col>
								</v-row>

								</template>
							</v-data-table>
						</v-col>
					</v-row>
				</v-container>
			
			</v-main>
		</v-app>
	</div>
</template>

<script>


export default {
	name: 'App',
	data(){
		return{
		items: [],
		loading: false,
		headers: [],
		search: null
		}
	},
	methods: {
		obtener_datos(){

			this.loading = true 

			fetch("data.json")
			.then(res => res.json())
			.then(data => {

				this.items = data
				this.loading = false

				const keys = Object.keys(data[0]);

				keys.forEach(key => {
					
					let element = {
						text: key,
						value: key
					}

					this.headers.push(element)

				});

			})

		
		}
	},
	created(){

		this.obtener_datos()

	}
}
</script>

<template>
	<div>
		<div class="additem">
			<input type="text" v-model="item.nama"/>
			<font-awesome-icon
			icon="plus-square"
			@click="additem()"
			:class="[ item.nama ? 'active' : 'inactive', 'plus']"
			/>
		</div>
	</div>
</template>

<script>
	export default{
		data: function() {
			return{
				item:{
					nama: ""
				}
			}
		},
		methods:{
			additem(){
				if (this.item.nama == '') {
					return;
				}
				axios.post('api/item/store', {
					item: this.item
				})
				.then( response => {
					if ( response.status == 201) {
						this.item.nama = "";
						this.$emit('reloadlist');
					}
				})
				.catch( error => {
					console.log(error);
				})
			}
		}
	};
</script>

<style scoped>
	.addItem{
		display: flex;
		justify-content: center;
		align-items: center;
	}
	input{
		background: #f7f7f7;
		border: 0px;
		outline: none;
		padding: 5px;
		margin-right: 10px;
		width: 100%;
		box-sizing: border-box;
	}
	.active{
		color: #00ce25;
	}
	.inactive{
		color: #9999;
	}
</style>
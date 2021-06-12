<template>
	<div class="relative h-10 m-1">
		<div style="border-top: 1px solid #e6e6e6" class="grid grid-cols-6">
			<input type="text"
			class="col-span-5 p-1 focus:ring-2 focus:ring-gray-300"
			style="border: 0px;" 
			v-model="message"
			@keyup.enter="sendMessage()"
			placeholder="Say something..."
			/>
			<button
			@click="sendMessage()"
			class="place-self-end hover:bg-blue-700 bg-gray-500 p-1 mt-1 rounded text-white">
			Send
			</button>
		</div>
	</div>
</template>
<script>
	import Input from '../../Jetstream/Input.vue'
	export default{
		props:['room'],
		data: function(){
			return{
				message: ''
			}
		},
		methods:{
			sendMessage(){
				if (this.message=='') {
					return;
				}
				axios.post('/chat/room/'+this.room.id+'/message',{
					message: this.message
				})
				.then(response=>{
					if (response.status==201) {
						this.message='';
						this.$emit('messagesent');
					}
				})
				.catch(error=>{
					console.log(error);
				})
			}
		}
	}
</script>
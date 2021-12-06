<template>
    <label class="hover-input">                                            		
        <p class="hover-input__title" v-bind:class="{ '-keyIn': input_focus }" >{{title}}</p>		        
        <input 			
			:name="title" 
            class="hover-input__keyIn" 
            type="hover-input__keyIn" 
            :placeholder="placeholder"
            @focus="input_focus = true"
            @blur="input_focus = false"
			v-model="inputVal"
			>
        <div class="hover-input-line-box">
            <div class="hover-input-line-box__line"></div>
        </div>			        
    </label>  
</template>

<script>
export default {
	props: [
		'value','title',"placeholder",		
	],
	computed: {
		inputVal: {
			get() {
				return this.value;
			},
			set(val) {
				this.$emit('input', val);
			}
		}
	},
	data() {
		return  {
			
			input_focus:false
		}
	}

};
</script>
<style lang="scss" scoped>

	select {
		background-color: white !important;
		border: 0px solid #f8f8f8 !important;
	}
	
	
</style>


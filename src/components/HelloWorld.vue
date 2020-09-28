<template>
  <div>
		<div class="messages">
			<div class="card">
			<strong>NAME</strong>
			<p class="message">asdlkadlaksdl</p>
		</div>
		</div>

		<input type="text" name="nickname">
		<textarea name="area-message" id="textarea-message" cols="30" rows="10"></textarea>
	</div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

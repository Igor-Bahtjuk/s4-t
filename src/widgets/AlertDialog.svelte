<script lang="ts">
	let resolveFunction: (value: string) => void; 

	let showModal      = false;
	var alertTitle:string     = "Are you sure?"
	var alertMessage:string   = "This is a default message";
	var positiveTitle         = "OK";
	var negativeTitle         = "";
	var callback:Function|null;


	export async function open(title:string, message:string, positive:string = "OK", negative:string = "", mCallback:Function|null = null ):Promise<string>{
		alertTitle    = title;
		alertMessage  = message;
		positiveTitle = positive;
		negativeTitle = negative;
		callback      = mCallback;
		showModal     = true;
		document.body.style.overflowY = "hidden";

		return new Promise((resolve) => {
			resolveFunction = resolve; 
		});
	}
	function _reset(){
		showModal      = false;
		alertTitle     = "";
		alertMessage   = "";
		document.body.style.overflowY = "auto";
	}
	function onNegative() {
		if (callback !=null)callback(false);
		resolveFunction('no'); 
		_reset();
	}
	function onPositive() {
		if (callback !=null)callback(true);
		resolveFunction('yes');
		_reset();
	}

</script>
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <!-- svelte-ignore a11y-no-static-element-interactions -->
   {#if showModal}
   <div class="parent" on:click|stopPropagation>
	<div class="content">
		<span class="title">{alertTitle}</span>
		<span class="message">{alertMessage}</span>
		<div  class="button-container">
			 {#if negativeTitle.trim().length>0}
			 <button on:click={onNegative} class="button-negative alert-button">{negativeTitle}</button>
			 {/if}
			<button on:click={onPositive} class="button-positive alert-button">{positiveTitle}</button>
		</div>
	</div>
  </div>
   {/if}

<style>
	.parent{
		position: fixed;
		display: flex;
		top: 0px;
		bottom: 0px;
		left: 0px;
		right: 0px;
		background: rgba(0, 0, 0, 0.404);
		z-index: 1000;
		align-items: center;
		justify-content: center;
		overflow: hidden;
		pointer-events: all;
		animation: fade 0.2s ease-out;
	}
	.content{
		position: relative;
		display: flex;
		flex-direction: column;
		border-radius: 5px;
		width: 450px;
		z-index: 1001;
		background: white;
		overflow: hidden;
		animation: zoom 0.3s cubic-bezier(0.34, 2.56, 0.64, 1);
		box-shadow: rgba(0, 0, 0, 0.19) 0px 10px 20px, rgba(0, 0, 0, 0.23) 0px 6px 6px;
	}
	.title{
		align-self: flex-start;
		padding: 0px 15px;
		padding-top: 15px;
		padding-bottom: 5px;
		font-size: 21px;
		font-weight: 500;
	}
	.message{
		padding: 0px 15px;
		font-size: 14px;
	}
	.button-container{
		gap: 10px;
		display: flex;
		flex: 1;
		align-items: flex-end;
		justify-content: flex-end;
		min-height: 55px;
		padding-top: 15px;
		padding-right: 15px;
		padding-bottom: 15px;
	}
	.alert-button{
		padding: 12px 20px;
		border-radius: 10px;
		outline: none;
		border: none;
		border-radius: 5px;
		min-width: 80px;
		cursor: pointer;
		font-size: 15px;
		font-weight: 500;
	}
	.button-negative{
		background-color: #fff;
		color: #212121;
		border: solid rgb(221, 221, 221) 1px;

	}
	.button-positive{
		background-color: #212121;
		color: white;
		cursor: pointer;
	}


	@keyframes zoom {
		from {
			transform: scale(0.95);
		}
		to {
			transform: scale(1);
		}
	}

	@keyframes fade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}
	@media only screen and (max-width: 500px) {
      .content{
		width: calc(100% - 30px);
      }
    }
</style>

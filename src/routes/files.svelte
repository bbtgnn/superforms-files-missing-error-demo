<script lang="ts">
	export let files: File[] = [];

	let fileList: FileList;

	$: if (fileList) {
		files = Array.from(fileList);
	}
</script>

<div>
	<input type="file" bind:files={fileList} multiple />
	<div>
		{#each files as file}
			<div class="file">
				<p>{file.name}</p>
				<p>{file.size}</p>
				<p>{file.type}</p>
			</div>
		{/each}
	</div>
</div>

<style>
	input[type='file'] {
		margin-bottom: 12px;
	}

	.file {
		padding: 8px;
		margin-bottom: 12px;
		background-color: lightblue;
	}
</style>

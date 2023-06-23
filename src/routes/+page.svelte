<script lang="ts">
	import { z } from 'zod';
	import { superForm, superValidateSync } from 'sveltekit-superforms/client';
	import Files from './files.svelte';

	const maxSize = 1024 * 1024 * 0.5;
	const mimeTypes = ['image/png'];

	const fileSchema = z
		.custom<File>((f) => f instanceof File, 'NOT_A_FILE')
		.refine((f) => f.size < maxSize, 'FILE_SIZE_TOO_BIG')
		.refine((f) => mimeTypes.includes(f.type), `FILE_TYPE_NOT_ALLOWED`);

	const filesSchema = z.array(fileSchema);

	const formSchema = z.object({
		files: filesSchema
	});

	const supervalidate = superValidateSync(undefined, formSchema, { errors: false });
	const superform = superForm(supervalidate, {
		SPA: true,
		applyAction: false,
		scrollToError: 'smooth',
		validators: formSchema,
		onUpdate: async (input) => {
			try {
				console.log(input);
			} catch (e) {
				console.log(e);
			}
		}
	});

	const { form, errors, enhance } = superform;

	$: if ($form.files.length) {
		console.log('------- Superforms error -------');
		console.log($errors.files);

		console.log('\n');

		console.log('------- Zod error -------');
		try {
			filesSchema.parse($form.files);
			console.log('valid');
		} catch (e) {
			console.log(e);
		}

		console.log('\n\n\n\n');
	}
</script>

<form use:enhance method="POST">
	<Files bind:files={$form.files} />
</form>

<style>
	form {
		padding: 12px;
	}
</style>

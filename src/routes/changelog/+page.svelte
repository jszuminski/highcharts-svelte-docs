<script lang="ts">
    import { marked } from 'marked';
    import DOMPurify from 'dompurify';
	import { onMount } from 'svelte';
    import { PUBLIC_CHANGELOG_URL } from '$env/static/public';

    let loading = false;
    let docs = '';

    onMount(async () => {
        loading = true;
        try {
            const response = await fetch(PUBLIC_CHANGELOG_URL);
            docs = DOMPurify.sanitize(await marked(await response.text()));
        } catch (e) {
            docs = 'Error loading changelog.';
        } finally {
            loading = false;
        }
    });
</script>

<article id="docs" class="markdown-body">
    {@html docs}
</article>

<script context="module" lang="ts">
	import type { IAya } from '$contract/surah';

	import type { Load } from '@sveltejs/kit';
	let surah: IAya[];

	const getSurah = async (source, surah_id) => {
		surah = (await import(`../../../db/${source}/surah/${surah_id}.json`)).default;
	};

	export const load: Load = async ({ page, fetch, session }) => {
		await getSurah(page.params.source, page.params.surah_id);
		return {
			status: 200,
			props: {
				surah
			}
		};
	};
</script>

{#each surah as aya}
	<div class="font-arab" style="direction: rtl;">
		{aya.aya_text}
	</div>
{/each}

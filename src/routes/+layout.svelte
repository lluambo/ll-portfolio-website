<!--
Quick GitHub push steps:
1) cd /path/to/project
2) git init
3) git add .
4) git commit -m "Initial commit"
5a) git remote add origin git@github.com:USERNAME/REPO.git
    git branch -M main
    git push -u origin main
5b) OR using GitHub CLI:
    gh repo create USER/REPO --public --source=. --remote=origin --push
-->
<script>
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
{@render children()}

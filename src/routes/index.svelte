<script>
	import { HighlightAuto, HighlightSvelte } from 'svelte-highlight';

	const heroExample = `<script>
    import { query, graphql } from '$houdini'

    const { data } = query(graphql\`
        query AllTodoItems {
            items {
                text
            }
        }
    \`)
<\/script>

{#each $data.items as item}
    <div>{item.text}</div>
{/each}
`;

	const sellingPoints = [
		{
			header: 'Composable',
			text: 'Your components can define what data they need to do their job by and you can mix them together however you want.',
			example: `<script>
    import { query, graphql } from '$houdini'
    import { UserAvatar } from '~/components'

    const { data } = query(graphql\`
        query AllUsers {
            users {
                ...UserAvatar
            }
        }
    \`)
<\/script>

{#each $data.users as user}
    <UserAvatar {user} />
{/each}`
		},
		{
			header: 'Declarative',
			text: 'Updates to your application cache are made with a set of declarative fragments that the avoids surgical logic necessary to keep your application up to date.',
			example: `<script>
    import { mutation, graphql } from '$houdini'

    const createProject = mutation(graphql\`
            mutation CreateProject {
                createProject(name: "houdini") {
                    project { 
                        ...All_Projects_insert
                    } 
                }
            }
    \`)
<\/script>

<button onClick={createProject} />`
		},
		{
			header: 'Type Safe',
			text: 'Generate TypeScript definitions for every document in your application.',
			example: `<script lang="ts">
    import { query, graphql } from '$houdini'
    import type { AllTodoItems } from '$houdini'

    const { data } = query<AllTodoItems>(graphql\`
        query AllTodoItems {
            items {
                text
            }
        }
    \`)
<\/script>

{#each $data.items as item}
    <div>{item.text}</div>
{/each}
`
		}
	];
</script>

<svelte:head>
	<title>Houdini</title>
</svelte:head>

<a id="skip-nav" href="#main"> Skip to Content </a>

<header class="content">
	<a href="/">
		<img src="/static/images/logo.svg" alt="Houdini Logo" width="175px" />
	</a>
	<nav>
		<a href="/tour" class="nav-link">Get Started</a>
		<a href="/docs" class="nav-link">Docs</a>
		<a href="https://opencollective.com/houdini" class="nav-link" target="_blank"> Support </a>
		<a href="https://www.github.com/AlecAivazis/houdini" target="_blank" id="gh-link">
			<img src="/static/images/github.svg" alt="Github" height="20px" />
		</a>
	</nav>
</header>
<main id="main">
	<section id="hero" class="content">
		<div>
			<h1>
				The disappearing <span id="graphql-text">GraphQL</span>
				client for <span class="svelte-text">SvelteKit</span>.
			</h1>
			<nav id="hero-buttons">
				<a href="/tour" class="button-shadow" rel="prefetch">Get Started</a>
				<a href="/docs" class="button-shadow">Docs</a>
			</nav>
		</div>
		<HighlightSvelte code={heroExample} class="shadow" />
	</section>
	<section id="info">
		<div id="angle" />
		<article>
			<div id="showcase" class="content">
				{#each sellingPoints as point}
					<div class="showcase-item">
						<div class="showcase-text">
							<h2>{point.header}</h2>
							<p>
								{point.text}
							</p>
						</div>
						<pre class="showcase-example">
                        <HighlightAuto code={point.example} />
                    </pre>
					</div>
				{/each}
			</div>
		</article>
	</section>
</main>

<style>
	:global(body) {
		background-color: #f9fbff;
		display: flex;
		flex-direction: column;
	}

	:global(#hero pre) {
		width: 10px;
		flex-grow: 1;
		background: #161b22;
		border-radius: 32px;
		color: white;
		font-family: 'Roboto Mono', monospace;
	}

	:global(.shadow) {
		box-shadow: 10px 12px 25px 3px rgba(23, 40, 102, 0.25);
	}

	main {
		flex-grow: 1;
		display: flex;
		flex-direction: column;
	}

	#skip-nav {
		border: 0;
		clip: rect(0 0 0 0);
		height: 1px;
		width: 1px;
		margin: -1px;
		padding: 0;
		overflow: hidden;
		position: absolute;
	}

	#skip-nav:focus {
		padding: 1rem;
		position: fixed;
		top: 10px;
		left: 10px;
		background: white;
		z-index: 1;
		width: auto;
		height: auto;
		clip: auto;
	}

	header {
		height: 80px;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		padding: 10px 60px;
	}

	.nav-link {
		font-size: 16px;
		font-family: 'Roboto', sans-serif;
		color: #161b22;
		text-decoration: none;
		font-weight: bold;
	}

	.nav-link:hover {
		padding-bottom: 4px;
		border-bottom: 2px solid #ff3e00;
		margin-bottom: -6px;
	}

	nav {
		display: flex;
		flex-direction: row;
		align-items: center;
	}

	nav a {
		margin-left: 2rem;
	}

	.content {
		max-width: 1100px;
		margin: 0 auto;
		width: 100%;
	}

	#hero {
		display: flex;
		flex-direction: row;
		margin-top: 90px;
	}

	#hero div {
		width: 10px;
		flex-grow: 1;
		margin-top: 24px;
	}

	#hero h1 {
		flex-grow: 1;
		font-size: 3rem;
		margin-right: 4rem;
		font-family: 'Roboto', sans-serif;
		font-weight: bold;
		line-height: 4rem;
		color: #161b22;
	}

	#graphql-text {
		color: #e10098;
	}

	.svelte-text {
		color: #ff3e00;
	}

	.button-shadow {
		box-shadow: 1px 2px 25px 3px rgba(23, 40, 102, 0.1);
	}

	#info {
		display: flex;
		flex-direction: column;
		margin-top: 80px;
		flex-grow: 1;
	}

	#angle {
		width: 100%;
		height: 100px;
		background: #161b22;
		clip-path: polygon(-1% 101%, 100% 0%, 100% 101%);
	}

	article {
		flex-grow: 1;
		background: #161b22;
	}

	#hero-buttons {
		display: flex;
		flex-direction: row;
		margin-top: 40px;
	}

	#hero-buttons a {
		height: 35px;
		width: 150px;
	}

	#hero-buttons a {
		font-family: 'Roboto', sans;
		font-weight: 500;
		color: white;
		background-color: #ff3e00;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 13px;
		text-decoration: none;
	}

	#showcase {
		display: grid;
		width: 100%;
		margin-bottom: 100px;
	}

	.showcase-item {
		display: flex;
		flex-direction: row;
		margin-bottom: 100px;
	}

	h2 {
		font-family: 'Roboto', sans;
		color: white;
		font-size: 40px;
		margin-bottom: 16px;
	}

	p {
		font-family: 'Roboto', sans;
		color: white;
		font-size: 26px;
		line-height: 1.3;
		margin-right: 35px;
	}

	.showcase-text {
		width: 10px;
		flex-grow: 1;
		display: flex;
		flex-direction: column;
		justify-content: center;
		margin-right: 12px;
	}

	.showcase-example {
		width: 10px;
		flex-grow: 1;
		font-size: 18px;
		font-family: 'Roboto Mono', monospace;
	}
</style>
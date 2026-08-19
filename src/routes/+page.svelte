<script lang="ts">
	type SignupState = 'idle' | 'unconfigured';

	// Paste the action URL from MailerLite here when your form is ready.
	const newsletterEndpoint = '';

	let email = '';
	let signupState: SignupState = 'idle';
	const year = new Date().getFullYear();

	function handleSignup(event: SubmitEvent) {
		if (newsletterEndpoint) return;
		event.preventDefault();
		signupState = 'unconfigured';
	}
</script>

<svelte:head>
	<title>TinyWijk — Kleiner wonen, meer ruimte om te leven</title>
	<meta
		name="description"
		content="Een kleinschalig, parkachtig woonconcept in de Gentse rand en de Vlaamse Ardennen."
	/>
	<meta name="theme-color" content="#173c2d" />
</svelte:head>

<div class="page">
	<header>
		<a class="brand" href="/" aria-label="TinyWijk startpagina">
			<span class="mark" aria-hidden="true"><i></i><i></i><i></i></span>
			TinyWijk
		</a>
		<span class="status"><i></i> Project in haalbaarheidsfase</span>
	</header>

	<main>
		<section class="hero" aria-labelledby="title">
			<div class="visual" aria-hidden="true">
				<div class="visual-meta">
					<span>Concept 01</span>
					<span>Gentse rand · Vlaamse Ardennen</span>
				</div>

				<div class="home home-30"><div class="house"></div><b>30 m²</b></div>
				<div class="home home-45"><div class="house"></div><b>45 m²</b></div>
				<div class="home home-60"><div class="house"></div><b>60 m²</b></div>

				<div class="visual-footer">
					<span>Compact wonen</span>
					<span>Eigen buitenruimte</span>
					<span>Groen & privacy</span>
				</div>
			</div>

			<div class="content">
				<p class="eyebrow">Een nieuw woonconcept voor Vlaanderen</p>
				<h1 id="title">Kleiner wonen.<br /><em>Meer ruimte om te leven.</em></h1>

				<p class="intro">
					Een kleinschalige, parkachtige woonomgeving met compacte, volwaardige woningen in
					het groen. Het doel is permanente bewoning met een eigen buitenruimte, voldoende
					privacy, parking, vaste nutsvoorzieningen en een volwaardig adres.
				</p>

				<div class="facts" aria-label="Projectrichting">
					<div><strong>30–60 m²</strong><span>Woninggroottes in onderzoek</span></div>
					<div><strong>Gentse rand</strong><span>en de Vlaamse Ardennen</span></div>
					<div><strong>Vaste bewoning</strong><span>als uitgangspunt</span></div>
				</div>

				<div class="reality-check">
					<strong>Waar staan we nu?</strong>
					<p>
						Er ligt nog geen terrein vast en er zijn nog geen definitieve prijzen,
						vergunningen of startdatum. Eerst onderzoeken we wat ruimtelijk, praktisch en
						financieel haalbaar is.
					</p>
				</div>

				<div class="signup">
					<div class="signup-title">
						<p>Blijf vrijblijvend op de hoogte</p>
						<h2>Volg de ontwikkeling.</h2>
					</div>

					<form
						action={newsletterEndpoint || undefined}
						method="post"
						onsubmit={handleSignup}
					>
						<label for="email">E-mailadres</label>
						<div class="form-row">
							<input
								id="email"
								name="fields[email]"
								type="email"
								placeholder="jij@email.be"
								autocomplete="email"
								required
								bind:value={email}
							/>
							<input type="hidden" name="email" value={email} />
							<button type="submit">Hou me op de hoogte <span>→</span></button>
						</div>
					</form>

					<p class="fine-print">Alleen relevante projectupdates. Uitschrijven kan altijd.</p>
					{#if signupState === 'unconfigured'}
						<p class="message" role="status">Het inschrijfformulier wordt binnenkort geactiveerd.</p>
					{/if}
				</div>
			</div>
		</section>
	</main>

	<footer><span>© {year} TinyWijk</span><span>Gentse rand · Vlaamse Ardennen</span></footer>
</div>

<style>
	:global(*) { box-sizing: border-box; }
	:global(html) { background: #f3f0e8; }
	:global(body) {
		margin: 0;
		min-width: 320px;
		background: #f3f0e8;
		color: #173c2d;
		font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
		-webkit-font-smoothing: antialiased;
	}
	:global(button), :global(input) { font: inherit; }

	.page {
		width: min(1500px, 100%);
		min-height: 100vh;
		margin: auto;
		padding: 0 42px;
	}

	header {
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 92px;
	}

	.brand {
		display: flex;
		align-items: center;
		gap: 11px;
		color: inherit;
		font-size: 1.05rem;
		font-weight: 780;
		letter-spacing: -.02em;
		text-decoration: none;
	}

	.mark {
		display: grid;
		grid-template-columns: repeat(3, 6px);
		align-items: end;
		gap: 2px;
		width: 27px;
		height: 27px;
		padding: 4px;
		border: 1px solid #173c2d33;
		border-radius: 8px;
	}
	.mark i { display: block; height: 9px; border-radius: 2px; background: #173c2d; }
	.mark i:nth-child(2) { height: 16px; background: #c6814f; }
	.mark i:nth-child(3) { height: 12px; }

	.status {
		display: flex;
		align-items: center;
		gap: 9px;
		padding: 9px 14px;
		border: 1px solid #173c2d29;
		border-radius: 999px;
		background: #ffffff6b;
		font-size: .76rem;
		font-weight: 680;
	}
	.status i { width: 7px; height: 7px; border-radius: 50%; background: #c6814f; box-shadow: 0 0 0 4px #c6814f24; }

	.hero {
		display: grid;
		grid-template-columns: minmax(430px, .94fr) minmax(520px, 1.06fr);
		gap: clamp(48px, 6vw, 100px);
		align-items: center;
		min-height: calc(100vh - 160px);
		padding: 18px 0 50px;
	}

	.visual {
		position: relative;
		isolation: isolate;
		min-height: 680px;
		overflow: hidden;
		border-radius: 30px;
		background:
			radial-gradient(circle at 78% 17%, #f8e8b5 0 7%, transparent 7.3%),
			radial-gradient(circle at 8% 38%, #58795e 0 13%, transparent 13.3%),
			radial-gradient(circle at 91% 47%, #355d45 0 17%, transparent 17.3%),
			linear-gradient(155deg, #dbe3d2 0 38%, #9db394 38.2% 60%, #6e8c70 60.2%);
		box-shadow: 0 24px 70px #1b3a2b24;
	}

	.visual::before {
		position: absolute;
		z-index: 1;
		bottom: -180px;
		left: 39%;
		width: 175px;
		height: 650px;
		border-radius: 50% 50% 0 0;
		background: linear-gradient(90deg, #aa9879, #dfcfaa 52%, #9f8c6f);
		content: "";
		transform: perspective(450px) rotateX(61deg) rotate(7deg);
	}

	.visual::after {
		position: absolute;
		inset: 0;
		z-index: 20;
		border: 1px solid #ffffff73;
		border-radius: inherit;
		content: "";
		pointer-events: none;
	}

	.visual-meta, .visual-footer {
		position: absolute;
		z-index: 30;
		left: 24px;
		right: 24px;
		display: flex;
		justify-content: space-between;
		gap: 10px;
		font-size: .65rem;
		font-weight: 780;
		letter-spacing: .08em;
		text-transform: uppercase;
	}
	.visual-meta { top: 24px; }
	.visual-footer { bottom: 22px; color: #f9f6ed; letter-spacing: .02em; text-transform: none; }
	.visual-footer span { padding: 7px 9px; border: 1px solid #ffffff4d; border-radius: 999px; background: #173c2dc7; backdrop-filter: blur(8px); }

	.home { position: absolute; z-index: 8; filter: drop-shadow(0 18px 14px #173c2d38); }
	.home b {
		position: absolute;
		top: calc(100% + 10px);
		left: 50%;
		padding: 5px 8px;
		border-radius: 999px;
		background: #f4f0e5d9;
		font-size: .62rem;
		transform: translateX(-50%);
		white-space: nowrap;
	}

	.house {
		position: relative;
		width: 190px;
		height: 108px;
		border: 1px solid #304a3a38;
		border-radius: 3px;
		background: repeating-linear-gradient(90deg, transparent 0 15px, #5848381a 16px), #bd8157;
	}
	.house::before {
		position: absolute;
		top: -26px;
		left: -8px;
		width: calc(100% + 16px);
		height: 30px;
		background: #29483a;
		clip-path: polygon(5% 55%, 50% 0, 100% 70%, 97% 100%, 3% 100%, 0 70%);
		content: "";
	}
	.house::after {
		position: absolute;
		left: 18px;
		bottom: 17px;
		width: 92px;
		height: 48px;
		border: 4px solid #314b40;
		background: linear-gradient(145deg, #d9e8e1 0 45%, #88a09a 46%);
		box-shadow: 53px 10px 0 -6px #52685b, 53px 10px 0 -2px #314b40;
		content: "";
	}

	.home-30 { top: 38%; left: 7%; transform: rotate(-3deg) scale(.74); }
	.home-45 { top: 23%; right: 2%; transform: rotate(4deg) scale(.88); }
	.home-45 .house { background: #ded6c3; }
	.home-60 { right: 3%; bottom: 16%; transform: rotate(2deg) scale(1.02); }
	.home-60 .house { background: repeating-linear-gradient(90deg, transparent 0 17px, #304a3a12 18px), #bfc2aa; }

	.content { max-width: 650px; }
	.eyebrow {
		margin: 0 0 18px;
		color: #a36238;
		font-size: .74rem;
		font-weight: 800;
		letter-spacing: .14em;
		text-transform: uppercase;
	}

	h1 {
		margin: 0;
		font-family: Georgia, "Times New Roman", serif;
		font-size: clamp(3.35rem, 5.2vw, 5.8rem);
		font-weight: 500;
		letter-spacing: -.058em;
		line-height: .92;
	}
	h1 em { color: #658069; font-weight: 400; }

	.intro {
		margin: 27px 0 0;
		color: #496156;
		font-size: 1rem;
		line-height: 1.7;
	}

	.facts {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		margin: 28px 0;
		padding: 20px 0;
		border-block: 1px solid #173c2d24;
	}
	.facts div { padding: 0 17px; border-left: 1px solid #173c2d1f; }
	.facts div:first-child { padding-left: 0; border: 0; }
	.facts strong, .facts span { display: block; }
	.facts strong { margin-bottom: 5px; font-size: .86rem; }
	.facts span { color: #728078; font-size: .7rem; line-height: 1.4; }

	.reality-check {
		display: grid;
		grid-template-columns: 145px 1fr;
		gap: 18px;
		margin-bottom: 25px;
		padding: 16px 18px;
		border-left: 3px solid #c6814f;
		border-radius: 0 12px 12px 0;
		background: #e6e0d19e;
	}
	.reality-check strong { font-size: .74rem; }
	.reality-check p { margin: 0; color: #596c62; font-size: .77rem; line-height: 1.55; }

	.signup {
		padding: 22px;
		border-radius: 18px;
		background: #173c2d;
		color: #f8f4e9;
		box-shadow: 0 18px 50px #173c2d2e;
	}
	.signup-title { display: flex; align-items: end; justify-content: space-between; gap: 18px; margin-bottom: 14px; }
	.signup-title p { margin: 0; color: #afc1b5; font-size: .7rem; font-weight: 700; }
	.signup-title h2 { margin: 0; font: 400 1.5rem Georgia, serif; letter-spacing: -.035em; }
	form label { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0 0 0 0); }
	.form-row { display: grid; grid-template-columns: 1fr auto; gap: 9px; }

	input[type="email"] {
		min-width: 0;
		padding: 13px 15px;
		border: 1px solid #ffffff26;
		border-radius: 10px;
		outline: 0;
		background: #ffffff1a;
		color: white;
		transition: 160ms ease;
	}
	input[type="email"]::placeholder { color: #ffffff7a; }
	input[type="email"]:focus { border-color: #dfb08a; background: #ffffff24; }

	button {
		padding: 13px 17px;
		border: 0;
		border-radius: 10px;
		background: #c98250;
		color: white;
		font-size: .76rem;
		font-weight: 760;
		cursor: pointer;
		transition: 160ms ease;
	}
	button:hover { background: #d18c58; transform: translateY(-1px); }
	button span { display: inline-block; margin-left: 4px; transition: transform 160ms ease; }
	button:hover span { transform: translateX(3px); }
	button:focus-visible, .brand:focus-visible { outline: 3px solid #c6814f80; outline-offset: 3px; }
	.fine-print, .message { margin: 9px 0 0; font-size: .64rem; }
	.fine-print { color: #ffffff80; }
	.message { color: #f0bc94; font-weight: 650; }

	footer {
		display: flex;
		justify-content: space-between;
		padding: 15px 0 26px;
		border-top: 1px solid #173c2d1f;
		color: #778179;
		font-size: .66rem;
	}

	@media (max-width: 1050px) {
		.page { padding-inline: 28px; }
		.hero { grid-template-columns: minmax(360px, .85fr) minmax(450px, 1.15fr); gap: 42px; }
		.visual { min-height: 610px; }
		.facts { grid-template-columns: 1fr; gap: 13px; }
		.facts div, .facts div:first-child { padding: 0; border: 0; }
	}

	@media (max-width: 820px) {
		.page { padding-inline: 20px; }
		header { height: 78px; }
		.status { padding: 8px 10px; font-size: .64rem; }
		.hero { grid-template-columns: 1fr; gap: 42px; min-height: auto; padding: 10px 0 46px; }
		.visual { min-height: min(650px, 78vh); }
		.content { max-width: none; }
		h1 { font-size: clamp(3.2rem, 12vw, 5.3rem); }
		.facts { grid-template-columns: repeat(3, 1fr); gap: 0; }
		.facts div, .facts div:first-child { padding: 0 14px; border-left: 1px solid #173c2d1f; }
		.facts div:first-child { padding-left: 0; border-left: 0; }
	}

	@media (max-width: 560px) {
		.page { padding-inline: 15px; }
		header { height: 70px; }
		.status { max-width: 175px; line-height: 1.2; }
		.visual { min-height: 480px; border-radius: 22px; }
		.visual-meta span:last-child { display: none; }
		.visual-footer { left: 16px; right: 16px; bottom: 16px; justify-content: flex-start; }
		.visual-footer span { font-size: .58rem; }
		.visual-footer span:nth-child(2) { display: none; }
		.home-30 { left: -6%; transform: rotate(-3deg) scale(.58); }
		.home-45 { right: -15%; transform: rotate(4deg) scale(.66); }
		.home-60 { right: -13%; bottom: 17%; transform: rotate(2deg) scale(.76); }
		.eyebrow { font-size: .66rem; }
		h1 { font-size: clamp(2.8rem, 14vw, 4.3rem); }
		.intro { font-size: .93rem; }
		.facts { grid-template-columns: 1fr; gap: 13px; }
		.facts div, .facts div:first-child { padding: 0; border: 0; }
		.reality-check { grid-template-columns: 1fr; gap: 6px; }
		.signup-title { display: block; }
		.signup-title h2 { margin-top: 4px; }
		.form-row { grid-template-columns: 1fr; }
		button { width: 100%; }
		footer { flex-direction: column; gap: 7px; }
	}

	@media (prefers-reduced-motion: reduce) {
		:global(*) { transition-duration: .01ms !important; }
	}
</style>

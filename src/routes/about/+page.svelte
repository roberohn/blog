<script>
	import { Github, Linkedin } from 'lucide-svelte';
</script>

<!-- <img src="./avatar/Avatar24.png" alt="Avatar of John" /> -->
<h2 class="title">Hi i'm John 👋🏻</h2>
<p>I like to build things and automate stuff</p>

<div class="contactInfo">
	<!-- <p>Email: your.email@example.com | Phone: (555) 123-4567</p> -->
	<p>Location: UK</p>
	<p>&nbsp;|&nbsp;</p>
	<a href="https://www.linkedin.com/in/jroberts99/"><Linkedin /></a>
	<p>&nbsp;|&nbsp;</p>
	<a href="https://github.com/roberohn"><Github /></a>
</div>

<div class="summary">
	<h2>Professional Summary</h2>
	<p>
		A brief 2-3 sentence overview of your professional background, key skills, and what you're
		looking for.
	</p>
</div>

<main>
	<section>
		<h2>Work Experience</h2>

		<div class="experience-item">
			<p>
				<span class="job-title">Job Title</span> at <span class="company">Company Name</span> |
				<span class="date">Month Year - Present</span>
			</p>
			<ul>
				<li>Key accomplishment or responsibility</li>
				<li>Another achievement with quantifiable results</li>
				<li>Description of project or initiative you led</li>
			</ul>
		</div>

		<div class="experience-item">
			<p>
				<span class="job-title">Previous Job Title</span> at
				<span class="company">Previous Company</span>
				| <span class="date">Month Year - Month Year</span>
			</p>
			<ul>
				<li>Key accomplishment or responsibility</li>
				<li>Another achievement with quantifiable results</li>
			</ul>
		</div>
	</section>

	<section>
		<h2>Skills</h2>

		<div class="skills-section">
			<h3>Technical Skills</h3>
			<div class="skills-list">
				<span class="skill-tag">Skill 1</span>
				<span class="skill-tag">Skill 2</span>
				<span class="skill-tag">Skill 3</span>
				<span class="skill-tag">Skill 4</span>
				<span class="skill-tag">Skill 5</span>
			</div>
		</div>

		<div class="skills-section">
			<h3>Soft Skills</h3>
			<div class="skills-list">
				<span class="skill-tag">Skill 1</span>
				<span class="skill-tag">Skill 2</span>
				<span class="skill-tag">Skill 3</span>
			</div>
		</div>
	</section>

	<section>
		<h2>Education</h2>

		<div class="education-item">
			<p>
				<span class="degree">Degree Name</span> from <span class="school">University Name</span> |
				<span class="date">Graduation Year</span>
			</p>
			<p>Relevant coursework, honors, or activities</p>
		</div>

		<div class="education-item">
			<p>
				<span class="degree">Another Degree or Certification</span> from
				<span class="school">Institution</span>
				| <span class="date">Year</span>
			</p>
		</div>
	</section>
</main>

<style>
	h2 {
		font-size: var(--font-size-fluid-3);
		max-inline-size: var(--size-header-3);
	}

	h3 {
		font-size: var(--font-size-fluid-2);
	}

	main {
		display: grid;
		gap: var(--size-fluid-4);
		padding-block: var(--size-fluid-4);
		margin-inline: max(((100% - 70rem) / 2), var (--size-fluid-4));
	}

	section {
		display: grid;
		gap: var(--size-fluid-2);
		/* margin: auto; */
		max-inline-size: var(--size-content-3);
	}

	.contactInfo {
		padding-block: var(--size-fluid-2);
		display: flex;
	}
</style>

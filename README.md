<div class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="MWYROoK" data-preview="true" data-editable="true" data-user="ilithya"  data-prefill='{"title":"Stretch Typo","description":"I created this Stretch Typo Effect, with mobile support, to experiment with different mix-blend-modes in CSS while having a masked galaxy photo in the background.\n\n- Move your mouse or drag your finger to stretch the typo and stop the animation.\n- Click the black banner or your right/left arrow keys to switch the CSS mix-blend-mode, and experience the different effects with the masked galaxy photo.\n- Headline is editable, so place your cursor in the text and type anything else you&apos;d like.\n\nEnjoy!","tags":["javascript","css","typography","cssvariables","animation"],"head":"<link href=\"https://fonts.googleapis.com/css?family=Roboto+Condensed:700&amp;display=swap\" rel=\"stylesheet\">","scripts":["https://unpkg.com/splitting@1.0.6/dist/splitting.min.js"],"stylesheets":[]}'>
  <pre data-lang="pug">.typo#typo-wrapper
	h1(
		contenteditable='true'
		spellcheck='false'
	).typo__heading.has-anim Stretch

button(
	type='button'
	title='Click me! or click your right/left arrows'
)#btn.btn.btn--blend-mode CSS - mix-blend-mode: 
	span overlay
	| ;
	
p
	small.credit by ilithya </pre>
  <pre data-lang="scss" data-option-autoprefixer="true">:root {
	--shadow_x: 10px;
	--shadow_y: 10px;
}

$c_bg: hotpink;
$c_pen: #fffffd; // white
$c_dark: #191919; // black
$c_purple: #7c4de1;
$c_hue: 259; // Edit shadow color here

@mixin size($w, $h: $w) {
	width: $w;
	height: $h;
}

html,
body {
	height: 100%;
}

body {
	background-color: $c_bg;
	margin: 0;
	padding: 0;
	overflow: hidden;
}

::selection {
	background-color: $c_pen;
	color: $c_bg;
}

.typo {
	@include size(100%);
	cursor: default;
	display: flex;
	align-items: center;
	justify-content: center;
	
	// Galaxy photo by Marc Schulte
	// https://www.pexels.com/@marc-schulte-656598
	background-image: url('https://images.pexels.com/photos/2779948/pexels-photo-2779948.jpeg?auto=compress&cs=tinysrgb&h=1150&w=1660'); // More img compression - h=750&w=1260
	// Just another galaxy image to play with:
	// background-image: url('https://images.pexels.com/photos/957010/milky-way-starry-sky-night-sky-star-957010.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940');
	position: fixed;
	top: 0;
	left: 0;
	
	// Colored effect in galaxy bg photo toggled via JS
	&::after {
		@include size(100%);
		background-color: $c_bg;
		mix-blend-mode: overlay;
		content: '';
		position: absolute;
		top: 0;
		left: 0;
	}
	
	&__heading {
		color: $c_dark;
		font-family: 'Roboto Condensed', sans-serif;
		font-size: 35vmin;
		line-height: 30vmin;
		margin: 0;
		mix-blend-mode: lighten;
		outline: none;
		position: relative;
		z-index: 10; // To place it on top of color background
		
		// Color background - to cover galaxy bg, except inside typo
		&::after {
			@include size(500vw, 500vh);
			background-color: $c_bg;
			content: '';
			position: absolute;
			top: -250vh;
			left: -250vw;
			z-index: -1;
		}
	}
}

.has-shadow {
	text-shadow: 
		calc(var(--shadow_x) * -1) calc(var(--shadow_y) * 1) 0 hsl($c_hue, 11%, 71%),
		calc(var(--shadow_x) * -2) calc(var(--shadow_y) * 2) 0 hsl($c_hue, 21%, 69%),
		calc(var(--shadow_x) * -3) calc(var(--shadow_y) * 3) 0 hsl($c_hue, 31%, 67%),
		calc(var(--shadow_x) * -4) calc(var(--shadow_y) * 4) 0 hsl($c_hue, 41%, 65%),
		calc(var(--shadow_x) * -5) calc(var(--shadow_y) * 5) 0 hsl($c_hue, 51%, 63%),
		calc(var(--shadow_x) * -6) calc(var(--shadow_y) * 6) 0 hsl($c_hue, 61%, 61%),
		calc(var(--shadow_x) * -7) calc(var(--shadow_y) * 7) 0 hsl($c_hue, 71%, 59%), 
		calc(var(--shadow_x) * -8) calc(var(--shadow_y) * 8) 0 hsl($c_hue, 81%, 57%);
}

.has-anim {
	animation: anim_text 0.8s 0.4s cubic-bezier(.17,.67,.66,1.03) infinite alternate;
	
	@at-root {
		@keyframes anim_text {
			100% {
				transform: translate(80px, -80px);
				
				// FYI: I do not recommend attempting animating the text-shadow property in production or a real project, as performance-wise it's not the best because of the paint and layout time. Reference  - https://csstriggers.com/
				text-shadow: 
					calc(var(--shadow_x) * -1) calc(var(--shadow_y) * 1) 0 hsl($c_hue, 11%, 71%),
					calc(var(--shadow_x) * -2) calc(var(--shadow_y) * 2) 0 hsl($c_hue, 21%, 69%),
					calc(var(--shadow_x) * -3) calc(var(--shadow_y) * 3) 0 hsl($c_hue, 31%, 67%), 
					calc(var(--shadow_x) * -4) calc(var(--shadow_y) * 4) 0 hsl($c_hue, 41%, 65%),
					calc(var(--shadow_x) * -5) calc(var(--shadow_y) * 5) 0 hsl($c_hue, 51%, 63%),
					calc(var(--shadow_x) * -6) calc(var(--shadow_y) * 6) 0 hsl($c_hue, 61%, 61%),
					calc(var(--shadow_x) * -7) calc(var(--shadow_y) * 7) 0 hsl($c_hue, 71%, 59%),
					calc(var(--shadow_x) * -8) calc(var(--shadow_y) * 8) 0 hsl($c_hue, 81%, 57%);
			}
		}
	}
}

.btn {
	$font-size: 0.7rem;
	
	border: 0;
	color: $c_pen;
	cursor: pointer;
	font-family: Georgia, Times, "Times New Roman", serif;
	font-size: $font-size;
	letter-spacing: 1px;
	line-height: $font-size;
	outline: 1px solid transparent; // Fixes iOs jagged edges
	padding: 7px 10px 9px;
	position: absolute;
	right: -5px;
	text-decoration: none; // In case it's a link tag
	user-select: none;
	-webkit-tap-highlight-color: rgba(0,0,0,0);
	
	&--blend-mode {
		background-color: $c_dark;
		bottom: 25px;
		transform: rotateZ(-2deg);
	}
}

.credit {
	color: rgba($c_pen, 0.3);
	font-size: 0.6em;
	letter-spacing: 1px;
	position: absolute;
	bottom: 5px;
	right: 5px;
	user-select: none;
}

// Mix Blend Mode Options
// For a full view of current browser options and support - https://developer.mozilla.org/en-US/docs/Web/CSS/mix-blend-mode
// FYI - You could totally do this via CSS Variables instead, but in this case I wanted to play with old school classes.
.is-overlay {
	// This is also the default mix-blend mode in container
	&::after {
		mix-blend-mode: overlay;
	}
}

.is-color {
	&::after {
		mix-blend-mode: color;
	}
}

.is-exclusion {
	&::after {
		mix-blend-mode: exclusion;
	}
}

.is-hard-light {
	&::after {
		mix-blend-mode: hard-light;
	}
}

.is-color-burn {
	&::after {
		mix-blend-mode: color-burn;
	}
}

.is-darken {
	&::after {
		mix-blend-mode: darken;
	}
}

.is-difference {
	&::after {
		mix-blend-mode: difference;
	}
}

.is-saturation {
	&::after {
		mix-blend-mode: saturation;
	}
}

.is-color-dodge {
	&::after {
		mix-blend-mode: color-dodge;
	}
}

.is-multiply {
	&::after {
		mix-blend-mode: multiply;
	}
}

.is-normal {
	&::after {
		mix-blend-mode: normal;
	}
}

.is-hue {
	&::after {
		mix-blend-mode: hue;
	}
}

.is-screen {
	&::after {
		mix-blend-mode: screen;
	}
}</pre>
  <pre data-lang="babel">/*
 * STRETCH TYPO
 * Move your mouse or drag your finger to stretch the typo and stop the animation.
 * Click the black banner or your right/left arrow keys to switch the CSS mix-blend-mode, and experience the different effects with the masked galaxy photo in the background.
 *
 * Headline is editable, so place your cursor in the text and type anything else you'd like.
 *
 * #041 - #100DaysOfCode
 * By ilithya | 2020
 * https://www.ilithya.rocks/
 * https://twitter.com/ilithya_rocks
 */

const blendModes = [
	"overlay",
	"color",
	"exclusion",
	"hard-light",
	"color-burn",
	"darken",
	"difference",
	"saturation",
	"color-dodge",
	"multiply",
	"normal", // Same effect as lighten
	"hue",
	"screen",
];

function updateBlendMode(parentSelector) {
	const wrapper = document.querySelector("#typo-wrapper");
	const classPrefix = "is-";

	// Create current classes array
	const currentClasses = wrapper.className.split(" ");
	// Filter all classes NOT starting with the classPrefix
	const filteredClasses = currentClasses.filter(c => !c.startsWith(classPrefix));
	// Add all filteredClasses to wrapper
	wrapper.className = filteredClasses.join(" ").trim();	
	
	const modeContainer = parentSelector.querySelector("span");
	const modeVal = blendModes[modeIndex];
	// Add the appropriate text inside button, depeding on which mix-blend-mode value is running
	modeContainer.textContent = modeVal;
	
	// Add the appropriate class name, depeding on which mix-blend-mode value is running
	wrapper.classList.add(`is-${modeVal}`);
}

let modeIndex = 0;
function nextBlendMode(e, el = null) {
	// Update blend mode array index after last selection
	modeIndex = modeIndex >= blendModes.length - 1 ? 0 : ++modeIndex;
	
	const parentContainer = el === null ? e.currentTarget : el;
	updateBlendMode(parentContainer);
}

function prevBlendMode(el) {
	// Update blend mode array index after last selection
	modeIndex = modeIndex &lt;= 0 ? blendModes.length - 1 : --modeIndex;
	
	updateBlendMode(el);
}

const btn = document.querySelector("#btn");
btn.addEventListener("click", nextBlendMode);

function onClickArrowKeys(e) {
	// Right arrow key
	if (e.keyCode === 39) {
		nextBlendMode(null, btn);
	}
	
	// Left arrow key
	if (e.keyCode === 37) {
		prevBlendMode(btn);
	}
}
// Let's add the key events for the blend mode toggling
document.onkeydown = onClickArrowKeys;

function createShadows(e, currTarget) {
	// Walk effect based on Wes Bos' Mouse Move Shadow Exercise
	// https://tinyurl.com/touabxe
	const walk = Math.round(Math.max(window.innerWidth, window.innerHeight) / 2.5);
	const coordWalk = (coord, side) =>
		Math.round((coord / side * walk) - (walk / 2));
	const xWalk = coordWalk(e.clientX, currTarget.offsetWidth);
	const yWalk = coordWalk(e.clientY, currTarget.offsetHeight);

	const root = document.querySelector(":root");
	const cssVarX = "--shadow_x";
	const cssVarY = "--shadow_y";
	root.style.setProperty(cssVarX, `${xWalk / 10}px`);
	root.style.setProperty(cssVarY, `${yWalk / -10}px`);

	const typo = currTarget.querySelector(".typo__heading");
	typo.classList.remove("has-anim");
	typo.classList.add("has-shadow");
	typo.style.transform = `translate(${xWalk}px, ${yWalk}px)`;
	typo.blur();
}

function onMouseMove(e) {
	createShadows(e, e.currentTarget);
}
function onTouchMove(e) {
	createShadows(e.changedTouches[0], e.currentTarget);
}

const heading = document.querySelector(".typo");
heading.addEventListener("mousemove", onMouseMove);
heading.addEventListener("touchmove", onTouchMove);</pre></div>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

![mohammx-abrar-aleef-fsociety](https://user-images.githubusercontent.com/71467992/227808664-42e0e9df-e338-40cf-8826-ddc60d7f409d.jpg)

![github-contribution-grid-snake](https://user-images.githubusercontent.com/71467992/227808198-1cec7aca-fb25-4d69-a39b-af97faff2a97.svg)

<h1 align="center">Hi 👋, I'm Baran!</h1>
<h3 align="center">a pinch of stardust exploring the universe</h3>

<p align="center"> <img src="https://komarev.com/ghpvc/?username=samibarankorkmaz&label=Profile%20views&color=0e75b6&style=flat" alt="samibarankorkmaz" /> </p>

<p align="center"> <a href="https://github.com/ryo-ma/github-profile-trophy"><img src="https://github-profile-trophy.vercel.app/?username=samibarankorkmaz" alt="samibarankorkmaz" /></a> </p>

  - I’m currently working on: <h4>Computer Vision</h4>
  - I’m currently learning: <h4>OpenCV, MediaPipe, Numpy, PyTorch, YOLO, Sci-Kit</h4>
  - How to reach me: <h4>bkwebtr@gmail.com</h4>
<div class="container">
  <h1 class="heading" data-target-resolver></h1>
</div>


<h3 align="center">Socials</h3>
<p align="center">
<a href="https://linkedin.com/in/samibarankorkmaz" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="samibarankorkmaz" height="30" width="40" /></a>
<a href="https://stackoverflow.com/users/9073462" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/stack-overflow.svg" alt="9073462" height="30" width="40" /></a>
<a href="https://kaggle.com/samibarankorkmaz" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/kaggle.svg" alt="samibarankorkmaz" height="30" width="40" /></a>
<a href="https://instagram.com/samibarankorkmaz" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="@samibarankorkmaz" height="30" width="40" /></a>
<a href="https://medium.com/@samibarankorkmaz" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/medium.svg" alt="@samibarankorkmaz" height="30" width="40" /></a>
<a href="https://www.youtube.com/c/samibarankorkmaz" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="@samibarankorkmaz" height="30" width="40" /></a>
<a href="https://www.hackerrank.com/mrreboot" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/hackerrank.svg" alt="@mrreboot" height="30" width="40" /></a>
</p>

<h3 align="center">Languages and Tools</h3>
<p align="center"> <a href="https://getbootstrap.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/bootstrap/bootstrap-plain-wordmark.svg" alt="bootstrap" width="40" height="40"/> </a> <a href="https://codeigniter.com" target="_blank" rel="noreferrer"> <img src="https://cdn.worldvectorlogo.com/logos/codeigniter.svg" alt="codeigniter" width="40" height="40"/> </a> <a href="https://www.w3schools.com/css/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original-wordmark.svg" alt="css3" width="40" height="40"/> </a> <a href="https://firebase.google.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/firebase/firebase-icon.svg" alt="firebase" width="40" height="40"/> </a> <a href="https://flutter.dev" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/flutterio/flutterio-icon.svg" alt="flutter" width="40" height="40"/> </a> <a href="https://www.w3.org/html/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original-wordmark.svg" alt="html5" width="40" height="40"/> </a> <a href="https://www.adobe.com/in/products/illustrator.html" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/adobe_illustrator/adobe_illustrator-icon.svg" alt="illustrator" width="40" height="40"/> </a> <a href="https://www.java.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/java/java-original.svg" alt="java" width="40" height="40"/> </a> <a href="https://www.microsoft.com/en-us/sql-server" target="_blank" rel="noreferrer"> <img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="40" height="40"/> </a> <a href="https://opencv.org/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/opencv/opencv-icon.svg" alt="opencv" width="40" height="40"/> </a> <a href="https://www.photoshop.com/en" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/photoshop/photoshop-line.svg" alt="photoshop" width="40" height="40"/> </a> <a href="https://www.postgresql.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/postgresql/postgresql-original-wordmark.svg" alt="postgresql" width="40" height="40"/> </a> <a href="https://postman.com" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/getpostman/getpostman-icon.svg" alt="postman" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://spring.io/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/springio/springio-icon.svg" alt="spring" width="40" height="40"/> </a> <a href="https://www.sqlite.org/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/sqlite/sqlite-icon.svg" alt="sqlite" width="40" height="40"/> </a> </p>






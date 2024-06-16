---
title: Playground
---

<link rel="stylesheet" href="/playground/simulator.css">
<script type="module" src="/playground-play.js"></script>
<style>
#playground {
	margin-top: 1.5rem;
	margin-bottom: 0.75rem;
	display: flex;
	flex-direction: column;
}
#playground-header {
	display: flex;
	align-items: center;
	justify-content: space-between;
	flex-wrap: wrap;
}
#target .project-name .buttons {
	margin-left: 16px;
}
#input {
	min-height: 60vh;
	font-family: monospace;
	tab-size: 4;
	flex: 1 0 0;
	width: initial;
	resize: none; /* somehow it doesn't work, so disable it */
}
#middle {
	display: flex;
	flex-grow: 1;
	flex-direction: column;
	gap: 0.75rem;
}
#output {
	flex: 1 0 0;
}
@media (min-width: 768px) {
	#playground {
		margin-top: 5.5rem;
		/* 100% - header - padding bottom */
		height: calc(100vh - 5.5rem - 0.75rem);
	}
	#middle {
		flex-direction: row;
	}
}
</style>
<div id="playground">
	<div id="playground-header">
		<h2>Playground</h2>
		<div>
			<div id="target" class="btn-group mb-2">
				<button type="button" class="btn btn-primary dropdown-toggle" data-bs-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
				Console (TinyGo)
				</button>
				<div class="dropdown-menu">
					<a class="dropdown-item active" href>Console (TinyGo)</a>
					<span id="target-loading" class="dropdown-item disabled">Loading...</span>
				</div>
			</div>
			<button type="button" id="btn-flash" class="btn btn-secondary mb-2" disabled>Flash</button>
			<button type="button" id="btn-about" class="btn btn-secondary mb-2" data-bs-toggle="modal" data-bs-target="#aboutModal">About</button>
			<a href="/tour/" class="btn btn-secondary mb-2">Tour</a>
		</div>
	</div>
	<div id="middle">
		<textarea id="input" class="form-control input" spellcheck="false"></textarea>
		<div id="output" class="simulator inline">
			<div class="schematic-buttons">
				<button class="schematic-button-pause schematic-button" title="Pause/resume the simulation">
					<!-- only one of these two images is visible at a time -->
					<img src="/playground/resources/codicon/debug-pause.svg" class="button-img-pause"/>
					<img src="/playground/resources/codicon/play.svg" class="button-img-play"/>
				</button>
			</div>
			<svg class="schematic">
				<g class="schematic-wrapper" style="transform: translate(50%, 50%)">
					<g class="schematic-parts"></g>
					<g class="schematic-wires"></g>
				</g>
			</svg>
			<div class="panels">
				<div class="tabbar">
					<span class="tab active panel-tab-terminal"><a>Terminal</a></span>
					<span class="tab"><a>Properties</a></span>
					<span class="tab"><a>Add</a></span>
				</div>
				<div class="tabcontent active terminal-box">
					<textarea class="terminal" readonly></textarea>
				</div>
				<div class="tabcontent panel-properties">
					<div class="content"></div>
				</div>
				<div class="tabcontent panel-add">
					Loading...
				</div>
			</div>
			<div class="schematic-tooltip"></div>
		</div>
	</div>
	<div class="modal fade" id="aboutModal" tabindex="-1" aria-labelledby="aboutModalTitle" aria-hidden="true">
		<div class="modal-dialog">
			<div class="modal-content">
				<div class="modal-header">
					<h1 class="modal-title fs-5" id="exampleModalLabel">About TinyGo Playground</h1>
					<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
				</div>
				<div class="modal-body">
					<p>
						The TinyGo Playground is a service provided by the TinyGo project
						to compile and run small code samples directly in the browser. It
						has been heavily inspired by the <a
						href="https://play.golang.org/">Go Playground</a> but differs in
						some significant ways:
					</p>
					<ul>
						<li>
							We use the <a href="https://github.com/tinygo-org/tinygo">TinyGo compiler</a> in addition to the main Go compiler.
						</li>
						<li>
							Instead of running code on the server, code is compiled to <a
							href="https://webassembly.org/">WebAssembly</a> and runs
							directly in the browser.
						</li>
						<li>
							It can simulate a few popular boards directly in the browser.
							However, please note that this is a simulation which can differ
							in behavior from how the program will run on the actual device.
						</li>
						<li>
							Boards that support drag-and-drop programming can be flashed
							directly using the Flash button.
						</li>
					</ul>
					<p>
						For more information, visit <a
						href="https://tinygo.org/">tinygo.org</a>.
					</p>
					<p>
						Source code of the playground: <a
						href="https://github.com/tinygo-org/playground">github.com/tinygo-org/playground</a>.
					</p>
				</div>
				<div class="modal-footer">
					<button type="button" class="btn btn-primary" data-bs-dismiss="modal">Close</button>
				</div>
			</div>
		</div>
	</div>
</main>

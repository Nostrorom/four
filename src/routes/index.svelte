<script lang="ts">
	import { browser } from '$app/env';
	import * as THREE from 'three';

	let scene: THREE.Scene;
	let camera: THREE.Camera;
	let renderer: THREE.Renderer;
	let cube: THREE.Mesh;

	const createScene = () => {
		scene = new THREE.Scene();

		camera = new THREE.PerspectiveCamera(
			75,
			window.innerWidth / window.innerHeight,
			0.1,
			1000,
		);

		renderer = new THREE.WebGLRenderer({ antialias: true });
		renderer.setSize(window.innerWidth, window.innerHeight);
		document.body.appendChild(renderer.domElement);

		const geometry = new THREE.BoxGeometry(1, 1, 1);
		const texture = new THREE.TextureLoader().load('images/basalt.jpg');
		const material = new THREE.MeshBasicMaterial({ map: texture });

		cube = new THREE.Mesh(geometry, material);

		scene.add(cube);

		camera.position.z = 5;
	};
	const animate = (): void => {
		requestAnimationFrame(animate);

		cube.rotation.x += 0.01;
		cube.rotation.y += 0.02;

		renderer.render(scene, camera);
	};

	if (browser) {
		createScene();

		animate();
	}
</script>

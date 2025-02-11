<script lang="ts">
    import {T as Threlte} from "@threlte/core";
	import { createTransition, Float } from "@threlte/extras";
    import * as THREE from 'three';
    import gsap from "gsap";
	import { elasticOut } from "svelte/easing";

    export let position: [number, number, number] = [0,0,0];
    export let geometry: THREE.BufferGeometry = new THREE.IcosahedronGeometry(3);
    export let rate = 0.5;
    
    const soundEffects = [
        new Audio('/sounds/hit1.ogg'),
        new Audio('/sounds/hit2.ogg'),
        new Audio('/sounds/hit3.ogg')
    ]

    let visible = false;

	const materialParams = [
		{ color: 0xf87171, roughness: 0 },
		{ color: 0xf97316, roughness: 0.4 },
		{ color: 0xfef08a, roughness: 0.1 },
		{ color: 0x84cc16, roughness: 0.1 },
		{ color: 0x6ee7b7, roughness: 0.1 },
		{ color: 0x0891b2, roughness: 0, metalness: 0.5 },
		{ color: 0xc084fc, roughness: 0.1, metalness: 0.5 },
        { color: 0xa21caf, roughness: 0.3, metalness: 0.5 },
        { color: 0x9d174d, roughness: 0.2},
        { color: 0xe11d48, roughness:0.1, metalness: 0.5},
        { color: 0x0c4a6e, roughness:0.2},
        { color: 0xa8a29e, roughness:0, metalness: 0.5}
	];

    function getRandomMaterial(){
        const randomInt = gsap.utils.random(1,10,1)
        if( randomInt == 1){
            return new THREE.MeshNormalMaterial();
        }
        return new THREE.MeshStandardMaterial(gsap.utils.random(materialParams));
    }

    function handleClick(event: MouseEvent){
        gsap.utils.random(soundEffects).play();

        if('object' in event && event.object instanceof THREE.Mesh){
            gsap.to(event.object.rotation, {
                x: '+=2',
                y: '+=2',
                z: '+=2',
                duration: 1.3,
                ease: 'elastic.out(1, 0.3)',    
                yoyo: true
            })



            event.object.material = getRandomMaterial();
        }
    }
    

    const bounce = createTransition((ref) => {
        return {
            tick(t) {
                if( t>0 ) visible = true;
                ref.scale.set(t,t,t);
            },
            easing: elasticOut,
            duration: gsap.utils.random(800,1200),
            delay: gsap.utils.random(0,500)
        }
    })
</script>

<Threlte.Group position={position.map((p)=> p*2)}>
    <Float speed={5 * rate} rotationSpeed={5 * rate} rotationIntensity={6 * rate} floatIntensity={5 * rate}>
        <Threlte.Mesh {visible} {geometry} in={bounce} material={getRandomMaterial()}
            interactive
            on:click={handleClick}
        ></Threlte.Mesh> 
    </Float>
</Threlte.Group>


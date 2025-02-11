<script lang="ts">
	import { isFilled, type Content } from "@prismicio/client";
	import NavBarLinks from "./NavBarLinks.svelte";
	import Button from "./Button.svelte";
    import IcBaselineMenu from '~icons/ic/baseline-menu';
    import IcOutlineCancel from '~icons/ic/outline-cancel';


    export let settings: Content.SettingsDocument;

    let open = false;

    function OnLinkClick(){

    }
</script>

<header class="top-0 z-50 mx-auto max-w-7xl md:sticky md:top-4 relative">
    <nav>
        <div class="flex flex-col justify-between rounded-b-lg bg-slate-50 px-4 py-2 md:m4 md:flex-row md:items-center md:rounded-xl">
            <div class="flex items-center justify-between">
                <a href="/" aria-label="Homepage" class="text-xl font-extrabold tracking-tigther text-slate-900 hover:text-yellow-400">
                    {settings.data.name} 
                </a>
                <button aria-expanded={open} aria-label="Open Menu" class="block p-2 text-2xl text-slate-800 md:hidden" on:click={()=>(open = true)}>
                    <IcBaselineMenu />
                </button>
            </div>


            
            <ul class={`fixed inset-0 z-50 flex flex-col items-end gap-4 bg-slate-50 pr-4 pt-14 transition-transform duration-300 ease-in-out md:hidden ${open ? 'translate-x-0' : 'translate-x-[100%]'}`}>
                <li>
                    <button aria-expanded={open} aria-label="Close Menu" class="fixed right-4 top-3 block p-2 text-2xl text-slate-800 md:hidden" on:click={()=>(open = false)}>
                        <IcOutlineCancel />
                    </button>
                </li>
                {#each settings.data.nav_item as {label, link}}
                    <li class="first:mt-8">
                        <NavBarLinks field={link} label={label} {OnLinkClick} type="mobile" />
                    </li>
                {/each}
                {#if isFilled.link(settings.data.cta_link)}
                    <Button linkField = {settings.data.cta_link} label={settings.data.cta_label} class="ml-3" />
                {/if}  
            </ul>



            <ul class="relative z-50 hidden flex-row items-center gap-3 bg-transparent py-0 md:flex">
                {#each settings.data.nav_item as {label, link}}
                    <li>
                        <NavBarLinks field={link} label={label} {OnLinkClick} type="desktop" />
                    </li>
                {/each}   
                {#if isFilled.link(settings.data.cta_link)}
                    <Button linkField = {settings.data.cta_link} label={settings.data.cta_label} class="ml-3" />
                {/if}            
            </ul>
        </div>
    </nav>
</header>
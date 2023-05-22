<script lang="ts">
    import { writable } from 'svelte/store';
    import { slide } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';

    import MenuIcon from '../components/MenuIcon.svelte';
    import MobileMenu from '../components/MenuMobile.svelte';
	import Logo from '../components/Logo.svelte';
  
    // Create a store and update it when necessary...
    let visible = writable(false);
</script>
  
<div class="navbar w-full m-0 p-0">
    <div class="flex-1">
        <Logo />
    </div>
    <div class="flex-none justify-end ">
        <!-- hides above sm breakpoint -->
        <div class="inline md:hidden h-full z-50 bg-inherit " on:click={() => $visible = !$visible } on:keypress={() => $visible = !$visible }>
            <MenuIcon />
        </div>

        <!-- md breakpoint and up-->
        <ul class="hidden md:flex text-black menu menu-horizontal">
            <li><a href="/platform">Platform</a></li>
            <li><a href="/runtime">Runtime</a></li>
            <li><a href="/playground">Playground</a></li>
            <!--
            <li>
                <a href="/">
                    Community
                    <svg class="fill-current" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24"><path d="M7.41,8.58L12,13.17L16.59,8.58L18,10L12,16L6,10L7.41,8.58Z"/></svg>
                </a>
                <ul class="p-1 shadow-sm bg-slate-700 border-slate-100">
                    <li class="bg-slate-600"><a href="/discord">Discord</a></li>
                    <li class="bg-slate-600"><a href="/github">Github</a></li>
                    <li class="bg-slate-600"><a href="/twitter">Twitter</a></li>
                    <li class="bg-slate-600"><a href="/instagram">Instagram</a></li>
                    <li class="bg-slate-600"><a href="/blog">Blog</a></li>
                    <li class="bg-slate-600"><a href="/tutorials">Tutorials</a></li>
                </ul>
            </li>
            -->
            <li><button class="p-3 ml-3 mr-5 bg-sky-700 text-white rounded-lg"><strong><a href="/signin">Sign In</a></strong></button></li>
        </ul>
    </div>
</div>
  
{#if $visible}
    <div class="drawerMenu" transition:slide="{{delay: 150, duration: 450, easing: quintOut}}">
        <MobileMenu />
    </div>
{/if}


<style>
    .drawerMenu {
        position: absolute;
        top: 0;
        left: 0;
        width: 104%;
        height: 100vh;
        color: #fff;
        z-index: 4;
        padding-top: 80px;
        overflow: hidden;
        text-align: center;
        background-color: #efefef;
    }
</style>
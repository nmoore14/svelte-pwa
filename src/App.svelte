<script>
    import { writable } from 'svelte/store';
    import Modal, { bind } from 'svelte-simple-modal';
    import Events from './lib/Events.js';
    import Navbar from './components/Navbar.svelte';
    import Footer from './components/Footer.svelte';
    import MinimalCard from './components/cards/MinimalCard.svelte';
    import TalkInfo from './components/modals/TalkInfo.svelte';

    const modal = writable(null);
    const showModal = (forum) => {
        modal.set(bind(TalkInfo, { forum: forum }));
    }

    let forums = Events;

    function handleTalk(event) {
        showModal(event.detail.forum);
    }
</script>

<main class="grid grid-r-3 grid-c-3 w-screen h-screen bg-gray-200">
    <Modal show={$modal}
        styleBg={{ backgroundColor: 'rgba(0, 0, 0, 0.75)' }}
        styleWindow={{ boxShadow: '0 2px 5px 0 rgba(0, 0, 0, 0.15)' }}
    >
    </Modal>
    <Navbar/>
    <div class="flex flex-col justify-start items-start nowrap span-c-center w-full h-full scroll-y content">
        {#each forums as forum}
            <MinimalCard forum={forum} on:talk={handleTalk}/>
        {/each}
    </div>
    <Footer/>
</main>

<style>
</style>

<script>
  import { Modal } from 'sveltestrap';
  import Skill from './Skill.svelte';
  import { theme } from '../store';
  import { locale } from 'svelte-i18n';
  import Icon from '@iconify/svelte';
  export let data;
  export let show;
  export let closeModal;
</script>

<Modal
  size="md"
  aria-labelledby="contained-modal-title-vcenter"
  centered
  class={`${$theme}-bg`}
  isOpen={show}
  toggle={closeModal}>
  <div class={`${$theme}-bg p-3`}>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <span on:click={() => closeModal()} class="mb-5"><Icon icon="formkit:close" width={20} /></span>
    <div class="d-flex flex-column align-items-center">
      <img src={data.image.url} alt="None" class={data.image.orientation} />
      <h3 class={`${$theme}-text pt-5 pb-5`}>
        {data.title}
        <a href={data.url} target="_blank" rel="noopener noreferrer" class="link-href">
          <i class="fas fa-external-link-alt" style={{ marginLeft: '10px' }} />
        </a>
      </h3>
      <p class={`modal-description pt-5 pb-5 ${$theme}-text`}>
        {data.description[$locale]}
      </p>
      <div class="col-md-12 text-center pt-5 pb-5">
        <ul class="list-inline mx-auto">
          {#each data.tech as skill}
            <Skill {skill} textTheme={$theme} />
          {/each}
        </ul>
      </div>
    </div>
  </div>
</Modal>

<style>
  .portrait {
    width: 300px;
  }
  .landscape {
    min-width: 400px;
    width: 100%;
  }
</style>

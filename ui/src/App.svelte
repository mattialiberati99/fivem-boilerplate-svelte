<script>
  let name = $state("");
  let lastname = $state("");
  let age = $state("");
  let height = $state("");
  let nationality = $state("");

  let isVisible = $state(true);

  window.addEventListener('message', (event) => {
    if (event.data.action === 'openIdentity') {
      isVisible = true; // Mostra l'interfaccia
    }
  });

  async function submit() {
    await fetch(`https://${GetParentResourceName()}/submitIdentity`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name, lastname, age, height, nationality }),
    });

    isVisible = false;
  }
</script>

{#if isVisible}
<main class="flex items-center justify-center h-screen w-screen text-white" style="background-image: url('/images/identity/bg.webp')">
  <div class="bg-gray-900 p-6 rounded-lg shadow-lg w-96">
    <h1 class="text-2xl font-bold mb-4 text-center">Creazione Personaggio</h1>
    <form class="space-y-4" onsubmit={submit}>
      <input
        type="text"
        class="w-full p-2 rounded bg-gray-700 text-white"
        placeholder="Nome"
        bind:value={name}
      />
      <input
        type="text"
        class="w-full p-2 rounded bg-gray-700 text-white"
        placeholder="Cognome"
        bind:value={lastname}
      />
      <input
        type="number"
        class="w-full p-2 rounded bg-gray-700 text-white"
        placeholder="Età"
        bind:value={age}
      />
      <input
        type="number"
        class="w-full p-2 rounded bg-gray-700 text-white"
        placeholder="Altezza"
        bind:value={height}
      />
      <input
        type="text"
        class="w-full p-2 rounded bg-gray-700 text-white"
        placeholder="Nazionalità"
        bind:value={nationality}
      />
      <button
        type="submit"
        class="w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 rounded"
      >
        Conferma
      </button>
    </form>
  </div>
</main>
{/if}

<style>
</style>
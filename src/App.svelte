<script>
  import RandomComponent from './RandomComponent.svelte';
  import TheBigParagraph from './TheBigParagraph.svelte';

  let user = { loggedIn: false}

  function toggle(){
    user.loggedIn = !user.loggedIn;
  }

  const paragraphInfo = {
    animal: "Donkey",
    location: "Bear Creek Park",
    gender: "Male",
    number_of_frogs: 18
  }

  export let name;
  export let methhead;
  let count = 0;
  $: doubled = count * 2;
  function handleClick() {
    count += 1;
  }
  $: {
    console.log(`The Count is ${count}`);
    if (count >= 5) {
      alert(`The count is too dangerously high bud. We gonna stop it here.`);
      count = 5;
    }
  }

  let numbers = [1, 2, 3, 4];

  function addNumber() {
    numbers = [...numbers, numbers.length + 1];
  }

  $: sum = numbers.reduce((t, n) => t + n, 0);
</script>

<main>
  <h1 class="blue">Hello {name}!</h1>
  <p>
    Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn
    how to build Svelte apps.
  </p>
  <button on:click="{handleClick}">
    Clicked {count}{count == 1 ? ' time': ' times'}
  </button>
  <p>{count} doubled is {doubled}</p>
  <button on:click="{addNumber}">
    Add a number
  </button>
  <p>{numbers.join(' + ')} = {sum}</p>
  <div>
    <p class = "randomcomponent">
      RandomComponent w/ prop: <RandomComponent answer = {42}/>
    </p>
    <p class = "randomcomponent">
      RandomComponent with default: <RandomComponent/>
    </p>
  </div>
  <section>
    <TheBigParagraph {...paragraphInfo}/>
  </section>

  {#if user.loggedIn}
	  <button on:click={toggle}>
		  Log out
	  </button>
  {:else}  <!--this could be an else if as well-->
  	<button on:click={toggle}>
  		Log in
  	</button>
  {/if}

</main>

<style>
  section {
    text-align: center;
  }

  p.randomComponent {
    text-align: center;
  }

  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

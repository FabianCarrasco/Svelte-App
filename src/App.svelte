<script lang="ts">
  const name = 'Batman';
  const channel = '<b>Codevolution</b>';
  const id = 'heading';
  const disabled = true;
  const status = 'success';
  const isPromoted = true;
  const promoted = true;


  let num: number = 1;

  const names = ['Bruce', 'Clark', 'Diana'];
  const fullNames = [
    {first: 'Bruce', last: 'Wayne'},
    {first: 'Clark', last: 'Kent'},
    {first: 'Princess', last: 'Diana'}
  ]

  let count: number = 0;

  function handleClick(event, stepSize: number) {
    console.log(event)
    count += stepSize;
  }

  const formValues = {
    name: '',
    profileSummary: '',
    country: '',
    jobLocation: '',
    remoteWork: false,
    skillSet: [],  
    yearsOfExperience: '',

  }  

  function submitForm(event: SubmitEvent){
    event.preventDefault();
    console.log(formValues)
  }
</script>

<main>
  <h1>Hello {2 + 2}</h1>
  <h2 class={status}>Status</h2>
  <div {id}>{@html channel}</div>
  <button {disabled}>Bind</button>
  <h2 class="underline">Underlined Text</h2>
  <h2 class={isPromoted? 'promoted' : ''}>Movie Title</h2>
  <h2 class:promoted={isPromoted}>Movie Title</h2>

  {#if num === 0}
    <h2>The number is zero</h2>
  {:else if num < 0}
    <h2>The number is negative</h2>
  {:else if num > 0}
    <h2>The number is positive</h2>
  {:else}
    <h2>Not a number</h2>
  {/if}

  {#each names as name, index (name)}
    <h2>{index + 1} {name}</h2>
  {/each}   

  {#each fullNames as name, index (name.first)}
    <h1>{index + 1} {name.first} {name.last}</h1>
  {/each}

  <button on:click={() => (count = count + 1)}>Count {count}</button>
  <button on:click={() => handleClick(event, 10)}>Count {count}</button>

  <div>
    <pre>
      {JSON.stringify(formValues, null, 2)}
    </pre>
  </div>

  <form on:submit|preventDefault={submitForm}>
    <div>
      <label for="name">name</label>
      <input type="text" id="name" bind:value={formValues.name}>
    </div>
  
    <div>
      <label for="profile">Profile Summary</label>
      <textarea id="profile" bind:value={formValues.profileSummary} ></textarea>
    </div>

    <div>
      <label for="country">Country</label>
      <select  id="country" bind:value={formValues.country}>
        <option value="">Select a Country</option>
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
      </select>
    </div>

    
    <div>
      <label for="job-location">Job Location</label>
      <select  id="job-location" bind:value={formValues.jobLocation} multiple>
        <option value="">Select a Country</option>
        <option value="india">India</option>
        <option value="vietnam">Vietnam</option>
        <option value="singapore">Singapore</option>
      </select>
    </div>

    <div>
      <input type="checkbox" id="remoteWork" bind:checked={formValues.remoteWork}/>
      <label for="remoteWork">Open to remote work?</label>
    </div>

    <div>
      <label>Skill set</label>
      <input type="checkbox" id="html" value="html" bind:group={formValues.skillSet}/>
      <label for="html">HTML</label>
      <input type="checkbox" id="css" value="css" bind:group={formValues.skillSet} />
      <label for="css">CSS</label>
      <input type="checkbox" id="javascript" value="javascript" bind:group={formValues.skillSet}>
      <label for="javascript">JavaScript</label>
    </div>
    
    <div>
      <label>Years of Experience</label>
      <input type="radio" id="0-2" value="0-2" bind:group={formValues.yearsOfExperience}/>
      <label for="0-2">0-2</label>
      <input type="radio" id="3-5" value="3-5" bind:group={formValues.yearsOfExperience}/>
      <label for="3-5">3-5</label>
      <input type="radio" id="6-10" value="6-10" bind:group={formValues.yearsOfExperience}/>
      <label for="6-10">6-10</label>
      <input type="radio" id="10+" value="10+" bind:group={formValues.yearsOfExperience}/>
      <label for="10+">10+</label>
    </div>

    <div>
      <button>Submit</button>
    </div>

  </form>


</main>

<style>
  input + label {
    display: inline-flex;
  }
  .underline {
    text-decoration: underline;
  }
  .danger {
    color: red;
  }
  .success {
    color: olive;
  }
  .promoted {
    font-style: italic;
  }
  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
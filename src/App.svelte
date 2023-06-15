<script>
  import { onMount } from "svelte";
  import PlusMinus from "./lib/components/PlusMinus.svelte";
  import PlusMinus2 from "./lib/components/PlusMinus2.svelte";

  let testHeadline3;
  let w1;
  let w2;
  let w3;
  onMount(async () => {
    // console.log("test-headline3", testHeadline3);
    console.log("w1", w1);
    console.log("w2", w2);
    console.log("w3", w3);

    // await Promise.resolve().then(() => {
    //   testHeadline3.setAttribute("title", "How your salary affect your child benefit");
    //   testHeadline3.setAttribute(
    //     "figures",
    //     JSON.stringify([
    //       {
    //         label: "Child benefit lost each year",
    //         value: "£1915.60",
    //         color: "#DE0000",
    //       },
    //       {
    //         label: "Child benefit lost over 16 years",
    //         value: "£30,643.20",
    //         color: "#DE0000",
    //       },
    //     ]),
    //   );
    // });
  });

  const attachProps = (node) => {
    switch (node.localName) {
      case "eip-plusminus": {
        node.startingvalue = 3;
        node.incrementsize = 3;
        node.range = [0, 100];
        break;
      }
      default:
        break;
    }
  };

  let plusMinusValue = 0;
</script>

<main>
  <!-- <h1>SVELTE v4 COMPONENTS</h1>
  <p>
    This page showcases the exciting capabilities of Svelte (v4) components, allowing them to be created either as <span>
      <a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_components"> Custom Elements </a>
    </span>
    or as traditional
    <span>
      <a href="https://github.com/sveltejs/svelte/pull/8457"> Svelte components. </a>
    </span>
  </p> -->

  <section>
    <div>
      <p>PlusMinus.svelte:</p>
      <eip-plusminus bind:this={w1} value={0} type="pounds" use:attachProps />

      <hr />

      <eip-plusminus bind:this={w2} value={plusMinusValue} type="pounds" startingvalue={3} incrementsize={3} range={[0, 100]} />
    </div>

    <div>
      <!-- UN-COMMENT THIS COMPONENT BELOW TO SEE console.ERRORS -->
      <p>PlusMinus2.svelte:</p>
      <!-- <eip-plusminus2 bind:this={w3} value={plusMinusValue} type="pounds" starting-value={5} increment-size={10} range={[0, 100]} /> -->
    </div>
  </section>
</main>

<style>
  section {
    border: 1px solid #767676;
    border-radius: 4px;
    padding-block: 0.5rem 2rem;
    padding-inline: 1rem;
    margin-bottom: 2rem;
  }

  h1 {
    font-size: 2rem;
    line-height: 1.1;
  }

  h1,
  h2 {
    margin-bottom: 0;
  }
  h1 ~ p,
  h2 ~ p {
    margin-top: 0;
  }

  section p {
    font-weight: 500;
    margin-top: 0;
    margin-bottom: 4px;
  }

  hr {
    height: 8px;
    width: 100%;
    margin-block: 1.5rem;
    background-color: #222;
    border: none;
  }

  section div {
    margin-top: 0.5rem;
    border: 1px dashed #222;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    gap: 4px;
  }
</style>

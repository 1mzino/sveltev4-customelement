<svelte:options
  customElement={{
    tag: "eip-plusminus",
    props: {
      value: { reflect: true, type: "Number", attribute: "value" },
      type: { reflect: true, type: "String", attribute: "type" },
      startingvalue: { reflect: true, type: "Number", attribute: "startingvalue" },
      incrementsize: { reflect: true, type: "Number", attribute: "incrementsize" },
      range: { reflect: true, type: "Array", attribute: "range" },
    },
  }} />

<script>
  export let value = 0;
  export let type = "";
  export let startingvalue = 0;
  export let incrementsize = 0;
  export let range = [0, 100];

  let addOpacity;
  let subtractOpacity;

  const add = () => {
    let newValue = value + incrementsize;

    if (range) {
      if (newValue >= range[0] && newValue <= range[1]) {
        value = newValue;
      }
    } else {
      value = newValue;
    }
  };
  const subtract = () => {
    let newValue = incrementsize ? value - incrementsize : value - 1;

    if (range) {
      if (newValue >= range[0] && newValue <= range[1]) {
        value = newValue;
      }
    } else {
      value = newValue;
    }
  };

  if (startingvalue) value = startingvalue;

  $: if (value >= range[1]) {
    addOpacity = 0;
    subtractOpacity = 1;
  } else if (value <= range[0]) {
    subtractOpacity = 0;
    addOpacity = 1;
  } else {
    addOpacity = 1;
    subtractOpacity = 1;
  }
</script>

<div class="plus-minus__wrapper">
  <!-- <button class="plus-minus__button {subtractOpacity === 0 ? 'disable' : ''}"  on:click={subtract} -->
  <button class="plus-minus__button" class:disable={subtractOpacity === 0} on:click={subtract}
    ><svg width="12" height="2" viewBox="0 0 12 2" fill="none" xmlns="http://www.w3.org/2000/svg">
      <line x1="0.8" y1="1.2" x2="11.2" y2="1.2" stroke="#222222" stroke-width="1.6" stroke-linecap="round" />
    </svg>
  </button>

  <span class="plus-minus__value">{type === "pounds" ? "£" : ""}{value.toLocaleString()}{type === "percentage" ? "%" : ""} </span>
  <button class="plus-minus__button" on:click={add}>
    <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg" class={addOpacity === 0 ? "disable" : ""}>
      <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg" class:disable={addOpacity === 0}>
        <line x1="0.8" y1="5.8665" x2="11.2" y2="5.8665" stroke="#222222" stroke-width="1.6" stroke-linecap="round" />
        <line x1="6.13398" y1="0.8" x2="6.13398" y2="11.2" stroke="#222222" stroke-width="1.6" stroke-linecap="round" />
      </svg>
    </svg></button>
</div>

<style lang="scss">
  .plus-minus {
    &__wrapper {
      display: flex;
      flex-direction: row;
      margin: 12px 0px 18px;
      width: 100%;
    }

    &__value {
      font-family: "Doric News";
      font-variation-settings: var(--font-doric-news-ui-bold);
      margin: auto 8px;
      color: #494949;

      font-size: 30px;
      line-height: 39px;
      white-space: nowrap;
    }

    &__button {
      background-color: inherit;
      border: 1px solid #b5b5b5;
      border-radius: 4px;

      min-width: 42px;
      min-height: 42px;
      cursor: pointer;
    }
  }

  .disable {
    cursor: default;
    line {
      stroke: #b2b2b2;
    }
  }
</style>

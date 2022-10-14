<script lang="ts">
  let url = "";
  const cutting = () => {
    console.log("cut");
  };
  const pickup = () => {
    console.log("pickup");
    chrome.tabs.query({ active: true, lastFocusedWindow: true }, (tabs) => {
      url = tabs[0].url;
    });
  };
</script>

<div>
  <h1>ピカピカ</h1>
  <button type="button" on:click={cutting}>cutting, URL</button>
  <button type="button" on:click={pickup}>pick up, URL</button>
  {url}
</div>

<style>
  div {
    width: 500px;
  }
</style>

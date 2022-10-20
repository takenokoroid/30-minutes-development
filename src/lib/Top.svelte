<script lang="ts">
  import { tick } from "svelte";

  let url = "";
  let inputRef: HTMLInputElement = null;
  const NOTION_URL = "https://www.notion.so";

  const cutting = () => {
    console.log("cut");
  };

  const formatUrl = (url: string): string => {
    const notionId = url.split("-").slice(-1)[0];
    let result = `${NOTION_URL}/${notionId}`;
    return result;
  };

  const pickup = () => {
    console.log("pickup");
    chrome.tabs.query({ active: true, lastFocusedWindow: true }, (tabs) => {
      url = formatUrl(tabs[0].url);
      tick().then(() => {
        inputRef.focus();
        inputRef.select();
        document.execCommand("copy");
      });
    });
  };
</script>

<div>
  <h1>ピカピカ</h1>
  <button type="button" on:click={cutting}>cutting, URL</button>
  <button type="button" on:click={pickup}>pick up, URL</button>
  <input type="text" value={url} bind:this={inputRef} />
</div>

<style>
  div {
    width: 500px;
  }
</style>

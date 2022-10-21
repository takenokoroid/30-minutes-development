<script lang="ts">
  import { tick } from "svelte";

  let url = "";
  let inputRef: HTMLInputElement = null;
  let divRef: HTMLDivElement = null;

  const NOTION_URL = "https://www.notion.so";

  const formatUrl = (url: string): string => {
    const notionId = url.includes("?p=")
      ? url.split("?p=").at(0)
      : url.split("-").at(-1);
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
  <button type="button" on:click={pickup}>pick up, URL</button>
  <input type="text" value={url} bind:this={inputRef} />
  <div id="test" bind:this={divRef}>{url}</div>
</div>

<style>
  div {
    width: 500px;
  }
</style>

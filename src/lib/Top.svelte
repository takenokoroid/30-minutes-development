<script lang="ts">
  import { tick } from "svelte";
  import pickUpIcon from "../assets/pick-up.svg";

  let url = "";
  let inputRef: HTMLInputElement = null;

  const formatUrl = (url: string): string => {
    const NOTION_URL = new URL(url);
    const PARSED_URL = NOTION_URL.href.split("/").slice(0, -1).join("/");
    const notionId = url.includes("?p=")
      ? url.split("?p=").at(-1).split("&")[0]
      : url.split("-").at(-1);
    let result = `${PARSED_URL}/${notionId}`;
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
  <h1>pick up,pick up</h1>
  <div>
    <button type="button" on:click={pickup}>
      <img src={pickUpIcon} class="icon" alt="Pick up" />
    </button>
  </div>
  <input type="text" value={url} bind:this={inputRef} />
</div>

<style>
  div {
    width: 500px;
  }
  .icon {
    width: 200px;
  }
</style>

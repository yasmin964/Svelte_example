<script lang="ts">
  import type { Message } from './message';//import type

  export let message: Message;
</script>

<li>
  <span style="font-weight: bold;">{message.username}: </span>
  {message.message}
</li>

<style>
  li {
    padding: 0.5rem 1rem;
  }
  li:nth-child(odd) {
    background-color: #f8f8f8;
  }
</style>
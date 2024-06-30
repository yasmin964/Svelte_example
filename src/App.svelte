<script lang="ts">
  import { io } from "socket.io-client";
  import MessageItem from "./Message.svelte";
  import Input from "./Input.svelte";
  import type { Message } from "./message";

  let messages: Message[] = [];

  const socket = io("https://fwd.innopolis.university");

  // Whenever a new chat message is received, this function 'send' is executed.
  socket.on("chat message", function (msg: Message) {
    messages.push(msg);// adds the new message to the messages array.
    messages = messages;// triggers Svelte's reactivity to update the UI with the new message.
    // messages = [...messages, msg];
    window.scrollTo(0, document.body.scrollHeight);
  });

  function sendMessage(msg: Message) {
    socket.emit("chat message", msg);// that emits a "chat message" event to the server, sending the provided message msg.
  }
</script>

<main>
  <ul>
    {#each messages as message}
      <MessageItem {message} />
    {/each}
  </ul>
  <Input on:send={(e) => sendMessage(e.detail)} />
</main>

<style>
  ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
  }
</style>

<script lang="ts">
    import { createEventDispatcher } from 'svelte';// the Svelte framework used to create custom events.
    import type { Message } from './message';//  is an import of a TypeScript type definition for a Message, ensuring that the code adheres to a certain structure for the messages.
  
    const dispatch = createEventDispatcher<{ send: Message }>();// which means it can dispatch an event named send that carries a payload of type Message
  
    // These will hold the user input.
    let message = '';
    let username = '';
  
    // This function is triggered when the form is submitted
    function send(e: SubmitEvent) {
      if (!message || !username) return;// it returns early and does nothing.
      dispatch('send', { message, username });
      message = '';// After dispatching the event, it resets the message to an empty string 
    }
  </script>
  
  <form on:submit|preventDefault={send} action="">
    <input autocomplete="off" bind:value={username} placeholder="Name" style:flex-grow="0" />
    <input autocomplete="off" bind:value={message} placeholder="Type your message..." />
    <button>Send</button>
  </form>

  <!-- Two-Way Data Binding
    From Input to Variable:
    When the user types something into the input field, the value of the input field is automatically assigned to the message variable.

    From Variable to Input:
    If the message variable is updated programmatically within the Svelte component, the input field's value will automatically reflect the new value. -->
  
  <style>
    form {
      background: rgba(0, 0, 0, 0.15);
      padding: 0.25rem;
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      display: flex;
      height: 3rem;
      box-sizing: border-box;
      backdrop-filter: blur(10px);
    }
    input {
      border: none;
      padding: 0 1rem;
      flex-grow: 1;
      border-radius: 2rem;
      margin: 0.25rem;
    }
    input:focus {
      outline: none;
    }
    form > button {
      background: #333;
      border: none;
      padding: 0 1rem;
      margin: 0.25rem;
      border-radius: 3px;
      outline: none;
      color: #fff;
    }
  </style>
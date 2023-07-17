<template>
  <div class="flex flex-col gap-5 justify-center items-center m-5">
    <h1 class="text-2xl font-mono">{{ `<nostr-one />` }}</h1>
    <div>
      <a
        class="link link-primary"
        href="https://github.com/nostr-protocol/nips/blob/master/98.md"
        >NIP-98 specs</a
      >
      -
      <a class="link link-primary" href="https://github.com/dolu89/nostr-one"
        >Documentation</a
      >
    </div>
    <div>A login button for react, vue, native HTML... It's a native component</div>

    <div class="mockup-code">
      <pre data-prefix="$"><code>npm i nostr-one</code></pre>
      <pre data-prefix="#"><code>Edit my-component.vue</code></pre>
      <pre>
        <code>import "nostr-one";</code>
        <code>
          {{ `<nostr-one` }}
          {{ `  loginUrl="https://website.com/login"` }}
          {{ `  httpMethod="post"` }}
          {{ `  :onError.prop="handleError"` }}
          {{ `  :onSuccess.prop="handleSuccess"` }}
          {{ `>` }}
          {{ `</nostr-one>` }}
        </code>
      </pre>
    </div>
    <nostr-one
      loginUrl="https://website.com/login"
      httpMethod="post"
      :onClick.prop="handleClick"
    >
    </nostr-one>
    <div class="mockup-code max-w-full">
      <pre
        data-prefix="~"
      ><code>{{ tokenResult || 'Click on "Login with Nostr" button' }}</code></pre>
    </div>
    <div v-if="tokenResult">⬇️</div>
    <div v-if="tokenResult" class="mockup-code text-left max-w-full">
      <pre><code>{{ tokenDecoded }}</code></pre>
    </div>
  </div>
</template>

<script setup lang="ts">
import "nostr-one";
import { computed, ref } from "vue";
import { Buffer } from "buffer";

const tokenResult = ref("");
const code = ref(
  `<nostr-one
loginUrl="https://test.com"
httpMethod="get"
:onClick.prop="handleClick"
:onError.prop="handleError"
:onSuccess.prop="handleSuccess"
>
</nostr-one>`
);

const tokenDecoded = computed(() => {
  if (!tokenResult.value) return "";
  const obj = JSON.parse(
    Buffer.from(tokenResult.value, "base64").toString("utf-8")
  );
  return JSON.stringify(obj, null, 4);
});

async function handleClick(token: string) {
  console.log(token);
  tokenResult.value = token;
}
</script>
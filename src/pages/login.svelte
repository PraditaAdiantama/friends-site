<script>
  import discordSDK from "@/utils/discord";
  import { onMount } from "svelte";

  onMount(async () => {
    handleDiscordCode();
  });

  async function handleDiscordCode() {
    const code = new URLSearchParams(location.search).get("code");
    if (!code) return;

    const data = await discordSDK().getToken(code);

    localStorage.setItem("token", data.access_token);
    if(data.access_token){
      location.href = "/"
    }
  }
</script>

<main class="w-full h-screen flex justify-center items-center">
  <div class="card bg-base-200 border border-base-300">
    <div class="card-body">
      <h3 class="card-title">Login to your account</h3>
      <p class="text-muted">
        Please login to your discord account to access dashboard.
      </p>
      <button
        class="mt-3 btn btn-primary"
        onclick={() => {
          location.href =
            "https://discord.com/oauth2/authorize?client_id=1089840401994748044&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%3A5173%2Flogin&scope=identify";
        }}
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          style="fill: rgba(0, 0, 0, 1);transform: ;msFilter:;"
          ><path
            d="M14.82 4.26a10.14 10.14 0 0 0-.53 1.1 14.66 14.66 0 0 0-4.58 0 10.14 10.14 0 0 0-.53-1.1 16 16 0 0 0-4.13 1.3 17.33 17.33 0 0 0-3 11.59 16.6 16.6 0 0 0 5.07 2.59A12.89 12.89 0 0 0 8.23 18a9.65 9.65 0 0 1-1.71-.83 3.39 3.39 0 0 0 .42-.33 11.66 11.66 0 0 0 10.12 0q.21.18.42.33a10.84 10.84 0 0 1-1.71.84 12.41 12.41 0 0 0 1.08 1.78 16.44 16.44 0 0 0 5.06-2.59 17.22 17.22 0 0 0-3-11.59 16.09 16.09 0 0 0-4.09-1.35zM8.68 14.81a1.94 1.94 0 0 1-1.8-2 1.93 1.93 0 0 1 1.8-2 1.93 1.93 0 0 1 1.8 2 1.93 1.93 0 0 1-1.8 2zm6.64 0a1.94 1.94 0 0 1-1.8-2 1.93 1.93 0 0 1 1.8-2 1.92 1.92 0 0 1 1.8 2 1.92 1.92 0 0 1-1.8 2z"
          ></path></svg
        >
        Login with Discord</button
      >
    </div>
  </div>
</main>

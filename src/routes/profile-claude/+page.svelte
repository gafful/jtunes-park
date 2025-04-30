<!-- src/routes/+page.svelte -->
<script lang="ts">
  import { Button } from "bits-ui";
  import { Input } from "../../components/ui/input";

  let name = "";
  let email = "affulgodfred@gmail.com";
  let dateOfBirth = "";

  const handleUpdateAccount = () => {
    // Handle update logic
    console.log("Updating account...");
  };

  const handleSendResetEmail = () => {
    // Handle send reset email logic
    console.log("Sending password reset email...");
  };
</script>

<div class="min-h-screen bg-slate-50 pb-20">
  <!-- Header -->
  <header class="bg-white border-b border-gray-200 py-4 px-4">
    <div class="max-w-7xl mx-auto flex justify-between items-center">
      <div class="text-2xl font-bold text-purple-600">JobTunes</div>
      <button class="text-2xl">☰</button>
    </div>
  </header>

  <main class="max-w-2xl mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-center mb-10">Account Settings</h1>

    <section class="mb-12">
      <h2 class="text-2xl font-bold mb-6">My Account</h2>

      <div class="mb-6">
        <label for="name" class="block text-lg font-medium mb-2">Name</label>
        <Input
          id="name"
          type="text"
          bind:value={name}
          placeholder="Your name"
          class="w-full p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
        <p class="text-gray-500 mt-2">This is the name that will be displayed on your profile and in emails.</p>
      </div>

      <div class="mb-6">
        <label for="email" class="block text-lg font-medium mb-2">Email</label>
        <Input
          id="email"
          type="email"
          bind:value={email}
          class="w-full p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
      </div>

      <div class="mb-6">
        <label for="dob" class="block text-lg font-medium mb-2">Date of birth</label>
        <Input
          id="dob"
          type="date"
          bind:value={dateOfBirth}
          class="w-full p-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-purple-500"
        />
        <p class="text-gray-500 mt-2">Your date of birth is used to calculate your age.</p>
      </div>

      <Button.Root
        onclick={handleUpdateAccount}
        class="w-full bg-black text-white py-4 rounded-lg font-medium text-lg"
      >
        Update account
      </Button.Root>
    </section>

    <section class="mb-12">
      <h2 class="text-2xl font-bold mb-6">Change Password</h2>
      <h3 class="text-xl font-bold mb-4">Change Password By Email</h3>
      <p class="text-gray-500 mb-6">
        The button below will send you an email at {email} which will allow you to set your password.
      </p>
      <Button.Root
        onclick={handleSendResetEmail}
        class="w-full bg-black text-white py-4 rounded-lg font-medium text-lg"
      >
        Send Set Password Email
      </Button.Root>
    </section>
  </main>
</div>
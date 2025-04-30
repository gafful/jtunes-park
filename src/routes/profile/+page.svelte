<script lang="ts">
  import { getContext } from "svelte"
  import type { Writable } from "svelte/store"
  import { Label } from "bits-ui"
  import { Button } from "bits-ui";
  import { Input } from "../../components/ui/input";
  // import { getApiUrl } from "$lib/api"
  // import { storage } from "$lib/storage"
  // import SettingsModule from "./settings_module.svelte"

  // let adminSection: Writable<string> = getContext("adminSection")
  // adminSection.set("profile")

  let { data } = $props()
  let { user, supabase } = data
  let profile = $state({
    full_name: "",
    job_position: "",
    years_of_experience: "",
    industry: "",
    location: "",
    current_cv: "",
    updated_at: "",
    date_of_birth: "",
  })

  // // Add effect to fetch profile data
  // $effect(() => {
  //   void (async () => {
  //     try {
  //       let sessionHeaders = {}
  //       try {
  //         const storedSession = await storage.getItem("supabase:session")
  //         if (storedSession) {
  //           const fullSession = JSON.parse(storedSession)
  //           sessionHeaders = {
  //             Authorization: `Bearer ${fullSession.access_token}`,
  //             "Content-Type": "application/json",
  //             Accept: "application/json",
  //           }
  //         }
  //       } catch (error) {
  //         console.error("Error getting session from storage:", error)
  //       }

  //       const response = await fetch(`${getApiUrl()}/account/api/profile`, {
  //         method: "GET",
  //         headers: sessionHeaders,
  //         credentials: "include",
  //       })

  //       if (!response.ok) {
  //         console.error("Failed to fetch profile data:", response.status)
  //         return
  //       }

  //       const { profile: profileData } = await response.json()
  //       if (profileData) {
  //         // Update profile state with new data
  //         profile = {
  //           ...profile,
  //           ...profileData,
  //         }
  //         console.log("Profile data updated:", profile)
  //       }
  //     } catch (error) {
  //       console.error("Error fetching profile data:", error)
  //     }
  //   })()
  // })

  // @ts-expect-error: we ignore because Supabase does not maintain an AMR typedef
  let hasPassword = user?.amr?.find((x) => x.method === "password")
    ? true
    : false

  // @ts-expect-error: we ignore because Supabase does not maintain an AMR typedef
  let usingOAuth = user?.amr?.find((x) => x.method === "oauth") ? true : false

  let sendBtn: HTMLButtonElement = $state()
  let sentEmail = $state(false)
  let sendForgotPassword = async () => {
  //   try {
  //     sendBtn.disabled = true
  //     sendBtn.textContent = "Sending..."
  //     const apiUrl = getApiUrl()

  //     let sessionHeaders = {}
  //     try {
  //       const storedSession = await storage.getItem("supabase:session")
  //       if (storedSession) {
  //         const session = JSON.parse(storedSession)
  //         sessionHeaders = {
  //           Authorization: `Bearer ${session.access_token}`,
  //         }
  //       }
  //     } catch (error) {
  //       console.error("Error getting session from storage:", error)
  //     }

  //     const response = await fetch(`${apiUrl}/account/api/forgot_password`, {
  //       method: "POST",
  //       headers: {
  //         Accept: "application/json",
  //         "Content-Type": "application/json",
  //         "x-sveltekit-action": "true",
  //         ...sessionHeaders,
  //       },
  //       body: JSON.stringify({ email: user?.email }),
  //     })

  //     const data = await response.json()
  //     sentEmail = response.ok

  //     if (!response.ok) {
  //       throw new Error(data.error || "Failed to send reset email")
  //     }
  //   } catch (error) {
  //     console.error("Error sending reset email:", error)
  //     sentEmail = false
  //   } finally {
  //     sendBtn.disabled = false
  //     sendBtn.textContent = "Send Set Password Email"
  //   }
  }

  let loading = $state(false)
  let errorMessage = $state("")
  let successMessage = $state("")

  let form: HTMLFormElement

  async function handleProfileUpdate(event: SubmitEvent) {
    event.preventDefault()
    // loading = true
    // errorMessage = ""
    // successMessage = ""

    // try {
    //   const apiUrl = getApiUrl()

    //   let sessionHeaders = {}
    //   try {
    //     const storedSession = await storage.getItem("supabase:session")
    //     if (storedSession) {
    //       const session = JSON.parse(storedSession)
    //       sessionHeaders = {
    //         Authorization: `Bearer ${session.access_token}`,
    //       }
    //     }
    //   } catch (error) {
    //     console.error("Error getting session from storage:", error)
    //   }

    //   // Create FormData from the form
    //   const formData = new FormData(form)

    //   // Log form data for debugging
    //   console.log("Form data being sent:", Object.fromEntries(formData))

    //   const response = await fetch(`${apiUrl}/account/api/profile`, {
    //     method: "POST",
    //     body: formData,
    //     credentials: "include",
    //     headers: {
    //       Accept: "application/json",
    //       "x-sveltekit-action": "true",
    //       ...sessionHeaders,
    //     },
    //   })

    //   console.log("Response status:", response.status)
    //   const responseText = await response.text()
    //   console.log("Response text:", responseText)

    //   try {
    //     const result = JSON.parse(responseText)
    //     if (!response.ok) {
    //       throw new Error(result.error || "Failed to update profile")
    //     }

    //     // Update local state with returned profile data
    //     if (result.profile) {
    //       profile = result.profile
    //       // Force a UI update
    //       profile = { ...profile }
    //     }

    //     successMessage = result.message || "Profile updated successfully!"
    //   } catch (parseError) {
    //     console.error("Error parsing JSON:", parseError)
    //     throw new Error("Invalid response from server")
    //   }
    // } catch (error) {
    //   errorMessage = error.message
    // } finally {
    //   loading = false
    // }
  }
</script>

<svelte:head>
  <title>Account Settings</title>
</svelte:head>

<div class="max-w-3xl 2xl:max-w-6xl mx-auto max-lg:pt-16">
  <h1 class="text-2xl md:text-5xl text-center font-bold font-ibm mb-8 font-ibm">
    Account Settings
  </h1>

  <div class="grid grid-cols-1 md:grid-cols-2 gap-x-8 gap-y-12">
    <!-- My Account Section -->
    <div>
      <h2 class="text-xl font-semibold font-ibm mb-6">My Account</h2>
      <form
        class="space-y-6 font-inter"
        
        onsubmit={handleProfileUpdate}
      >
        <div class="space-y-2">
          <Label.Root for="fullName">Name</Label.Root>
          <Input
            id="fullName"
            name="fullName"
            value={profile?.full_name ?? ""}
            placeholder="Your name"
            class="border-gray-300 text-[#71717A] drop-shadow"
          />
          <p class="text-sm text-muted-foreground">
            This is the name that will be displayed on your profile and in
            emails.
          </p>
        </div>

        <div class="space-y-2 font-inter">
          <Label.Root for="email">Email</Label.Root>
          <Input
            id="email"
            name="email"
            value={user?.email ?? ""}
            placeholder="Your email"
            disabled={user?.app_metadata?.provider !== "email"}
            class="border-gray-300 text-[#71717A] drop-shadow"
          />
          {#if user?.app_metadata?.provider !== "email"}
            <p class="text-sm text-muted-foreground">
              Email cannot be changed for accounts created with social login.
            </p>
          {/if}
        </div>

        <div class="space-y-2 font-inter">
          <Label.Root for="dob">Date of birth</Label.Root>
          <Input
            id="dob"
            name="dob"
            type="date"
            value={profile?.date_of_birth ?? ""}
            class="border-gray-300 text-[#71717A] drop-shadow inline-block w-full"
          />
          <p class="text-sm text-muted-foreground">
            Your date of birth is used to calculate your age.
          </p>
        </div>

        {#if errorMessage}
          <p class="text-destructive text-sm font-medium">{errorMessage}</p>
        {/if}

        {#if successMessage}
          <p class="text-green-600 text-sm font-medium">{successMessage}</p>
        {/if}

        <Button.Root
          type="submit"
          disabled={loading}
          class="bg-black hover:bg-black/90 text-white w-full md:w-fit"
        >
          {loading ? "Updating..." : "Update account"}
        </Button.Root>
      </form>
    </div>

    <!-- Change Password Section -->
    <div class="font-inter">
      <h2 class="text-xl font-semibold font-ibm mb-6">Change Password</h2>
      {#if hasPassword}
        <form
          class="space-y-6"
          action="/account/api?/updatePassword"
          method="POST"
        >
          <div class="space-y-2 font-inter">
            <Label.Root for="currentPassword">Current Password</Label.Root>
            <Input
              id="currentPassword"
              name="currentPassword"
              type="password"
              placeholder="••••••••"
            />
          </div>

          <div class="space-y-2 font-inter">
            <Label.Root for="newPassword1">New Password</Label.Root>
            <Input
              id="newPassword1"
              name="newPassword1"
              type="password"
              placeholder="••••••••"
            />
          </div>

          <div class="space-y-2 font-inter">
            <Label.Root for="newPassword2">Repeat New Password</Label.Root>
            <Input
              id="newPassword2"
              name="newPassword2"
              type="password"
              placeholder="••••••••"
            />
          </div>

          <Button.Root type="submit">Change Password</Button.Root>
        </form>
      {:else}
        <div class="space-y-4">
          {#if usingOAuth}
            <div class="font-bold font-inter">Set Password By Email</div>
            <div class="text-sm text-[#71717A] font-inter">
              You use oAuth to sign in ("Sign in with Google" or similar). You
              can continue to access your account using only oAuth if you like!
            </div>
          {:else}
            <div class="font-bold font-inter">Change Password By Email</div>
          {/if}
          <div class="text-sm text-[#71717A] font-inter">
            The button below will send you an email at {user?.email} which will allow
            you to set your password.
          </div>
          <Button.Root
            class="{sentEmail
              ? 'hidden'
              : ''} bg-black hover:bg-black/90 text-white w-full md:w-fit"
            bind:this={sendBtn}
            onclick={sendForgotPassword}
          >
            Send Set Password Email
          </Button.Root>
          <div
            class="bg-green-100 text-green-800 p-4 rounded-md {sentEmail
              ? ''
              : 'hidden'}"
          >
            Sent email! Please check your inbox and use the link to set your
            password.
          </div>
          <div class="font-bold font-inter">Danger Zone</div>
          <!-- <SettingsModule
            class="!bg-transparent  !justify-start"
            editable={false}
            dangerous={true}
            fields={[]}
            editButtonTitle="Delete Account"
            editLink="/account/profile/delete_account"
          /> -->
        </div>
      {/if}
    </div>
  </div>
</div>

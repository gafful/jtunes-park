<script lang="ts">
  import { Calendar, Upload } from "lucide-svelte"

  let isUploading = $state(false)
    // CV store for a single CV
    let cv = $state({
    title: "My CV",
    description: "No CV uploaded yet",
    date: "",
  })

  let profile = $state({
    full_name: "",
    job_position: "",
    years_of_experience: "",
    industry: "",
    location: "",
    current_cv: "",
    updated_at: "",
  })

  async function handleCvUpload(event: Event) {
    event.preventDefault()
  }
</script>
<div class="max-w-3xl 2xl:max-w-6xl mx-auto px-4">
  <section class="mx-auto px-4 max-lg:pt-16">
    <h1 class="mb-8 text-center text-2xl md:text-5xl font-bold font-ibm">
      My CV
    </h1>

    <div class="flex flex-wrap gap-4 items-start font-inter">
      <!-- Existing CV -->
      <div
        class="flex-1 rounded-lg border bg-white p-6 shadow-sm relative flex flex-col gap-4"
      >
        {#if isUploading}
          <div
            class="absolute inset-0 bg-white/50 backdrop-blur-sm rounded-md z-10 flex items-center justify-center"
          >
            <div class="flex flex-col items-center gap-2">
              <div class="spinner scale-50">
                <div></div>
                <div></div>
                <div></div>
                <div></div>
                <div></div>
              </div>
            </div>
          </div>
        {/if}
        <div class="flex flex-col gap-2 {isUploading ? 'blur-[2px]' : ''}">
          <h2 class="text-xl font-semibold">
            {cv.title.length > 20 ? cv.title.slice(0, 20) + "..." : cv.title}
          </h2>
          <p class="text-gray-500">{cv.description}</p>
          <div class="flex items-center gap-2 text-gray-500">
            <Calendar class="h-4 w-4" />
            <span>{cv.date}</span>
          </div>
        </div>
        <!-- New CV Button -->
        <div class="mt-4 md:absolute md:top-4 md:right-4 md:mt-0">
          <label
            for="cv-upload"
            class="inline-flex cursor-pointer items-center justify-center gap-2 rounded-lg bg-gray-100 px-16 py-3 font-medium hover:bg-gray-200 w-full md:w-auto"
          >
            <Upload class="h-5 w-5" />
            New CV
          </label>
          <input
            id="cv-upload"
            type="file"
            accept=".pdf"
            class="hidden"
            onchange={handleCvUpload}
          />
          <p class="text-xs text-gray-500 mt-1 text-center md:text-right">
            Max size: 5MB
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Profile Section -->
  <div>
    <h2 class="mb-8 text-center text-xl font-bold my-4 font-ibm">Profile</h2>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 font-inter">
      <!-- Left Column -->
      <div class="space-y-4">
        <div>
          <label for="name" class="block text-sm font-medium text-gray-700"
            >Name</label
          >
          <input
            type="text"
            id="name"
            class="mt-1 w-full rounded-lg border border-[#BAB9FF] bg-gray-100 px-4 py-2 focus:outline-none text-slate-500 drop-shadow"
            value={profile?.full_name ||
              "Upload Your CV to Display Information"}
            readonly
          />
        </div>
        <div>
          <label
            for="job-position"
            class="block text-sm font-medium text-gray-700">Job Position</label
          >
          <input
            type="text"
            id="job-position"
            class="mt-1 w-full rounded-lg border border-[#BAB9FF] bg-gray-100 px-4 py-2 focus:outline-none text-slate-500 drop-shadow"
            value={profile?.job_position ||
              "Upload Your CV to Display Information"}
            readonly
          />
        </div>
        <div>
          <label for="location" class="block text-sm font-medium text-gray-700"
            >Location</label
          >
          <input
            type="text"
            id="location"
            class="mt-1 w-full rounded-lg border border-[#BAB9FF] bg-gray-100 px-4 py-2 focus:outline-none text-slate-500 drop-shadow"
            value={profile?.location || "Upload Your CV to Display Information"}
            readonly
          />
        </div>
      </div>

      <!-- Right Column -->
      <div class="space-y-4">
        <div>
          <label
            for="experience"
            class="block text-sm font-medium text-gray-700"
            >Years of Experience</label
          >
          <input
            type="text"
            id="experience"
            class="mt-1 w-full rounded-lg border border-[#BAB9FF] bg-gray-100 px-4 py-2 focus:outline-none text-slate-500 drop-shadow"
            value={profile?.years_of_experience ||
              "Upload Your CV to Display Information"}
            readonly
          />
        </div>
        <div>
          <label for="industry" class="block text-sm font-medium text-gray-700"
            >Industry</label
          >
          <input
            type="text"
            id="industry"
            class="mt-1 w-full rounded-lg border border-[#BAB9FF] bg-gray-100 px-4 py-2 focus:outline-none text-slate-500 drop-shadow"
            value={profile?.industry || "Upload Your CV to Display Information"}
            readonly
          />
        </div>
      </div>
    </div>
  </div>
</div>
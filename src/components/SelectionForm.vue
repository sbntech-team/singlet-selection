<template>
  <div class="mt-2 p-2 md:p-8">
    <div class="my-4">
      <Listbox v-model="selectedUnit">
        <div class="relative mt-1">
          <label class="pl-1 pb-1">Unit:</label>
          <ListboxButton
            class="relative w-full py-2 pl-3 pr-10 text-left bg-white rounded-lg shadow-md cursor-default focus:outline-none focus-visible:ring-2 focus-visible:ring-opacity-75 focus-visible:ring-white focus-visible:ring-offset-orange-300 focus-visible:ring-offset-2 focus-visible:border-indigo-500 sm:text-sm"
          >
            <span class="block truncate">{{ selectedUnit.displayName }}</span>
            <span
              class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none"
            >
              <SelectorIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
            </span>
          </ListboxButton>
          <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
          >
            <ListboxOptions
              class="absolute w-full py-1 mt-1 overflow-auto text-base bg-white rounded-md shadow-lg max-h-60 ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm z-10"
            >
              <ListboxOption
                v-slot="{ active, selected }"
                as="template"
                v-for="unit in units"
                :key="unit.folderName"
                :value="unit"
              >
                <li
                  :class="[
                    active ? 'text-blue-900 bg-blue-100' : 'text-gray-900',
                    'cursor-default select-none relative py-2 pl-10 pr-4',
                  ]"
                >
                  <span
                    :class="[
                      selected ? 'font-medium' : 'font-normal',
                      'block truncate',
                    ]"
                  >
                    {{ unit.displayName }}
                  </span>
                  <span
                    v-if="selected"
                    class="absolute inset-y-0 left-0 flex items-center pl-3 text-blue-600"
                  >
                    <CheckIcon class="w-5 h-5" aria-hidden="true" />
                  </span>
                </li>
              </ListboxOption>
            </ListboxOptions>
          </transition>
        </div>
      </Listbox>
    </div>
    <div class="my-4">
      <Listbox v-model="selectedDesign">
        <div class="relative mt-1">
          <label class="pl-1 pb-1">Design:</label>
          <ListboxButton
            class="relative w-full py-2 pl-3 pr-10 text-left bg-white rounded-lg shadow-md cursor-default focus:outline-none focus-visible:ring-2 focus-visible:ring-opacity-75 focus-visible:ring-white focus-visible:ring-offset-orange-300 focus-visible:ring-offset-2 focus-visible:border-indigo-500 sm:text-sm"
          >
            <span class="block truncate">{{ selectedDesign.displayName }}</span>
            <span
              class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none"
            >
              <SelectorIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
            </span>
          </ListboxButton>
          <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
          >
            <ListboxOptions
              class="absolute w-full py-1 mt-1 overflow-auto text-base bg-white rounded-md shadow-lg max-h-60 ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm"
            >
              <ListboxOption
                v-slot="{ active, selected }"
                as="template"
                v-for="design in designs"
                :key="design.folderName"
                :value="design"
              >
                <li
                  :class="[
                    active ? 'text-blue-900 bg-blue-100' : 'text-gray-900',
                    'cursor-default select-none relative py-2 pl-10 pr-4',
                  ]"
                >
                  <span
                    :class="[
                      selected ? 'font-medium' : 'font-normal',
                      'block truncate',
                    ]"
                  >
                    {{ design.displayName }}
                  </span>
                  <span
                    v-if="selected"
                    class="absolute inset-y-0 left-0 flex items-center pl-3 text-blue-600"
                  >
                    <CheckIcon class="w-5 h-5" aria-hidden="true" />
                  </span>
                </li>
              </ListboxOption>
            </ListboxOptions>
          </transition>
        </div>
      </Listbox>
    </div>
    <img
      :src="
        images[
          `/src/assets/${selectedUnit.folderName}/${selectedDesign.fileName}`
        ].default
      "
      class="my-4 mx-auto"
      alt="Singlet Image"
    />
    <a
      type="button"
      class="focus:outline-none text-white text-sm py-2.5 px-5 rounded-md bg-green-500 hover:bg-green-600 hover:shadow-lg w-full text-center flex justify-center items-center"
      href="/"
    >
      <span>Go to form</span>
      <ExternalLinkIcon class="w-5 h-5 ml-1 inline-block" />
    </a>
  </div>
</template>

<script setup>
import { ref } from "vue";
import {
  Listbox,
  ListboxButton,
  ListboxOptions,
  ListboxOption,
} from "@headlessui/vue";
import {
  CheckIcon,
  SelectorIcon,
  ExternalLinkIcon,
} from "@heroicons/vue/solid";

const units = [
  { displayName: "2 PDF", folderName: "2_PDF" },
  { displayName: "3 DIV", folderName: "3_DIV" },
  { displayName: "6 DIV", folderName: "6_DIV" },
  { displayName: "9 DIV", folderName: "9_DIV" },
  { displayName: "Armour", folderName: "Armour" },
  { displayName: "Army Intel", folderName: "Army_Intel" },
  { displayName: "Army Specialist", folderName: "Army_Specialist" },
  { displayName: "Artillery", folderName: "Artillery" },
  { displayName: "Commando", folderName: "Commando" },
  { displayName: "CSS Command", folderName: "CSS_Command" },
  { displayName: "Engineer", folderName: "Engineer" },
  { displayName: "General Staff", folderName: "General_Staff" },
  { displayName: "Guards", folderName: "Guards" },
  { displayName: "Joint Services", folderName: "Joint_Services" },
  { displayName: "MIO", folderName: "MIO" },
  { displayName: "PERSCOM", folderName: "PERSCOM" },
  { displayName: "SAF C4I", folderName: "SAF_C4I" },
  { displayName: "SAF_Medical Corps", folderName: "SAF_Medical_Corps" },
  { displayName: "SAF MP Command", folderName: "SAF_MP_Command" },
  { displayName: "SAF Volunteer Corps", folderName: "SAF_Volunteer_Corps" },
  { displayName: "SAFTI MI", folderName: "SAFTI_MI" },
  { displayName: "Sense Strike", folderName: "Sense_Strike" },
  { displayName: "Signal", folderName: "Signal" },
];
const designs = [
  { displayName: "1", fileName: "Design_1.png" },
  { displayName: "2", fileName: "Design_2.png" },
  { displayName: "3", fileName: "Design_3.png" },
  { displayName: "4", fileName: "Design_4.png" },
];
const selectedUnit = ref(units[0]);
const selectedDesign = ref(designs[0]);
const images = import.meta.globEager("/src/assets/*/*.png");
</script>

<style scoped>
</style>
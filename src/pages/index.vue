<script setup lang="ts">
import { drugs } from '~/data/drugs'

const filter = ref('')
const selectedDrug = ref({
  pct: 0,
  name: '',
  pub_price: 0,
  ref_price: 0,
  category: '',
  dci: '',
  ap: '',
})

const filtered = computed(() => drugs.filter(item => item.name.toLowerCase().includes(filter.value.toLowerCase())))

const { t } = useI18n()

function showDrug(pct: number) {
  const index = drugs.findIndex(item => item.pct === pct)
  selectedDrug.value = drugs[index]
}
</script>

<template>
  <div>
    <p class="text-4xl">
      <carbon-pills class="inline-block" />
    </p>
    <p>
      <a rel="noreferrer" href="#">
        PrixMédoc
      </a>
    </p>
    <p>
      <em class="text-sm opacity-75">{{ t('intro.desc') }}</em>
    </p>
    <p>
      <em class="text-sm opacity-75">{{ t('intro.updated') }} 10-02-2022</em>
    </p>

    <div class="py-4" />

    <input
      id="input"
      v-model="filter"
      :placeholder="t('intro.search')"
      :aria-label="t('intro.search')"
      type="text"
      autocomplete="false"
      p="x-4 y-2"
      m="y-4"
      w="250px"
      bg="transparent"
      border="~ rounded gray-200 dark:gray-700"
      outline="none active:none"
    >
    <div class="flex flex-col">
      <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block py-2 min-w-full sm:px-6 lg:px-8">
          <div class="overflow-hidden shadow-md sm:rounded-lg">
            <table class="table-auto w-full rounded-lg">
              <thead class="bg-gray-100 dark:bg-gray-700">
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  PCT
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  Désignation
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  Prix Publique
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  Prix Référence
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  Catégorie
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  DCI
                </th>
                <th scope="col" class="py-3 px-6 text-xs font-medium tracking-wider text-left text-gray-700 uppercase dark:text-gray-400">
                  AP
                </th>
              </thead>
              <tbody v-for="drug in filtered" :key="drug.pct">
                <tr
                  class="border-b odd:bg-white even:bg-gray-50 odd:dark:bg-gray-800 even:dark:bg-gray-700 dark:border-gray-600 hover:bg-lime-200 dark:hover:bg-lime-700"
                  @click="showDrug(drug.pct)"
                >
                  <td class="py-4 px-6 text-sm text-gray-900 text-left  dark:text-white">
                    {{ drug.pct }}
                  </td>
                  <td class="py-4 px-6 text-sm font-medium text-left text-gray-900  dark:text-white">
                    {{ drug.name }}
                  </td>
                  <td class="py-4 px-6 text-sm text-gray-900 text-left  dark:text-white">
                    {{ drug.pub_price }}
                  </td>
                  <td class="py-4 px-6 text-sm text-gray-900 text-left  dark:text-white">
                    {{ drug.ref_price }}
                  </td>
                  <td class="py-4 px-6 text-sm text-gray-900 text-left  dark:text-white">
                    {{ drug.category }}
                  </td>
                  <td class="py-4 px-6 text-sm text-left text-gray-900  dark:text-white">
                    {{ drug.dci }}
                  </td>
                  <td class="py-4 px-6 text-sm text-gray-900 text-left  dark:text-white">
                    {{ drug.ap }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<route lang="yaml">
meta:
  layout: home
</route>

<script setup>
import trophy from '@images/misc/trophy.png'
import arrowGrowth from '@images/cards/arrow-growth.png'
import atmCard from '@images/cards/atm-card.png'
import creditCard from '@images/cards/credit-card.png'
import paypal from '@images/cards/paypal.png'
import wallet from '@images/cards/wallet.png'
import { kFormatter } from '@core/utils/formatters'

import VueApexCharts from 'vue3-apexcharts'
import { useTheme } from 'vuetify'
import { useThemeConfig } from '@core/composable/useThemeConfig'
import { hexToRgb } from '@layouts/utils'

const vuetifyTheme = useTheme()
const { theme } = useThemeConfig()

const options = controlledComputed(theme, () => {
  const currentTheme = ref(vuetifyTheme.current.value.colors)
  const variableTheme = ref(vuetifyTheme.current.value.variables)
  const secondaryTextColor = `rgba(${ hexToRgb(currentTheme.value['on-surface']) },${ variableTheme.value['medium-emphasis-opacity'] })`
  const primaryTextColor = `rgba(${ hexToRgb(currentTheme.value['on-surface']) },${ variableTheme.value['high-emphasis-opacity'] })`
  
  return {
    chart: { sparkline: { enabled: true } },
    colors: [
      currentTheme.value.primary,
      `rgba(${ hexToRgb(currentTheme.value.primary) }, 0.7)`,
      `rgba(${ hexToRgb(currentTheme.value.primary) }, 0.5)`,
      currentTheme.value.background,
    ],
    stroke: { width: 0 },
    legend: { show: false },
    dataLabels: { enabled: false },
    labels: [
      'Apparel',
      'Electronics',
      'FMCG',
      'Other Sales',
    ],
    states: {
      hover: { filter: { type: 'none' } },
      active: { filter: { type: 'none' } },
    },
    plotOptions: {
      pie: {
        customScale: 0.9,
        donut: {
          size: '70%',
          labels: {
            show: true,
            name: {
              offsetY: 25,
              color: secondaryTextColor,
            },
            value: {
              offsetY: -15,
              fontWeight: 600,
              fontSize: '24px',
              color: primaryTextColor,
              formatter: value => `${ value }k`,
            },
            total: {
              show: true,
              label: 'Weekly Sales',
              fontSize: '12px',
              color: secondaryTextColor,
              formatter: value => `${ value.globals.seriesTotals.reduce((total, num) => total + num) }k`,
            },
          },
        },
      },
    },
  }
})

const series = [
  12,
  25,
  13,
  50,
]

const salesOverviews = [
  {
    product: 'Apparel',
    sales: '$1,840',
  },
  {
    product: 'Electronic',
    sales: '$11,420',
  },
  {
    product: 'FMCG',
    sales: '$1,840',
  },
  {
    product: 'Other Sales',
    sales: '$11,420',
  },
]

const transactions = [
  {
    gateway: 'Paypal',
    for: 'Freelance Work',
    amount: 2482,
    img: paypal,
  },
  {
    gateway: 'Credit Card',
    for: 'Digital Ocean',
    amount: -1250,
    img: creditCard,
  },
  {
    gateway: 'Mastercard',
    for: 'Netflix',
    amount: -99,
    img: atmCard,
  },
  {
    gateway: 'Wallet',
    for: 'Mac\'D',
    amount: -82,
    img: wallet,
  },
  {
    gateway: 'Transfer',
    for: 'Refund',
    amount: 8934,
    img: arrowGrowth,
  },
]

const transactionsColors = {
  'Paypal': 'error',
  'Credit Card': 'success',
  'Mastercard': 'warning',
  'Wallet': 'primary',
  'Transfer': 'info',
}

const formateAmount = amount => {
  return Math.sign(amount) === 1 ? `+${ kFormatter(amount) }` : `-${ Math.abs(amount) }`
}

const statistics = [
    {
        title: 'Pesanan Baru',
        stats: '2450',
        icon: 'mdi-trending-up',
        color: 'primary',
    },
    {
        title: 'Siap Proses',
        stats: '125',
        icon: 'material-symbols:order-approve-outline-sharp',
        color: 'success',
    },
    {
        title: 'Dalam Proses',
        stats: '154',
        icon: 'game-icons:box-unpacking',
        color: 'warning',
    },
    {
        title: 'Siap Kirim',
        stats: '88',
        icon: 'icon-park:delivery',
        color: 'info',
    },
    {
        title: 'Dikirim',
        stats: '1549',
        icon: 'tabler:truck',
        color: 'warning',
    },
    {
        title: 'Pembatalan',
        stats: '18',
        icon: 'tabler:truck-return',
        color: 'error',
    },
]

const totalOrder = {
    title: 'Total Order',
    icon: 'mdi-dollar',
    stats: '121.380',
    change: 42,
    color : "success",
    subtitle: 'Pesanan meningkat',
}

const totalPending = {
    title: 'Order Pending',
    icon: 'mdi-dollar',
    stats: '20',
    change: 12,
    color : "success",
    subtitle: 'Pesanan meningkat',
}

const totalOS = {
    title: 'Out of Stock',
    icon: 'mdi-dollar',
    stats: '120',
    change: 12,
    color : "success",
    subtitle: 'Pesanan meningkat',
}

const selectedMarketplace = ref('Tokopedia')
const selectedToko = ref('8Wood')

const marketplace = [
  'Tokopedia',
  'Shopee',
  'Tokopedia',
  'Bukalapak',
  'Jubelio',
]

const toko = [
  '8Wood',
  'CESSA'
]

const dateRange = ref('')

const salesByCountries = [
  {
    abbr: 'US',
    amount: '$8,656k',
    country: 'United states of america',
    change: '+25.8%',
    sales: '894k',
    color: 'success',
  },
  {
    abbr: 'UK',
    amount: '$2,415k',
    country: 'United kingdom',
    change: '-6.2%',
    sales: '645k',
    color: 'error',
  },
  {
    abbr: 'IN',
    amount: '$865k',
    country: 'India',
    change: '+12.4%',
    sales: '148k',
    color: 'warning',
  },
  {
    abbr: 'JA',
    amount: '$745k',
    country: 'Japan',
    change: '-11.9%',
    sales: '86k',
    color: 'secondary',
  },
  {
    abbr: 'KO',
    amount: '$45k',
    country: 'Korea',
    change: '+16.2%',
    sales: '42k',
    color: 'error',
  },
]
</script>

<template>
    <section>
        <VRow class="mb-2">
            <VCol cols="12" md="3" sm="6" class="d-flex flex-column align-self-end">
                <h3 class="pb-5">Marketplace</h3>
                <VCombobox
                    v-model="selectedMarketplace"
                    :items="marketplace"
                />
            </VCol>

            <VCol cols="12" md="3" sm="6" class="d-flex flex-column align-self-end">
                <h3 class="pb-5">Toko</h3>
                <VCombobox
                    v-model="selectedToko"
                    :items="toko"
                />
            </VCol>

            <VCol cols="12" md="4" sm="6" class="d-flex flex-column align-self-end">
                <h3 class="pb-5">Periode</h3>
                <AppDateTimePicker
                    v-model="dateRange"
                    label="Range"
                    :config="{ mode: 'range' }"
                />
            </VCol>

            <VCol cols="12" md="2" sm="6" class="d-flex flex-column align-self-end">
                <VBtn style="min-height:49px">
                    Atur
                </VBtn>
            </VCol>
        </VRow>

        <VRow class="mb-2">
            <VCol cols="12" md="3" sm="6" class="d-flex flex-column align-self-end"
                v-for="statistics in statisticsWithImages"
                :key="statistics.title"
            >
                <CardStatisticsWithImages v-bind="statistics" />
            </VCol>

            <VCol cols="12" md="6">
                <VCard title="Congratulations John! 🎉" subtitle="Best seller of the month" class="position-relative">
                    <VCardText>
                        <h5 class="text-2xl font-weight-medium text-primary">
                            Rp 42.243.343
                        </h5>
                        <p>78% of target 🚀</p>
                        <VBtn size="small">
                            Detail Penjualan
                        </VBtn>
                    </VCardText>

                    <!-- Trophy -->
                    <VImg :src="trophy" class="trophy"/>
                </VCard>
            </VCol>

            <VCol cols="12" md="2">
                <CardStatisticsVertical v-bind="totalOrder" :to="{ path: 'pages/apps/order' }" />
            </VCol>

            <VCol cols="12" md="2">
                <CardStatisticsVertical v-bind="totalPending" />
            </VCol>

            <VCol cols="12" md="2">
                <CardStatisticsVertical v-bind="totalOS" />
            </VCol>

            <VCol cols="12" md="12">
                <VCard title="Order Proses Per Status">
                    <VCardText>
                        <VRow>
                            <VCol cols="12" sm="2"
                                v-for="item in statistics"
                                :key="item.title"
                            >
                                <div class="d-flex align-center">
                                    <div class="me-3">
                                        <VAvatar :color="item.color" rounded size="44" class="elevation-1">
                                        <VIcon size="24" :icon="item.icon"/></VAvatar>
                                    </div>

                                    <div class="d-flex flex-column">
                                        <span class="text-caption">
                                            {{ item.title }}
                                        </span>
                                        <span class="text-h6">{{ item.stats }}</span>
                                    </div>
                                </div>
                            </VCol>
                        </VRow>
                    </VCardText>
                </VCard>
            </VCol>
        </VRow>

        <VRow class="mb-2">
            <VCol cols="12" md="4">
                <VCard>
                    <VCardItem>
                        <!-- 👉 Title -->
                        <VCardTitle>Transactions</VCardTitle>

                        <!-- 👉 menu -->
                        <template #append>
                            <div class="me-n3">
                            <VBtn
                                icon
                                size="x-small"
                                variant="text"
                                color="default"
                            >
                                <VIcon
                                size="24"
                                icon="mdi-dots-vertical"
                                />
                            </VBtn>
                            </div>
                        </template>
                    </VCardItem>
                    <!-- !SECTION -->

                    <!-- SECTION Transactions List -->
                    <VCardText>
                        <VList class="card-list">
                            <VListItem
                            v-for="transaction in transactions"
                            :key="transaction.for"
                            >
                            <!-- 👉 Avatar -->
                            <template #prepend>
                                <VAvatar
                                rounded
                                :color="transactionsColors[transaction.gateway]"
                                variant="tonal"
                                class="me-3"
                                >
                                <img
                                    width="20"
                                    :src="transaction.img"
                                    alt="transition"
                                >
                                </VAvatar>
                            </template>

                            <!-- 👉 Title and Subtitle  -->
                            <VListItemTitle class="font-weight-medium text-sm mb-1">
                                {{ transaction.gateway }}
                            </VListItemTitle>
                            <VListItemSubtitle class="text-xs">
                                {{ transaction.for }}
                            </VListItemSubtitle>

                            <!-- 👉 Amounts -->
                            <template #append>
                                <VListItemAction class="font-weight-medium">
                                <span class="text-base me-3">{{ formateAmount(transaction.amount) }}</span>
                                <VIcon
                                    :size="24"
                                    :color="Math.sign(transaction.amount) === 1 ? 'success' : 'error'"
                                    :icon="Math.sign(transaction.amount) === 1 ? 'mdi-chevron-up' : 'mdi-chevron-down'"
                                />
                                </VListItemAction>
                            </template>
                            </VListItem>
                        </VList>
                    </VCardText>
                </VCard>
            </VCol>

            <VCol cols="12" md="8">
                <VCard>
                    <VCardItem>
                    <VCardTitle>Sales Overview</VCardTitle>

                    <template #append>
                        <div class="me-n3">
                        <VBtn
                            icon
                            size="x-small"
                            color="default"
                            variant="text"
                        >
                            <VIcon
                            size="24"
                            icon="mdi-dots-vertical"
                            />
                        </VBtn>
                        </div>
                    </template>
                    </VCardItem>

                    <VCardText class="pt-4">
                    <VRow>
                        <VCol
                        sm="6"
                        cols="12"
                        >
                        <VueApexCharts
                            type="donut"
                            :options="options"
                            :series="series"
                            :height="220"
                        />
                        </VCol>

                        <VCol
                        cols="12"
                        sm="6"
                        >
                        <div class="d-flex align-center">
                            <div class="me-3">
                            <VAvatar
                                rounded
                                color="primary"
                                variant="tonal"
                            >
                                <VIcon icon="mdi-currency-usd" />
                            </VAvatar>
                            </div>

                            <div>
                            <p class="mb-0">
                                Number of Sales
                            </p>
                            <h6 class="text-h6">
                                $86,400
                            </h6>
                            </div>
                        </div>

                        <VDivider class="my-3" />
                        <VRow>
                            <VCol
                            v-for="sale in salesOverviews"
                            :key="sale.product"
                            cols="6"
                            >
                            <p class="mb-1">
                                <VIcon
                                icon="mdi-checkbox-blank-circle"
                                color="primary"
                                size="12"
                                class="me-2"
                                />
                                <span>{{ sale.product }}</span>
                            </p>
                            <p class="text-base font-weight-medium mb-0">
                                {{ sale.sales }}
                            </p>
                            </VCol>
                        </VRow>
                        </VCol>
                    </VRow>
                    </VCardText>
                </VCard>
            </VCol>
        </VRow>
    </section>
</template>

 <style lang="scss" scoped>
.card-list {
--v-card-list-gap: 1.5rem;
}
</style>

<style lang="scss">
@use "@layouts/styles/mixins" as layoutsMixins;

.trophy {
  position: absolute;
  inline-size: 4.9375rem;
  inset-block-end: 2rem;
  inset-inline-end: 2rem;
}

.flatpickr-input{
    padding-top: 10px;
}
</style>

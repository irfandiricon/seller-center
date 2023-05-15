<script setup>
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
        color: '#CC0000',
    },
]
</script>

<template>
    <VCard title="Order Proses Per Status" class="mt-5">
        <VCardText>
            <VRow>
                <VCol
                    v-for="item in statistics"
                    :key="item.title"
                    cols="12"
                    sm="2"
                >
                    <div class="d-flex align-center">
                        <div class="me-3">
                            <VAvatar
                                :color="item.color"
                                rounded
                                size="44"
                                class="elevation-1"
                            >
                            <VIcon
                                size="24"
                                :icon="item.icon"
                                color="white"
                            />
                            </VAvatar>
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
</template>

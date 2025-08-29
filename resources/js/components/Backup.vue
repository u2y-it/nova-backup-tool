<template>
    <tr :class="{ 'is-deleting': deleting }">
        <td class="px-2 py-2 border-t border-gray-100 dark:border-gray-700 whitespace-nowrap cursor-pointer dark:bg-gray-800 group-hover:bg-gray-50 dark:group-hover:bg-gray-900">{{ path }}</td>
        <td class="px-2 py-2 border-t border-gray-100 dark:border-gray-700 whitespace-nowrap cursor-pointer dark:bg-gray-800 group-hover:bg-gray-50 dark:group-hover:bg-gray-900">{{ date }}</td>
        <td class="px-2 py-2 border-t border-gray-100 dark:border-gray-700 whitespace-nowrap cursor-pointer dark:bg-gray-800 group-hover:bg-gray-50 dark:group-hover:bg-gray-900">{{ size }}</td>
        <td class="px-2 py-2 border-t border-gray-100 dark:border-gray-700 whitespace-nowrap cursor-pointer dark:bg-gray-800 group-hover:bg-gray-50 dark:group-hover:bg-gray-900 text-right flex items-center justify-center">
            <a
                :href="downloadUrl"
                target="_blank"
                rel="noopener nofollow"
                :title="__('Download')"
                class="inline-flex items-center justify-center h-9 text-gray-500 dark:text-gray-400 hover:[&:not(:disabled)]:text-primary-500 dark:hover:[&:not(:disabled)]:text-primary-500"
            >
                <icon type="download" view-box="0 0 24 24" width="24" height="24" />
            </a>
            <button
                :title="__('Restore')"
                class="inline-flex items-center justify-center h-9 text-gray-500 dark:text-gray-400 hover:[&:not(:disabled)]:text-primary-500 dark:hover:[&:not(:disabled)]:text-primary-500"
                @click.prevent="$emit('restore')"
            >
                <icon type="refresh" view-box="0 0 24 24" width="24" height="24" />
            </button>
            <button
                :title="__('Delete')"
                class="inline-flex items-center justify-center h-9 text-gray-500 dark:text-gray-400 hover:[&:not(:disabled)]:text-primary-500 dark:hover:[&:not(:disabled)]:text-primary-500"
                :class="deletable ? 'text-70 hover:text-primary' : 'cursor-default text-40'"
                :disabled="!deletable"
                v-if="deletable"
                @click.prevent="$emit('delete')"
            >
                <icon type="trash" view-box="0 0 24 24" width="24" height="24" />
            </button>
        </td>
    </tr>
</template>

<script setup>
import { Icon } from 'laravel-nova-ui';
import { computed } from 'vue';

const props = defineProps({
    date: { required: true },
    path: { required: true },
    size: { required: true },
    disk: { required: true },
    restorable: { required: true },
    deletable: { required: true },
    deleting: { required: true },
});

const downloadUrl = computed(() => {
    const endpoint = '/nova-vendor/spatie/backup-tool/download-backup';

    return `${endpoint}?disk=${props.disk}&path=${props.path}`;
});
</script>

<style scoped>
.is-deleting td {
    color: var(--60);
}
</style>

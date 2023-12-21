<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head } from '@inertiajs/vue3';
import { inject, ref } from 'vue';
import Card from '@/Components/Card.vue';

// Use 'discount' as the default value if 'discountValue' is not provided
const discountValue = inject('discountValue');
</script>

<template>
    <Head title="Dashboard" />



    <AuthenticatedLayout>
        <div class="py-12 fade-in">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900 dark:text-gray-100">
                    <!-- Loop All Plugins Created / Tailwind Modal Create / Tailwind Modal Edit / Tailwind Modal Delete -->


                    <div class="flex justify-end" style="">
                        <!-- <button> Discount </button> -->

                        <button @click="openCreateModal" class="bg-blue-600 p-3 rounded-lg hover:bg-blue-800 duration-200"><i class="fa fa-fish"></i> Add Fish</button>

                    </div>

                    <div>
                        <header style="font-size: 30px;"><i class="fa-solid fa-fish"></i> Fish Items</header>
                    </div> <br>
                    <div>
                        <!-- Loop All Plugin -->
                        <div class="bg-blue-700 p-8 text-white rounded-2xl">
    <form @submit.prevent="submitFilter" class="flex flex-col items-center mb-8">
        <div class="flex items-center mb-4">
            <label for="startDate" class="mr-2 text-lg">📅 Start Date:</label>
            <div class="relative">
                <input v-model="startDate" type="date" id="startDate" name="startDate"
                    class="text-black py-2 px-3 border border-gray-300 rounded-md focus:outline-none focus:border-blue-300">
                <span class="absolute right-3 top-2.5">
                    🗓️
                </span>
            </div>
        </div>

        <div class="flex items-center mb-4">
            <label for="endDate" class="mr-2 text-lg">📅 End Date:</label>
            <div class="relative">
                <input v-model="endDate" type="date" id="endDate" name="endDate"
                    class="text-black py-2 px-3 border border-gray-300 rounded-md focus:outline-none focus:border-blue-300">
                <span class="absolute right-3 top-2.5">
                    🗓️
                </span>
            </div>
        </div>

        <button type="submit" class="bg-green-500 text-white py-2 px-6 rounded-md hover:bg-green-700">
            🐠 Apply Filter
        </button>
    </form>

    <div v-for="plugin in plugins" :key="plugin.id" class="mb-8">
        <div class="flex justify-between bg-blue-500 p-6 rounded-lg shadow-lg">
            <div class="w-2/3">
                <Card>
                    <template #header>
                        <h2 class="mb-2 text-xl"><b>🐚 Name:</b> {{ plugin.name }}</h2>
                    </template>
                    <template #body>
                        <p class="mb-2"><b>🎵 Type:</b> {{ plugin.daws }}</p>
                        <p class="mb-2"><b>💰 Price:</b> ${{ plugin.price }}</p>
                    </template>

                    <template #footer>
                        <br> <hr> <br>
                        <div class="">
                            <div class="">
                                <b>📝 Description:</b>
                            </div>
                            <div class="p-3">
                                {{ plugin.description }}
                            </div>
                        </div>
                    </template>
                </Card>
            </div>
            <div class="flex items-center">
                <button @click="openEditModal(plugin)" class="text-yellow-400 p-3 hover:text-yellow-600">
                    ✏️ Edit
                </button>
                <button @click="deletePlugin(plugin.id)" class="text-red-400 p-3 hover:text-red-600">
                    🗑️ Delete
                </button>
            </div>
        </div>
    </div>
</div>



                    </div>

                    <!-- Create Modal -->
                    <div v-if="showCreateModal" class="fixed z-10 inset-0 overflow-y-auto">
                        <div class="flex items-center justify-center min-h-screen">
                            <div class="fixed inset-0 bg-black opacity-50"></div>
                            <div class="relative dark:bg-gray-800 w-96 p-6 rounded shadow-lg">
                                <h2 class="text-2xl font-bold mb-4">Create Fish</h2>

                                <!-- Add your form elements for creating a new plugin -->

                                <div class="flex justify-end mt-6">
                                    <form @submit.prevent="createPlugin">
                                        <div class="mb-4">
                                            <label for="name" class="text-sm font-medium text-gray-100">Name</label>
                                            <input style="width: 340px;" type="text" id="name" v-model="newPlugin.name" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="mb-4">
                                            <label for="description" class="block text-sm font-medium text-gray-100">Description</label>
                                            <textarea style="width: 340px;" id="description" v-model="newPlugin.description" class="mt-1 p-2 bg-transparent border-b-2 border-0" required></textarea>
                                        </div>

                                        <div class="mb-4">
                                            <label for="daws" class="block text-sm font-medium text-gray-100">Type</label>
                                            <input style="width: 340px;" type="text" id="daws" v-model="newPlugin.daws" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="mb-4">
                                            <label for="price" class="block text-sm font-medium text-gray-100">Price</label>
                                            <input style="width: 340px;" type="number" id="price" v-model="newPlugin.price" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="flex justify-end mt-6">
                                            <button @click="closeCreateModal" class="bg-gray-700 hover:bg-gray-900 duration-200 px-4 py-2 rounded mr-2"><i class="fa fa-close"></i> Close</button>

                                            <button type="submit" class="bg-orange-600 hover:bg-orange-800 duration-200 text-white px-4 py-2 rounded "><i class="fa fa-add"></i> Add</button>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>


                    <!-- Edit Modal -->
                    <div v-if="showEditModal" class="fixed z-10 inset-0 overflow-y-auto">
                        <div class="flex items-center justify-center min-h-screen">
                            <div class="fixed inset-0 bg-black opacity-50"></div>
                            <div class="relative dark:bg-gray-800 w-96 p-6 rounded shadow-lg">
                                <h2 class="text-2xl font-bold mb-4">Edit Fish</h2>

                                <!-- Form for editing an existing plugin -->
                                <div class="flex justify-end mt-6">
                                    <form @submit.prevent="updatePlugin">
                                        <div class="mb-4">
                                            <label for="name" class="text-sm font-medium text-gray-100">Name</label>
                                            <input style="width: 340px;" type="text" id="name" v-model="editPlugin.name" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="mb-4">
                                            <label for="description" class="block text-sm font-medium text-gray-100">Description</label>
                                            <textarea style="width: 340px;" id="description" v-model="editPlugin.description" class="mt-1 p-2 bg-transparent border-b-2 border-0" required></textarea>
                                        </div>

                                        <div class="mb-4">
                                            <label for="daws" class="block text-sm font-medium text-gray-100">Type</label>
                                            <input style="width: 340px;" type="text" id="daws" v-model="editPlugin.daws" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="mb-4">
                                            <label for="price" class="block text-sm font-medium text-gray-100">Price</label>
                                            <input style="width: 340px;" type="number" id="price" v-model="editPlugin.price" class="mt-1 p-2 bg-transparent border-b-2 border-0" required>
                                        </div>

                                        <div class="flex justify-end mt-6">
                                            <button @click="closeEditModal" class="bg-gray-700 hover:bg-gray-900 duration-200 px-4 py-2 rounded mr-2"><i class="fa fa-close"></i> Close</button>

                                            <button type="submit" class="bg-blue-600 hover:bg-blue-800 duration-200 text-white px-4 py-2 rounded "><i class="fa fa-edit"></i> Update</button>
                                        </div>
                                    </form>
                                </div>
                            </div>
                        </div>
                    </div>



                    </div>
                    <br>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
<script>
export default {
    props: {
        plugins: Array,
        discounts: Array,

    },
    data() {
        return {
            showCreateModal: false,
            showEditModal: false,
            showDeleteModal: false,
            selectedPlugin: null,
            showCreateModal: false,
            startDate: '',
            endDate: '',
            newPlugin: {
                name: '',
                description: '',
                daws: '',
                price: '',

            },
                editPlugin: {
                id: null,
                name: '',
                description: '',
                daws: '',
                price: 0,
            },
        };

    },

    computed: {
        filteredPlugins() {
            // Implement the logic to filter plugins based on start and end dates
            if (this.startDate && this.endDate) {
                const startTimestamp = new Date(this.startDate).getTime();
                const endTimestamp = new Date(this.endDate).getTime();

                return this.plugins.filter(plugin => {
                    const pluginDate = new Date(plugin.date).getTime();
                    return pluginDate >= startTimestamp && pluginDate <= endTimestamp;
                });
            } else {
                // Return all plugins if no date range is specified
                return this.plugins;
            }
        },
    },

    methods: {
        openCreateModal() {
            this.showCreateModal = true;
        },
        closeCreateModal() {
            this.showCreateModal = false;
        },

        openEditModal(plugin) {
            this.showEditModal = true;
            this.editPlugin = { ...plugin }; // Create a copy of the plugin details
        },
        closeEditModal() {
            this.showEditModal = false;
        },
        updatePlugin() {
            this.$inertia.put(`/plugins/${this.editPlugin.id}`, this.editPlugin).then(() => {
                this.closeEditModal();
            }).catch(error => {
                console.error('Error updating plugin:', error);
            });
        },
        openDeleteModal(pluginId) {
            this.selectedPluginId = pluginId;
            this.showDeleteModal = true;
        },
        closeDeleteModal() {
            this.selectedPluginId = null;
            this.showDeleteModal = false;
        },
        deletePlugin() {
            // Add logic to delete the selected plugin
            this.closeDeleteModal();
        },

        createPlugin() {
            this.$inertia.post('/plugins', this.newPlugin).then(() => {
                this.closeCreateModal();
            });
        },

        deletePlugin(pluginId) {
            if (confirm("Are you sure you want to delete this plugin?")) {
                this.$inertia.delete(`/plugins/${pluginId}`).then(() => {
                    // Optionally, you can fetch the updated data from the server and update the local state
                    // Example: this.fetchPluginData();

                    // You can also close the modal or perform other actions as needed
                }).catch(error => {
                    // Handle error if the delete request fails
                    console.error('Error deleting plugin:', error);
                });
            }
        },


        submitFilter() {
            // Fetch and update plugins based on the selected date range
            // You can make an Inertia request to your Laravel backend here
            this.$inertia.get('/plugins', { startDate: this.startDate, endDate: this.endDate }).then(response => {
                // Update the plugins with the response
                this.$emit('update-plugins', response.plugins);

                // Close the filter form or perform any other actions
            });
        },

    },
};
</script>

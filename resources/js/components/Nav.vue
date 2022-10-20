<template>
    <div
        class="bg-white h-12 px-4 flex items-center border-b border-gray-400 shadow-sm"
    >
        <div class="w-1/3">
            <div class="flex">
                <router-link to="/">
                    <svg
                        class="fill-current w-8 h-8"
                        xmlns="http://www.w3.org/2000/svg"
                        viewBox="0 0 24 24"
                    >
                        <path
                            d="M23 12.1c0-6.1-4.9-11-11-11S1 6 1 12.1c0 5.5 4 10.1 9.3 10.9v-7.7H7.5v-3.2h2.8V9.7c0-2.8 1.6-4.3 4.2-4.3 1.2 0 2.5.2 2.5.2v2.7h-1.4c-1.4 0-1.8.8-1.8 1.7v2.1h3.1l-.5 3.2h-2.6V23c5.2-.9 9.2-5.4 9.2-10.9z"
                            fill="#1877f2"
                        />
                    </svg>
                </router-link>
            </div>
        </div>
        <div
            class="w-1/3 flex justify-center items-center h-full"
            v-if="getAuthUser"
        >
            <router-link
                to="/"
                class="mx-6 h-full flex items-center"
                active-class="border-blue-500 border-b-2"
            >
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 24 24"
                    class="fill-current w-5 h-5"
                >
                    <path
                        d="M22.6 11l-9.9-9c-.4-.4-1.1-.4-1.5 0l-9.9 9c-.3.3-.5.8-.3 1.2.2.5.6.8 1.1.8h1.6v9c0 .4.3.6.6.6h5.4c.4 0 .6-.3.6-.6v-5.5h3.2V22c0 .4.3.6.6.6h5.4c.4 0 .6-.3.6-.6v-9h1.6c.5 0 .9-.3 1.1-.7.3-.5.2-1-.2-1.3zm-2.5-8h-4.3l5 4.5V3.6c0-.3-.3-.6-.7-.6z"
                    />
                </svg>
            </router-link>
            <router-link
                :to="'/users/' + getAuthUser.user_id"
                class="mx-6 h-full flex items-center"
                active-class="border-blue-500 border-b-2"
            >
                <img
                    :src="
                        imagepath +
                        getAuthUser.profileimage.data.attributes.image_path
                    "
                    alt="profile image for user"
                    class="w-8 h-8 object-cover rounded-full max-w-none"
                />
            </router-link>
        </div>
        <div class="w-1/3 flex justify-end" title="Logout">
            <svg
                class="cursor-pointer"
                width="24"
                height="24"
                xmlns="http://www.w3.org/2000/svg"
                fill-rule="evenodd"
                clip-rule="evenodd"
                @click="logoutHandler"
            >
                <path
                    d="M16 2v7h-2v-5h-12v16h12v-5h2v7h-16v-20h16zm2 9v-4l6 5-6 5v-4h-10v-2h10z"
                />
            </svg>
        </div>
    </div>
</template>

<script>
import { mapGetters } from "vuex";

export default {
    name: "Nav",
    data() {
        return {
            loading: true,
        };
    },
    computed: {
        ...mapGetters(["getAuthUser", "imagepath"]),
    },
    methods: {
        logoutHandler() {
            axios.post("/logout");
            window.location.href = "/register";
        },
    },
    mounted() {
        this.$store.dispatch("fetchAuthUser");
        this.loading = false;
    },
    watch: {
        $route(to, from) {},
    },
};
</script>

<style scoped></style>

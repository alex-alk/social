<template>
    <div class="flex flex-col flex-1 h-screen">
        <Nav />

        <div class="flex flex-1">
            <Sidebar />

            <div class="overflow-x-hidden w-100 items-center">
                <router-view :key="$route.fullPath"></router-view>
            </div>
        </div>
    </div>
</template>

<script>
import Nav from "./Nav";
import Sidebar from "./Sidebar";

export default {
    name: "App",

    components: {
        Nav,
        Sidebar,
    },
};
</script>

<style scoped></style>

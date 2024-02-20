<template>
    <div>
        <header>
            <nav>
                <div class="logo-container">
                    <a href=""><img src="../assets/mylogo.png" alt="my logo"></a>
                    
                </div>  
            </nav>
        </header>
    </div>
</template>

<script setup>

</script>

<style lang="scss" scoped>
nav {
    padding: 1rem;
    display: flex;
    justify-content: space-between;
}

img {
    width: 100%;
}

@media screen and (min-width: 768px) {
    header {
        display: flex;
        justify-content: space-between;
    }
}
</style>
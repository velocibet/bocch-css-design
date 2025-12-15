<script setup>
const layoutColorRef = useState('layoutColor', () => '#2b66b2');
const layoutColor = computed(() => layoutColorRef.value);
</script>

<template>
    <header class="layout-wrapper" :style="{ '--layout-color': layoutColor }">
        <nav>
            <ul>
                <li><a href="#">HOME</a></li>
                <li><a href="#">MENU</a></li>
                <li><a href="#">CHARACTER</a></li>
                <li><a href="#">SHOP</a></li>
            </ul>
        </nav>
    </header>
    <slot />
</template>

<style scoped>

.layout-wrapper {
  background: linear-gradient(90deg, rgba(0,0,0,0.04), var(--layout-color));
  transition: background 600ms ease, color 400ms ease;
  position: relative;
}

nav {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    position: absolute;
    width: 100vw;
    top: 0;
    left: 0;
    padding: 10px 20px;
    font-family: GenEiGothicN-Heavy;
    z-index: 100;
}

nav ul {
    list-style: none;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 60px;
    margin: 0;
    margin-left: 30px;
    padding: 0;
  }

  nav ul li a {
    text-decoration: none;
    border-radius: 12px;
    padding: 2px 5px;
    color: var(--layout-color);
    transition: background-color 300ms ease, color 400ms ease;
  }

  nav ul li a:hover {
    background-color: var(--layout-color);
    color: #ffffff;
  }

</style>

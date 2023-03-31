<template>
    <div class="navbar">
        <div class="navbar__menu">
            <img src="@/assets/menu.png" alt="" class="navbar__menu-button" />
            <div class="navbar__menu-title">
                <hr class="navbar__menu-title-line-one">
                <hr class="navbar__menu-title-line-two">
                <div class="navbar__menu-title-block">
                    <h5>03</h5>
                    <p>Подсказки</p>
                </div>
                <hr class="navbar__menu-title-line-three">
            </div>
        </div>
        <div class="navbar__scroll">
            <img src="@/assets/arrow.png" alt="#" class="navbar__scroll-line">
            <div class="navbar__scroll-text">Скрольте вниз</div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'NavbarComp'
}
</script>

<style scoped>
.navbar {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;

    width: 152px;
    height: 700px;
}

.navbar__menu {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;

    position: relative;
    top: 2.3rem;
    height: 338.01px;

    margin-left: 2rem;
}

.navbar__menu-button {
    position: relative;
    cursor: pointer;
}

.navbar__menu-title-line-one {
    width: 4.03px;
    position: relative;
    bottom: 3.4rem;
    right: 2.6rem;
}

.navbar__menu-title-line-two {
    width: 8px;
    position: relative;
    bottom: .7rem;
    right: 2.6rem;
}

.navbar__menu-title-line-three {
    width: 8px;
    position: relative;
    top: .5rem;
    right: 2.6rem;
}

.navbar__menu-title-block {
    display: flex;
    flex-direction: row;

    position: relative;
    bottom: 1.1rem;
    left: .3rem;
}

.navbar__menu-title-block::after {
    content: " ";
    display: block;
    height: 2px;
    width: 115px;
    position: absolute;
    top: 75%;
    right: -18%;
    background: #333333;
}

.navbar__menu-title-block h5 {
    position: relative;
    right: .2rem;
    font-size: 16px;
    line-height: 15px;

    color: #333333;
}

.navbar__menu-title-block p {
    position: relative;
    top: .85rem;
    left: 1rem;
    font-size: 14px;
    line-height: 15px;

    color: #333333;
}

.navbar__scroll {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    position: relative;
    bottom: 9rem;
    right: 2rem;

    cursor: pointer;
    transform: rotate(-90deg) scaleX(1);
}

.navbar__scroll-line {
    position: relative;
    top: 1rem;
    right: 4.2rem;
    transform: rotate(90deg) scaleX(1);
}

.navbar__scroll-text {
    position: relative;
    top: 1rem;
    right: 1rem;

    font-size: 14px;
    font-weight: 400;
    color: #333333;
}

</style>
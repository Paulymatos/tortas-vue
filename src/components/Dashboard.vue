<template>
<div id="cake-table">
    <div>
    <div id="cake-table-hearding">
    <div class="order-id">#</div>
    <div>Cliente:</div>
    <div> Massa </div>
    <div> Recheio </div>
    <div> Cobertura </div>
    <div>Opcionais</div>
    <div>Ações</div>
</div>
</div>
<div id="cake-table-rows">
    <div class="cake-table-row">
        <div class="order-number">1</div>
        <div>João</div>
        <div>Branca</div>
        <div> Prestigio</div>
        <div> Nozes</div>
        <div>
            <ul>
                <li>Confete</li>
                <li>Disquete</li>
                <li>Castanha</li>
            </ul>
        </div>
        <div>
            <select name=" Status" class="">
                <option value="">Selecione o Status do Cupcake</option>
            </select>
        </div>
    </div>
</div>
</div>
</template>

<script>
export default {
    name:"Dashboard"
}
</script>
<style scoped>

</style>
<template>
    <button class="round-button" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasTop" aria-controls="offcanvasTop">+</button>

    <div class="offcanvas offcanvas-top" tabindex="-1" id="offcanvasTop" aria-labelledby="offcanvasTopLabel">
        <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasTopLabel">Neue Einnahme:</h5>
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body">
            <input type="date" placeholder="Datum auswählen:">
            <input type="text" pattern="-^\d+(\,\d{1,2})?$" placeholder="Euro-Betrag eingeben">
        </div>
    </div>
</template>

<script>
export default {
    name: "TransaktionCreateEinnahme"
}
</script>

<style scoped>
.round-button {
    width: 50px; /* Durchmesser des runden Buttons */
    height: 50px; /* Durchmesser des runden Buttons */
    border-radius: 50%; /* Macht den Button rund */
    border: none; /* Entfernt den Rand des Buttons */
    background-color: #27b827; /* Hintergrundfarbe des Buttons */
    color: white; /* Textfarbe des Pluszeichens */
    font-size: 24px; /* Größe des Pluszeichens */
    cursor: pointer; /* Zeigt an, dass es sich um einen anklickbaren Button handelt */
    bottom: 20px; /* Abstand vom unteren Rand der Seite */
    right: 20px; /* Abstand vom rechten Rand der Seite */
}
.round-button:hover {
    //background-color: #27b827; /* Ändert die Hintergrundfarbe beim Hovern über den Button */
}

</style>

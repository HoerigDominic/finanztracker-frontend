<template>
    <button class="btn btn-primary round-button" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasRight" aria-controls="offcanvasTop">+</button>

    <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
        <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasRightLabel">Transaktion erstellen</h5>
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <div class="offcanvas-body">
            <form class="row g-3">
                <div class="col-md-6">
                    <label for="inputDate" class="form-label">Datum</label>
                    <input type="date" class="form-control" id="inputDate">
                </div>
                <div class="col-md-6">
                    <label for="inputArt" class="form-label">Art</label>
                    <select class="form-select" v-model="art" id="inputArt">
                        <option value="Einnahme">Einnahme</option>
                        <option value="Ausgabe" >Ausgabe</option>
                    </select>
                </div>
                <div class="col-md-6">
                    <label for="inputBetrag" class="form-label">Betrag</label>
                    <input type="number" class="form-control" id="inputBetrag"
                           :min="art === 'Einnahme' ? 0.00 : -Infinity"
                           :max="art === 'Ausgabe' ? 0.00 : Infinity"
                           step="0.01" placeholder="0.00 €" />
                </div>
                <div class="col-md-6">
                    <label for="inputKategorie" class="form-label">Kategorie</label>
                    <select class="form-select"  v-model= "kategorie" id="inputKategorie">
                        <option v-for="kategorie in kategorien" :value="kategorie" :key="kategorie">{{ kategorie }}</option>

                    </select>
                </div>

                <div class="col-12">
                    <label for="inputBeschreibung" class="form-label">Beschreibung</label>
                    <input type="text" class="form-control" id="inputAddress2">
                </div>
                <div class="col-12">
                    <button type="submit" class="btn btn-primary">Bestätigen</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "TransactionCreate",
    data() {
        return {
            art: null,
            kategorie: null,
            kategorien: ['Gehalt', 'Gutschrift', 'Miete', 'Transport', 'Lebensmittel', 'Freizeit', 'Kleidung']
        };
    }
}
</script>

<style scoped>
.round-button {
    width: 50px; /* Durchmesser des runden Buttons */
    height: 50px; /* Durchmesser des runden Buttons */
    border-radius: 50%; /* Macht den Button rund */
    border: none; /* Entfernt den Rand des Buttons */
    color: white; /* Textfarbe des Pluszeichens */
    font-size: 24px; /* Größe des Pluszeichens */
    cursor: pointer; /* Zeigt an, dass es sich um einen anklickbaren Button handelt */
    bottom: 20px; /* Abstand vom unteren Rand der Seite */
    right: 20px; /* Abstand vom rechten Rand der Seite */
}


</style>

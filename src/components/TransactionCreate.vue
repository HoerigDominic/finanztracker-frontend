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
                    <input type="date" v-model="datum" required class="form-control" id="inputDate">
                </div>
                <div class="col-md-6" >
                    <label for="inputArt" class="form-label">Art</label>
                    <select class="form-select" v-model="art" required id="inputArt">
                        <option value="" selected disabled>Auswählen...</option>
                        <option value="Einnahme">Einnahme</option>
                        <option value="Ausgabe" >Ausgabe</option>
                    </select>
                </div>
                <div class="col-md-6">
                    <label for="inputBetrag" class="form-label">Betrag</label>
                    <input type="number" v-model="betrag" required class="form-control" id="inputBetrag"
                           :min="art === 'Einnahme' ? 0.00 : -Infinity"
                           :max="art === 'Ausgabe' ? 0.00 : Infinity"
                           step="0.01" placeholder="0.00 €" />
                </div>
                <div class="col-md-6" >
                    <label for="inputKategorie" class="form-label">Kategorie</label>
                    <select class="form-select" v-model= "kategorie" required id="inputKategorie">
                        <option value="" selected disabled>Auswählen...</option>
                        <option v-for="kategorie in kategorien" :value="kategorie" :key="kategorie">{{ kategorie }}</option>
                    </select>
                </div>
                <div class="col-12">
                    <label for="inputBeschreibung" class="form-label">Beschreibung</label>
                    <input type="text" v-model="beschreibung" class="form-control" id="inputAddress2">
                </div>
                <div class="col-12">
                    <button type= submit @click="createTransaktion" class="btn btn-primary me-3">Bestätigen</button>
                    <button class="btn btn-danger" type="reset">Reset</button>
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
            datum: '',
            art: '',
            betrag: '',
            kategorie: '',
            kategorien: ['Gehalt', 'Gutschrift', 'Miete', 'Transport', 'Lebensmittel', 'Freizeit', 'Kleidung'],
            beschreibung: '',
        }
    },
    methods: {
        createTransaktion() {

            const endpoint = 'http://localhost:8080/transaktionen'

            const payload = JSON.stringify( {
                datum: this.datum,
                art: this.art,
                betrag: this.betrag,
                kategorie: this.kategorie,
                beschreibung: this.beschreibung
            })

            const requestOption = {
                method: 'POST',
                headers: {'Content-Type': 'application/json'},
                body: payload,
                redirect: 'follow'
            }

            fetch(endpoint, requestOption)
                .catch(error => console.log('error', error))
        }
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

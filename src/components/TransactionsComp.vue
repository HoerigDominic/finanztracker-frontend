<template>
    <button class="btn btn-primary" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasRight" aria-controls="offcanvasTop">Transaktion erstellen</button>

    <!-- Offcanvas rechts für Create//-->
    <div class="offcanvas offcanvas-end" tabindex="-1" id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
        <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasRightLabel">Transaktion erstellen</h5>
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <!-- Eingabefelder für die Transaktion -->
        <div class="offcanvas-body">
            <form class="row g-3">
                <!-- Datum -->
                <div class="col-md-6">
                    <label for="inputDate" class="form-label">Datum</label>
                    <input type="date" v-model="datum" required class="form-control" id="inputDate">
                </div>
                <!-- Art-->
                <div class="col-md-6" >
                    <label for="inputArt" class="form-label">Art</label>
                    <select class="form-select" v-model="art" required id="inputArt">
                        <option value="" selected disabled>Auswählen...</option>
                        <option value="Einnahme">Einnahme</option>
                        <option value="Ausgabe" >Ausgabe</option>
                    </select>
                </div>
                <!-- Betrag-->
                <div class="col-md-6">
                    <label for="inputBetrag" class="form-label">Betrag</label>
                    <input type="number" v-model="betrag" required class="form-control" id="inputBetrag"
                           :min="art === 'Einnahme' ? 0.00 : -Infinity"
                           :max="art === 'Ausgabe' ? 0.00 : Infinity"
                           step="0.01" placeholder="0.00 €" />
                </div>
                <!-- Kategorie-->
                <div class="col-md-6" >
                    <label for="inputKategorie" class="form-label">Kategorie</label>
                    <select class="form-select" v-model= "kategorie" required id="inputKategorie">
                        <option value="" selected disabled>Auswählen...</option>
                        <option v-for="kategorie in kategorien" :value="kategorie" :key="kategorie">{{ kategorie }}</option>
                    </select>
                </div>
                <!-- Beschreibung-->
                <div class="col-12">
                    <label for="inputBeschreibung" class="form-label">Beschreibung</label>
                    <input type="text" v-model="beschreibung" class="form-control" id="inputAddress2">
                </div>
                <!-- Button zur Bestätigung mit createFunktion-->
                <div class="col-12">
                    <button type= submit @click="createTransaction()" class="btn btn-primary">Bestätigen</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Offcanvas links für Update//-->
    <div class="offcanvas offcanvas-start" tabindex="-1" id="offcanvasLeft" aria-labelledby="offcanvasLeftLabel">
        <div class="offcanvas-header">
            <h5 class="offcanvas-title" id="offcanvasLeftLabel">Transaktion bearbeiten</h5>
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
        </div>
        <!-- Eingabefelder für die Transaktionsaktualierung -->
        <div class="offcanvas-body">
            <form class="row g-3">
                <!-- Datum-->
                <div class="col-md-6">
                    <label for="inputDate" class="form-label">Datum</label>
                    <input type="date" v-model="datum" required class="form-control" id="inputDate">
                </div>
                <!-- Art-->
                <div class="col-md-6" >
                    <label for="inputArt" class="form-label">Art</label>
                    <select class="form-select" v-model="art" required id="inputArt">
                        <option value="" selected disabled>Auswählen...</option>
                        <option value="Einnahme">Einnahme</option>
                        <option value="Ausgabe" >Ausgabe</option>
                    </select>
                </div>
                <!-- Betrag-->
                <div class="col-md-6">
                    <label for="inputBetrag" class="form-label">Betrag</label>
                    <input type="number" v-model="betrag" required class="form-control" id="inputBetrag"
                           :min="art === 'Einnahme' ? 0.00 : -Infinity"
                           :max="art === 'Ausgabe' ? 0.00 : Infinity"
                           step="0.01" placeholder="0.00 €" />
                </div>
                <!-- Kategorie-->
                <div class="col-md-6" >
                    <label for="inputKategorie" class="form-label">Kategorie</label>
                    <select class="form-select" v-model= "kategorie" required id="inputKategorie">
                        <option value="" selected disabled>Auswählen...</option>
                        <option v-for="kategorie in kategorien" :value="kategorie" :key="kategorie">{{ kategorie }}</option>
                    </select>
                </div>
                <!-- Beschreibung-->
                <div class="col-12">
                    <label for="inputBeschreibung" class="form-label">Beschreibung</label>
                    <input type="text" v-model="beschreibung" class="form-control" id="inputAddress2">
                </div>
                <!-- Button zur Bestätigung mit updateFunktion-->
                <div class="col-12">
                    <button type= submit @click="updateTransaction(id)" class="btn btn-primary">Bestätigen</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Button deleteAllFunktion-->
    <div class="button-container">
        <button class="btn btn-danger" @click="confirmDelete()" >Alle Transaktionen löschen</button>
    </div>
    <!-- Tabelle für Transaktionen-->
    <div class="transactionsList">
        <table class="centered-table">
            <thead>
            <tr>
                <th>Datum</th>
                <th>Art</th>
                <th>Betrag</th>
                <th>Kategorie</th>
                <th>Beschreibung</th>
                <th></th>
            </tr>
            </thead>
            <tbody>
            <!-- Schleife um alle Transaktionen aus Beackend anzuzeigen-->
            <tr v-for="transaktion in transaktionen" :key="transaktion.id">
                <td>{{ transaktion.datum }}</td>
                <td>{{ transaktion.art }}</td>
                <td>{{ transaktion.betrag}}</td>
                <td>{{ transaktion.kategorie }}</td>
                <td>{{ transaktion.beschreibung }}</td>
                <td>
                    <!-- Dropwonbutton um Transaktion zu löschen (deleteFunktion) oder zu bearbeiten-->
                    <div class="dropdown">
                        <button class="btn btn-primary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
                            Aktionen
                        </button>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                            <li><a class="dropdown-item" @click="deleteTransaction(transaktion.id)"  href="#">Löschen</a> </li>
                            <li><a class="dropdown-item" data-bs-toggle="offcanvas" data-bs-target="#offcanvasLeft" @click = "loadTransactionDataForUpdate(transaktion)" href="#">Bearbeiten</a></li>
                        </ul>
                    </div>
                </td>
            </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    data() {
        return {
            id:'',
            transaktionen: [],
            datum: '',
            art: '',
            betrag: '',
            kategorie: '',
            kategorien: ['Gehalt', 'Gutschrift', 'Miete', 'Transport', 'Lebensmittel', 'Freizeit', 'Kleidung'],
            beschreibung: '',
        };
    },
    methods: {
        //unused da mount Funktion//
        loadThings () {
            const requestOptions = {
            method: 'GET',
            redirect: 'follow'
            }
            fetch('http://localhost:8080/transaktionen', requestOptions)
                .then(response => response.json())
                .then(result => result.forEach(transaktion => {
                    this.transaktionen.push(transaktion)
                }))
                .catch(error => console.log('error', error))
        },

        //Methode um eine Transaktion zu erstellen//
        createTransaction() {

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
        },

        //Methode um eine Transaktion zu löschen//
        deleteTransaction(transaktionId) {

            const endpoint = 'http://localhost:8080/transaktionen/' + transaktionId

            const requestOptions = {
                method: 'DELETE',
                headers: {'Content-Type': 'application/json'}
            }
            fetch(endpoint, requestOptions)
                .then(response => response.json())
                .then(data => {
                    console.log('Success:', data)
                })
                .catch(error => console.log('error', error))
            location.reload()
        },

        //Methode Löschung aller Transaktionen zu bestätigen//
        confirmDelete() {
            if (confirm('Sind Sie sicher, dass Sie alle Transaktionen löschen möchten?')) {
                this.deleteAllTransactions();
            }
        },

        //Methode um alle Transaktionen zu löschen//
        deleteAllTransactions() {
            const endpoint = 'http://localhost:8080/transaktionen'

            const requestOptions = {
                method: 'DELETE',
                headers: {'Content-Type': 'application/json'}
            }
            fetch(endpoint, requestOptions)
                .then(response => response.json())
                .then(data => {
                    console.log('Success:', data)
                })
                .catch(error => console.log('error', error))
            location.reload()
        },

        //Methode um die Daten der ausgewählten Transaktion in Datenfdelder der offcanvas-Felder zu laden //
        loadTransactionDataForUpdate(transaktion) {

            this.id = transaktion.id;
            this.datum = transaktion.datum;
            this.art = transaktion.art;
            this.betrag = transaktion.betrag;
            this.kategorie = transaktion.kategorie;
            this.beschreibung = transaktion.beschreibung;
        },
        //Methode um eine Transaktion zu aktualisieren//
        updateTransaction(transaktionId) {

            const updatedData = {
                datum: this.datum,
                art: this.art,
                betrag: this.betrag,
                kategorie: this.kategorie,
                beschreibung: this.beschreibung,
            }

            const endpoint = 'http://localhost:8080/transaktionen/' + transaktionId

            const requestOptions = {
                method: 'PUT',
                headers: {'Content-Type': 'application/json'},
                body: JSON.stringify(updatedData)
            }
            fetch(endpoint, requestOptions)
                .then(response => response.json())
                .then(data => {
                    console.log('Success:', data)
                })
                .catch(error => console.log('error', error))

        }
    },
    //Methode um alle Transaktionen zu laden//
    mounted() {
        const requestOptions = {
            method: 'GET',
            redirect: 'follow'
        }
        fetch('http://localhost:8080/transaktionen', requestOptions)
            .then(response => response.json())
            .then(result => result.forEach(transaktion => {
                this.transaktionen.push(transaktion)
            }))
            .catch(error => console.log('error', error))
    },
};
</script>

<style>

.button-container {
    position: fixed;
    top: 20px; /* Abstand vom oberen Rand */
    right: 20px; /* Abstand vom rechten Rand */
    z-index: 999; /* Z-Index, um sicherzustellen, dass der Button über anderen Elementen liegt */
}

.transactionsList {
    display: flex;
    justify-content: center;
}

.centered-table {
    border-collapse: collapse;/* Stil für die Tabelle */
    width: 70%; /* Beispiel für die Breite der Tabelle */
    margin-top: 20px; /* Beispiel für den oberen Abstand */
}
.centered-table th, .centered-table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
}
.centered-table th {
    background-color: #f2f2f2;
}

</style>

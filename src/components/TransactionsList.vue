<template>
    <div class="button-container">
        <button class="btn btn-danger" @click="confirmDelete" >Alle Transaktionen löschen</button>
    </div>
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
            <tr v-for="transaktion in transaktionen" :key="transaktion.id">
                <td>{{ transaktion.datum }}</td>
                <td>{{ transaktion.art }}</td>
                <td>{{ transaktion.betrag}}</td>
                <td>{{ transaktion.kategorie }}</td>
                <td>{{ transaktion.beschreibung }}</td>
                <td>
                    <div class="dropdown">
                        <button class="btn btn-primary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
                            Aktionen
                        </button>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                            <li><a class="dropdown-item" @click="deleteTransaction(transaktion.id)"  href="#">Löschen</a> </li>
                            <li><a class="dropdown-item" @click="updateTransaction(transaktion.id,transaktion)"  href="#">Bearbeiten</a></li>
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
            transaktionen: [],
            datum: '',
            art: '',
            betrag: '',
            kategorie: '',
            beschreibung: '',
        };
    },
    methods: {

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

        confirmDelete() {
            if (confirm('Sind Sie sicher, dass Sie alle Transaktionen löschen möchten?')) {
                this.deleteAllTransactions();
            }
        },

        deleteAllTransactions() {
            const endpoint = 'http://localhost:8080/transaktionen/'

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

        updateTransaction(transaktionId, updatedData) {

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
/* CSS-Stile für den Button-Container oben rechts */
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
    /* Stile für die Tabelle */
    border-collapse: collapse;
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

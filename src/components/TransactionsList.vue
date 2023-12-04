<template>
    <h1>Finanztracker</h1>
    <div class="transaction">
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
            <tr v-for="transaction in transactions" :key="transaction.id">
                <td>{{ transaction.datum }}</td>
                <td>{{ transaction.art }}</td>
                <td>{{ transaction.betrag}}</td>
                <td>{{ transaction.kategorie }}</td>
                <td>{{ transaction.beschreibung }}</td>
                <td>
                    <div class="dropdown">
                        <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
                            Aktionen
                        </button>
                        <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                            <li><a class="dropdown-item" href="#">Löschen</a></li>
                            <li><a class="dropdown-item" href="#">Bearbeiten</a></li>
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
            transactions: [],
            datum: '',
            art: '',
            betrag: '',
            kategorie: '',
            beschreibung: '',
            aktionen:''
        };
    },
    methods: {

    },

    mounted() {
        const requestOptions = {
            method: 'GET',
            redirect: 'follow'
        }

        fetch('http://localhost:8080/transaktionen',requestOptions)
            .then(response => response.json())
            .then(result => result.forEach(transaction =>{
                this.transactions.push(transaction)
            }))
            .catch(error => console.log('error',error))
    }

};
</script>

<style>
.transaction {
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

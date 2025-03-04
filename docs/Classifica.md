# 🏆 Classifica Utenti

Questa classifica mostra gli utenti con il **maggior numero di passi**, **minuti di attività fisica** o **ore di sonno** negli ultimi giorni.

## 🔢 **Seleziona il numero di utenti e il tipo di classifica**
<label for="num_utenti">Mostra:</label>
<select id="num_utenti" onchange="aggiornaClassifica()">
    <option value="5">Top 5</option>
    <option value="10">Top 10</option>
    <option value="20">Top 20</option>
</select>

<label for="tipo_classifica">Classifica per:</label>
<select id="tipo_classifica" onchange="aggiornaClassifica()">
    <option value="passi">Passi Giornalieri</option>
    <option value="attivita">Minuti di Attività Fisica</option>
    <option value="sonno">Durata del Sonno (ore)</option>
</select>

## 📊 **Classifica Interattiva**
<div id="chart_classifica" style="width: 100%; height: 500px;"></div>

<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
<script>
// Dati di esempio per 20 utenti
var utenti = [
    { nome: "Marco", passi: 10500, attivita: 75, sonno: 7.5 },
    { nome: "Elena", passi: 12500, attivita: 90, sonno: 8 },
    { nome: "Luca", passi: 9800, attivita: 65, sonno: 6.8 },
    { nome: "Giulia", passi: 11500, attivita: 85, sonno: 7.2 },
    { nome: "Andrea", passi: 8900, attivita: 50, sonno: 6.5 },
    { nome: "Paolo", passi: 13400, attivita: 95, sonno: 8.2 },
    { nome: "Francesca", passi: 7500, attivita: 45, sonno: 6.2 },
    { nome: "Matteo", passi: 9200, attivita: 60, sonno: 7.1 },
    { nome: "Anna", passi: 10800, attivita: 80, sonno: 7.3 },
    { nome: "Giorgio", passi: 9700, attivita: 55, sonno: 6.9 },
    { nome: "Sara", passi: 11200, attivita: 78, sonno: 7.6 },
    { nome: "Davide", passi: 9900, attivita: 62, sonno: 7 },
    { nome: "Martina", passi: 9400, attivita: 58, sonno: 6.7 },
    { nome: "Simone", passi: 8600, attivita: 50, sonno: 6.5 },
    { nome: "Valentina", passi: 8300, attivita: 48, sonno: 6.4 },
    { nome: "Federico", passi: 7200, attivita: 40, sonno: 6 },
    { nome: "Claudia", passi: 6800, attivita: 38, sonno: 5.9 },
    { nome: "Alessandro", passi: 10400, attivita: 85, sonno: 7.4 },
    { nome: "Roberta", passi: 9100, attivita: 60, sonno: 7.1 },
    { nome: "Giovanni", passi: 9950, attivita: 70, sonno: 7.2 }
];

// Funzione per aggiornare la classifica
function aggiornaClassifica() {
    var numUtenti = document.getElementById("num_utenti").value;
    var tipoClassifica = document.getElementById("tipo_classifica").value;

    var metrica = tipoClassifica;
    var titolo = {
        passi: "🏆 Passi Giornalieri",
        attivita: "🏋️ Minuti di Attività Fisica",
        sonno: "😴 Durata del Sonno (ore)"
    }[tipoClassifica];

    // Ordina gli utenti in base alla metrica selezionata
    var utentiTop = utenti.sort((a, b) => b[metrica] - a[metrica]).slice(0, numUtenti);

    var nomi = utentiTop.map(u => u.nome);
    var valori = utentiTop.map(u => u[metrica]);

    // Grafico della classifica
    var chartClassifica = echarts.init(document.getElementById('chart_classifica'));
    var optionClassifica = {
        title: { text: `${titolo} (${numUtenti} utenti)` },
        xAxis: { type: 'category', data: nomi },
        yAxis: { type: 'value' },
        series: [{ data: valori, type: 'bar', color: '#4CAF50' }]
    };
    chartClassifica.setOption(optionClassifica);
}

// Inizializza il grafico con la top 5 per passi
aggiornaClassifica();
</script>

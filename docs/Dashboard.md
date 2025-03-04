# 📊 Dashboard Avanzata
In questa sezione potrai visualizzare la tua dashboard, interagisci con i grafici per scoprire tutti i dati nel miglior modo possibili e avere una visione più chiara. Imposta il tuo periodo di visualizzazione preferito così da isolare i dati relativi a quel periodo particolare.                      


### **📅 Seleziona Periodo**
<label for="periodo">Periodo:</label>
<select id="periodo" onchange="aggiornaGrafici()">
    <option value="7">Ultimi 7 giorni</option>
    <option value="14">Ultimi 14 giorni</option>
    <option value="30">Ultimi 30 giorni</option>
</select>

## **🚶 Distanza Camminata (km)**
<div id="chart_distanza" style="width: 100%; height: 400px;"></div>

## **👣 Numero di Passi**
<div id="chart_passi" style="width: 100%; height: 400px;"></div>

## **🏃 Velocità Camminata (km/h)**
<div id="chart_velocita" style="width: 100%; height: 400px;"></div>

## **⚖️ Stabilità Camminata (score)**
<div id="chart_stabilita" style="width: 100%; height: 400px;"></div>

## **❤️ Frequenza Cardiaca (BPM)**
<div id="chart_battiti" style="width: 100%; height: 400px;"></div>

## **🫀 Tono Cardiovascolare (score)**
<div id="chart_tono" style="width: 100%; height: 400px;"></div>

## **🌬️ Frequenza Respiratoria (respiri/min)**
<div id="chart_respirazione" style="width: 100%; height: 400px;"></div>

## **🩸 Ossigeno nel Sangue (SpO2%)**
<div id="chart_ossigeno" style="width: 100%; height: 400px;"></div>

<script src="https://cdn.jsdelivr.net/npm/echarts/dist/echarts.min.js"></script>
<script>
// Dati di esempio per 30 giorni
var giorniCompleti = Array.from({length: 30}, (_, i) => `Giorno ${i+1}`);

var datiCompleti = {
    distanza: Array.from({length: 30}, () => (Math.random() * 5 + 1).toFixed(2)),
    passi: Array.from({length: 30}, () => Math.floor(Math.random() * 6000) + 5000),
    velocita: Array.from({length: 30}, () => (Math.random() * 2 + 3).toFixed(2)),
    stabilita: Array.from({length: 30}, () => Math.floor(Math.random() * 50) + 50),
    battiti: Array.from({length: 30}, () => Math.floor(Math.random() * 20) + 60),
    tono: Array.from({length: 30}, () => Math.floor(Math.random() * 50) + 50),
    respirazione: Array.from({length: 30}, () => Math.floor(Math.random() * 5) + 12),
    ossigeno: Array.from({length: 30}, () => Math.floor(Math.random() * 3) + 95)
};

// Funzione per aggiornare i grafici in base al periodo selezionato
function aggiornaGrafici() {
    var periodo = document.getElementById("periodo").value;
    var giorni = giorniCompleti.slice(-periodo);

    var metriche = Object.keys(datiCompleti);
    var nomiMetriche = {
        distanza: "Distanza Camminata (km)",
        passi: "Numero di Passi",
        velocita: "Velocità Camminata (km/h)",
        stabilita: "Stabilità Camminata (score)",
        battiti: "Frequenza Cardiaca (BPM)",
        tono: "Tono Cardiovascolare (score)",
        respirazione: "Frequenza Respiratoria (respiri/min)",
        ossigeno: "Ossigeno nel Sangue (SpO2%)"
    };

    metriche.forEach(metrica => {
        var dati = datiCompleti[metrica].slice(-periodo);
        var chart = echarts.init(document.getElementById(`chart_${metrica}`));

        var option = {
            title: { text: `${nomiMetriche[metrica]} (${periodo} giorni)` },
            xAxis: { type: 'category', data: giorni },
            yAxis: { type: 'value' },
            series: [{ data: dati, type: 'line' }]
        };

        chart.setOption(option);
    });
}

// Inizializza i grafici al primo caricamento
aggiornaGrafici();
</script>

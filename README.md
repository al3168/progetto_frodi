# Credit Card Fraud Detection 🛡️💳  

## 📌 Descrizione del progetto  
Questo progetto ha come obiettivo l’analisi e il rilevamento di transazioni fraudolente con carte di credito.  
Il dataset contiene oltre **280.000 transazioni** effettuate in due giorni, di cui circa **0.17% sono frodi**.  

🎯 Obiettivi principali:  
- Effettuare **analisi esplorativa (EDA)** per comprendere il dataset.  
- Applicare **tecniche di preprocessing** e **modelli di Machine Learning** per rilevare le frodi.  
- Valutare le performance del modello con metriche appropriate (Precision, Recall, F1-score, ROC AUC).  

---

## 📂 Dataset  
Il dataset contiene 31 colonne:  

- **Time** → tempo trascorso dalla prima transazione registrata.  
- **V1 … V28** → variabili ottenute tramite PCA (componenti principali), non interpretabili direttamente.  
- **Amount** → importo della transazione.  
- **Class** → variabile target (0 = transazione legittima, 1 = frode).  

---

## 🔎 Analisi Esplorativa (EDA) svolta finora  

✅ Caricamento dataset con `pandas`  
✅ Analisi generale con `info()`, `describe()` e `value_counts()` sulla colonna target `Class`  
✅ Verifica valori nulli (`isnull().sum()`)  
✅ Visualizzazione distribuzione della variabile target  
✅ Creazione di una feature derivata da `Time` (**ora del giorno**)  
✅ Barplot della **percentuale di frodi per ora del giorno** con `matplotlib` e `seaborn`  

📊 *Esempio: percentuale di frodi per ora*  

```python
plt.figure(figsize=(14, 6))
sns.barplot(data=fraud_pct_df,
            x='hour_of_day',
            y='fraud_pct',
            color='steelblue')
plt.xlabel('Ora del giorno')
plt.ylabel('Percentuale di frodi (%)')
plt.title('Percentuale di frodi per ora')
plt.xticks(range(24))
plt.tight_layout()
plt.show()
🚧 Work in Progress

Le prossime fasi in programma:

Analisi delle correlazioni tra le variabili

Preprocessing (scaling, bilanciamento, train/test split)

Addestramento modelli (es. Logistic Regression, Random Forest)

Valutazione con metriche di classificazione

Creazione README completo con risultati e osservazioni finali

🛠️ Tecnologie utilizzate

Python (Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn)

Jupyter Notebook
🚧 Work in Progress

Le prossime fasi in programma:

Analisi delle correlazioni tra le variabili

Preprocessing (scaling, bilanciamento, train/test split)

Addestramento modelli (es. Logistic Regression, Random Forest)

Valutazione con metriche di classificazione

Creazione README completo con risultati e osservazioni finali

🛠️ Tecnologie utilizzate

Python (Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn)

Jupyter Notebook

import pandas as pd
import matplotlib.pyplot as plt 
import seaborn as sns 
froud= pd.read_csv("creditcard.csv")
froud.head()#mi stampo le prime 5 righe per capire come sia fatto il dataset
froud.info()
froud.describe()
nomi_colonne = froud.columns
print(nomi_colonne)
for colonna in froud.columns:
    print(colonna)
froud['Class'].value_counts()
froud.isnull().sum() 
import seaborn as sns
import matplotlib.pyplot as plt
dalle analisi fatte sul datatset emergono diverse informazioni sono presenti outlier  quindi per vedere la distrubuzione usa i grafici per un'analisi visiva 
plt.figure(figsize=(6,4))
sns.boxplot(x=froud['V1'])
plt.title("Boxplot della variabile V1")
plt.show()
# Seleziono solo le colonne numeriche
col_numeriche = froud.select_dtypes(include=['number'])


# Trasforma il DataFrame in formato "long" per visualizzazione
df_long = col_numeriche.melt(var_name='Variabile', value_name='Valore')

# Creo il boxplot
plt.figure(figsize=(14, 6))
sns.boxplot(x='Variabile', y='Valore', data=df_long)

# Migliora la leggibilità
plt.xticks(rotation=45)
plt.title("Boxplot degli outlier nelle variabili numeriche")
plt.tight_layout() ### adatta lo spazio nel grafico
plt.show()
# Seleziono solo le colonne numeriche ma togliendo le colonne time amount e class per migliorare la visibilità del grafico 
col_numeriche = froud.select_dtypes(include=['number']).drop(['Time', 'Amount', 'Class'], axis=1)


# Trasforma il DataFrame in formato "long" per visualizzazione
df_long = col_numeriche.melt(var_name='Variabile', value_name='Valore')

# Creo il boxplot
plt.figure(figsize=(14, 6))
sns.boxplot(x='Variabile', y='Valore', data=df_long)

# Migliora la leggibilità
plt.xticks(rotation=45)
plt.title("Boxplot degli outlier nelle variabili numeriche")
plt.tight_layout() ### adatta lo spazio nel grafico
plt.show()


# 1) CREAZIONE DELLE NUOVE FEATURE TEMPORALI

seconds_in_day = 86_400  # 24 * 60 * 60

# Ora del giorno (0–23)
froud['hour_of_day'] = ((froud['Time'] % seconds_in_day) // 3_600).astype(int)

# Giorno dall'inizio del log (0, 1, 2)
froud['day'] = (froud['Time'] // seconds_in_day).astype(int)


# 2) CONTEGGI PER ORA

# Totale transazioni per ogni ora
hour_counts = froud.groupby('hour_of_day').size()

# Transazioni fraudolente per ogni ora
fraud_hour_counts = (
    froud[froud['Class'] == 1]
    .groupby('hour_of_day')
    .size()
)


# PERCENTUALE DI FRODI PER ORA

fraud_pct = (fraud_hour_counts / hour_counts * 100).fillna(0)

# SOMMA IMPORTI FRAUDOLENTI PER ORA

fraud_hour_amount = (
    froud[froud['Class'] == 1]
    .groupby('hour_of_day')['Amount']
    .sum()
)


#  RISULTATI 

print("Totale transazioni per ora:\n", hour_counts.head(), "\n")
print("Frodi per ora:\n", fraud_hour_counts.head(), "\n")
print("Percentuale di frodi per ora (%):\n", fraud_pct.head(), "\n")
print("Somma importi frodi per ora (€):\n", fraud_hour_amount.head())

print(fraud_pct)          # percentuale frodi per tutte le 24 ore
print(fraud_hour_amount)  # somma importi frodi per tutte le 24 ore
import matplotlib.pyplot as plt
import seaborn as sns

# 1) Trasforma la Serie fraud_pct in un DataFrame
fraud_pct_df = fraud_pct.reset_index()         # diventa: hour_of_day, fraud_pct
fraud_pct_df.columns = ['hour_of_day', 'fraud_pct']

# 2) Crea il barplot
plt.figure(figsize=(14, 6))
sns.barplot(data=fraud_pct_df,
            x='hour_of_day',
            y='fraud_pct',
            color='steelblue')                 # colore unico per semplicità

# 3) Migliora la leggibilità
plt.xlabel('Ora del giorno')
plt.ylabel('Percentuale di frodi (%)')
plt.title('Percentuale di frodi per ora')
plt.xticks(range(24))                          # assicura le etichette 0-23
plt.tight_layout()
plt.show()

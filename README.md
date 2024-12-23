# myproyecto2
import requests
import pandas as pd

# URL del archivo
url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DS0321EN-SkillsNetwork/datasets/dataset_part_1.csv"

# Descargar el archivo
response = requests.get(url)
with open("dataset_part_1.csv", "wb") as file:
    file.write(response.content)

# Leer el archivo descargado con Pandas
df = pd.read_csv("dataset_part_1.csv")
print(df.head(10))
df.isnull().sum()/len(df)*100
df.dtypes
# Filtrar los registros donde la columna 'BoosterVersion' es 'Falcon 9'
falcon9_df = df[df['BoosterVersion'] == 'Falcon 9']

# Contar el número de lanzamientos de Falcon 9
num_falcon9_launches = falcon9_df.shape[0]
print(f'Número de lanzamientos de Falcon 9: {num_falcon9_launches}')
# Contar cuántos valores faltan (NaN) en la columna 'landingPad'
missing_values_landingPad = df['LandingPad'].isnull().sum()

print(f'Número de valores que faltan en la columna LandingPad: {missing_values_landingPad}')
# Filtrar lanzamientos exitosos
successful_launches = df[df['Outcome'].str.contains('True')]

# Contar el total de lanzamientos
total_launches = df.shape[0]

# Calcular la tasa de éxito
success_rate = (successful_launches.shape[0] / total_launches) * 100

print(f'Tasa de éxito: {success_rate:.2f}%')
# Calcular el número de apariciones para cada órbita
orbit_counts = df['Orbit'].value_counts()

# Filtrar el valor específico para 'GTO'
gto_count = orbit_counts['GTO']

print(f"El número de apariciones para la órbita 'GTO' es: {gto_count}")
# Filtrar aterrizajes fallidos
failed_landings = df['Outcome'].str.contains('False', na=False).sum()

print(f"El número de aterrizajes que fallaron por completo es: {failed_landings}")

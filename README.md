# Spotify Moods: segmentación musical con K-Means

Las plataformas de streaming clasifican canciones por género, pero el género no dice cómo se siente una pista. Una canción de rock y una de reggaetón pueden compartir energía y bailabilidad, y dos canciones del mismo género pueden ser opuestas. Este proyecto agrupa canciones de Spotify por sus características acústicas y las presenta en un dashboard para explorar esos ambientes.

## Resultado

Con una muestra de 18 000 canciones únicas, K-Means (K = 4) separa cuatro ambientes:

| Ambiente | Perfil |
|---|---|
| Fiesta / Bailable | Energía alta, positividad alta, muy bailable |
| Intensa / Oscura | Energía muy alta, positividad baja, poca acústica |
| Chill / Relajada | Energía media, acústica alta, bailabilidad moderada |
| Acústica íntima | Energía baja, positividad baja, acústica muy alta |

La configuración publicada usa `energy`, `valence`, `danceability` y `acousticness`. Añadir `tempo` y `loudness` empeora la silueta. El detalle, las métricas y la justificación están en el notebook y en `docs/Proyecto_Spotify_KMeans.pdf`.

## Herramientas

Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, Plotly y Streamlit.

## Dataset

[Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/spotify-tracks-dataset) de maharshipandya (Kaggle). El archivo usado es la copia pública de [Hugging Face](https://huggingface.co/datasets/maharshipandya/spotify-tracks-dataset): 114 000 registros y 114 géneros. El original se guarda en `data/raw/spotify_tracks.csv`. La muestra con el clúster asignado está en `data/processed/spotify_clusters.csv`.

La semilla es `random_state = 42` en la muestra, en el desempate de duplicados y en K-Means.

## Estructura

```
├── README.md
├── requirements.txt
├── data/
│   ├── raw/spotify_tracks.csv
│   └── processed/
│       ├── spotify_clusters.csv
│       └── metricas_kmeans.json
├── notebooks/analisis_kmeans.ipynb
├── src/analisis.py
├── dashboard/app.py
├── docs/Proyecto_Spotify_KMeans.pdf
└── images/
```

## Cómo ejecutarlo

Desde la raíz del proyecto:

```bash
pip install -r requirements.txt
python -m src.analisis
streamlit run dashboard/app.py
```

`python -m src.analisis` vuelve a limpiar los datos, evalúa K de 2 a 8 en las dos configuraciones y regenera el CSV, las métricas y las figuras. El dashboard lee esos archivos. Si solo quieres abrir la app y los archivos procesados ya están, basta con el comando de Streamlit.

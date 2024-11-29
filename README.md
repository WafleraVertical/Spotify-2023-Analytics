# Dashboard de Power BI: Análisis de las Canciones Más Famosas de 2023 en Spotify

Este dashboard de Power BI proporciona un análisis detallado de las canciones más famosas de 2023 según Spotify. Utiliza un dataset comprensivo que ofrece una rica gama de características, permitiendo profundizar en diversos aspectos de las canciones y su rendimiento en diferentes plataformas de música.

## Contenido del Dashboard

### 1. Análisis Musical
- **Exploración de Patrones:** Analiza características de audio para entender las tendencias y preferencias en las canciones populares.
- **Impacto del Artista:** Examina cómo la participación de los artistas y sus atributos se relacionan con el éxito de una canción.

### 2. Comparación de Plataformas
- **Comparación de Popularidad:** Compara la popularidad de las canciones a través de diferentes plataformas de música como Spotify, Apple Music, Deezer y Shazam.
- **Presencia en Varias Plataformas:** Investiga cómo las canciones se desempeñan en diferentes servicios de streaming.

### 3. Tendencias Temporales
- **Shifts en Atributos de Música:** Identifica cambios en los atributos musicales y preferencias a lo largo del tiempo.

### 4. Carga de Carátulas de los Álbumes
- **Visualización de Carátulas:** Cada canción está acompañada por la carátula del álbum correspondiente para una mejor visualización y contexto.

## Características del Dataset
El dataset incluye información sobre:
- Nombre de la canción
- Nombre del/los artista(s)
- Fecha de lanzamiento
- Listas y charts de Spotify
- Estadísticas de streaming
- Presencia en Apple Music
- Presencia en Deezer
- Charts de Shazam
- Varias características de audio

## Uso del Dashboard

1. **Cargar el Dataset:** Importa el dataset en Power BI.
2. **Configurar Visualizaciones:** Configura las visualizaciones de acuerdo a los puntos mencionados en el contenido del dashboard.
3. **Añadir Carátulas de Álbumes:** Asegúrate de que cada canción en el dashboard tenga su carátula de álbum correspondiente para mejorar la presentación visual.

## Contribuciones
Si deseas contribuir a mejorar este dashboard, por favor, abre un issue o envía un pull request.

## Licencia
Este proyecto está bajo la licencia MIT. Para más detalles, consulta el archivo LICENSE.

## Image HTML: Genera el código HTML para mostrar la imagen del álbum.
Image HTML = 
VAR x = CALCULATE(MAX(top_spotify_songs_2023_actualizado[url_imagen]), top_spotify_songs_2023_actualizado[streams] = MAX(top_spotify_songs_2023_actualizado[streams]))
RETURN "
<!DOCTYPE html>
<html lang='en'>
<head>
  <meta charset='UTF-8'>
  <meta name='viewport' content='width=device-width, initial-scale=1.0'>
  <title>Image Cropper</title>
  <style>
    body { font-family: Arial, sans-serif; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; background-color: transparent; }
    .image-container { position: relative; width: 80vw; aspect-ratio: 16 / 9; overflow: hidden; border-radius: 16px; display: flex; justify-content: center; align-items: center; background-color: #ddd; }
    .image-container img { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); min-width: 100%; min-height: 100%; object-fit: cover; }
  </style>
</head>
<body>
  <div class='image-container' id='imageContainer'>
    <img id='previewImage' src='" & x & "' alt='Image preview' />
  </div>
</body>
</html>
"

## Max Streams: Encuentra el valor máximo de streams.

Max streams = MAX(top_spotify_songs_2023_actualizado[streams])

## Percent_Val: Calcula el promedio del porcentaje de energía.

Percent_Val = AVERAGE(top_spotify_songs_2023_actualizado[energy_%])

## Top Song vs AVG: Compara los streams de la canción más popular con el promedio anual.

Top song vs AVG = 
VAR x = [_top song vs avg val]
RETURN IF(x > 0, FORMAT(x, "#.0%") & " " & UNICHAR(9650), FORMAT(x, "#.0%") & " " & UNICHAR(9660))

## Top Song vs AVG Val: Calcula la diferencia entre los streams de la canción más popular y el promedio anual.

top song vs avg val = DIVIDE([_Top Songs streams] - [_Average Stream per year], [_Average Stream per year])

## Top Songs Streams: Calcula la suma de streams de la canción más popular.

Top Songs streams = CALCULATE(SUM(top_spotify_songs_2023_actualizado[streams]), top_spotify_songs_2023_actualizado[streams] = MAX(top_spotify_songs_2023_actualizado[streams]))

## Track: Cuenta el número de canciones.

Track = COUNT(top_spotify_songs_2023_actualizado[track_name])

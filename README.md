# TP-Final-Programación-Funcional
================================================================================
  PROYECTO COMPLETO - RECOMENDADOR DE CANCIONES SEMÁNTICO
  Trabajo Final - Programación Funcional
  Sistema con ChromaDB + Embeddings + Python
================================================================================

ÍNDICE
------
1. Descripción del Proyecto
2. Estructura de Carpetas
3. Archivos de Configuración
4. Datos: songs.json (50 canciones)
5. Código Principal: recommender.py
6. Tests: test_recommender.py
7. Guía Paso a Paso en Visual Studio Code
8. Cómo Ejecutar el Proyecto
9. Cómo Defenderlo
10. Solución de Problemas


================================================================================
1. DESCRIPCIÓN DEL PROYECTO
================================================================================

Este proyecto implementa un recomendador de canciones que usa:

- ChromaDB: Base de datos vectorial para búsqueda semántica
- OpenAI Embeddings: Para convertir texto en vectores numéricos
- Python: Con enfoque en programación funcional
- 50 canciones: Top tracks de Argentina

FUNCIONAMIENTO:
1. El usuario escribe lo que quiere escuchar (ej: "algo triste de piano")
2. El sistema genera el embedding de esa frase
3. Busca en ChromaDB las canciones más similares semánticamente
4. Devuelve las 3 mejores recomendaciones con sus scores

ASPECTOS DE PROGRAMACIÓN FUNCIONAL:
- Funciones puras para transformar datos
- Separación clara entre lógica pura y efectos (IO, HTTP, BD)
- Inmutabilidad en estructuras de datos
- Composición de funciones
- Tests unitarios de funciones puras


================================================================================
2. ESTRUCTURA DE CARPETAS
================================================================================

recomendador-musica/
├── data/
│   └── songs.json           # 50 canciones con descripciones
├── src/
│   └── recommender.py       # Código principal (150 líneas)
├── tests/
│   └── test_recommender.py  # Tests con pytest
├── venv/                    # Ambiente virtual (crear con python -m venv venv)
├── docker-compose.yml       # Configuración de ChromaDB
├── requirements.txt         # Dependencias Python
├── .env                     # Variables de entorno (API key)
├── .gitignore              # Archivos a ignorar en Git
└── README.md               # Documentación (opcional)


================================================================================
3. ARCHIVOS DE CONFIGURACIÓN
================================================================================

---------------------------------------
ARCHIVO: docker-compose.yml
---------------------------------------
version: "3.8"
services:
  chroma:
    image: chromadb/chroma:latest
    ports:
      - "8000:8000"
    volumes:
      - chroma_data:/chroma/chroma
volumes:
  chroma_data:


---------------------------------------
ARCHIVO: requirements.txt
---------------------------------------
chromadb==0.4.18
openai==1.3.7
python-dotenv==1.0.0
pytest==7.4.3


---------------------------------------
ARCHIVO: .env
---------------------------------------
OPENAI_API_KEY=tu_clave_aqui

NOTA: Reemplazar "tu_clave_aqui" con tu API key de OpenAI
Obtener en: https://platform.openai.com/api-keys


---------------------------------------
ARCHIVO: .gitignore
---------------------------------------
venv/
__pycache__/
*.pyc
.env
.pytest_cache/
*.db


================================================================================
4. DATOS: songs.json (50 CANCIONES)
================================================================================

---------------------------------------
ARCHIVO: data/songs.json
---------------------------------------
[
  {
    "id": 1,
    "title": "Bzrp Music Sessions #53",
    "artist": "Shakira, Bizarrap",
    "description": "Session de trap latino con piano, letras sobre desamor y empoderamiento femenino"
  },
  {
    "id": 2,
    "title": "Quevedo: Bzrp Music Sessions #52",
    "artist": "Quevedo, Bizarrap",
    "description": "Trap melódico con piano y letras nostálgicas sobre el pasado"
  },
  {
    "id": 3,
    "title": "Entre Nosotros",
    "artist": "Tiago PZK, LIT killah, Maria Becerra",
    "description": "Trap romántico argentino con voces urbanas y ritmo suave"
  },
  {
    "id": 4,
    "title": "Ella Baila Sola",
    "artist": "Eslabon Armado, Peso Pluma",
    "description": "Corridos tumbados con guitarras mexicanas y letras románticas"
  },
  {
    "id": 5,
    "title": "Cruel Summer",
    "artist": "Taylor Swift",
    "description": "Pop synth ochentero con sintetizadores brillantes y melodía pegadiza"
  },
  {
    "id": 6,
    "title": "Flowers",
    "artist": "Miley Cyrus",
    "description": "Pop empoderamiento con disco vibes y mensaje de auto-amor"
  },
  {
    "id": 7,
    "title": "La Morocha",
    "artist": "Damas Gratis",
    "description": "Cumbia villera clásica con acordeón y letras de barrio argentino"
  },
  {
    "id": 8,
    "title": "Perfecta",
    "artist": "Miranda!",
    "description": "Electropop argentino bailable con sintetizadores y voces dulces"
  },
  {
    "id": 9,
    "title": "Te Amo",
    "artist": "Callejeros",
    "description": "Rock argentino emotivo con guitarras distorsionadas y letra melancólica"
  },
  {
    "id": 10,
    "title": "Claridad",
    "artist": "Duki",
    "description": "Trap argentino introspectivo con autotune suave y letras personales"
  },
  {
    "id": 11,
    "title": "Givenchy",
    "artist": "Duki",
    "description": "Trap intenso con 808s profundos y flow agresivo"
  },
  {
    "id": 12,
    "title": "Antes de Morirme",
    "artist": "C.R.O, Franky Style",
    "description": "Rap argentino melódico con piano y letras reflexivas sobre la vida"
  },
  {
    "id": 13,
    "title": "LALA",
    "artist": "Myke Towers",
    "description": "Reggaeton urbano con dembow y flow caribeño"
  },
  {
    "id": 14,
    "title": "Si No Estás",
    "artist": "Iñigo Quintero",
    "description": "Pop latino melancólico con guitarra acústica y voz emotiva"
  },
  {
    "id": 15,
    "title": "Butakera",
    "artist": "Ke Personajes",
    "description": "Cumbia santafesina moderna con ritmo pegadizo y acordeón"
  },
  {
    "id": 16,
    "title": "Un Finde",
    "artist": "Big One, FMK",
    "description": "Trap argentino fiestero con sintetizadores y letras sobre salir"
  },
  {
    "id": 17,
    "title": "Dos Besitos",
    "artist": "Rusherking, Maria Becerra",
    "description": "Trap romántico argentino con voces suaves y ritmo sensual"
  },
  {
    "id": 18,
    "title": "Algo Contigo",
    "artist": "Tiago PZK",
    "description": "Urban pop argentino romántico con producción moderna"
  },
  {
    "id": 19,
    "title": "Los del Espacio",
    "artist": "LIT killah, Duki, Emilia, Tiago PZK, FMK, Rusherking, Maria Becerra, Big One",
    "description": "Himno trap argentino colaborativo con múltiples voces urbanas"
  },
  {
    "id": 20,
    "title": "Miénteme",
    "artist": "TINI, Maria Becerra",
    "description": "Pop urbano argentino con ritmo reggaeton y voces femeninas potentes"
  },
  {
    "id": 21,
    "title": "Tan Enamorados",
    "artist": "CNCO",
    "description": "Pop latino romántico con coros pegadizos y ritmo alegre"
  },
  {
    "id": 22,
    "title": "Cupido",
    "artist": "TINI",
    "description": "Pop latino bailable con guitarras españolas y producción moderna"
  },
  {
    "id": 23,
    "title": "La Joaqui: Bzrp Music Sessions #60",
    "artist": "La Joaqui, Bizarrap",
    "description": "Cumbia 420 con ritmo de trap y letras de barrio argentino"
  },
  {
    "id": 24,
    "title": "Soltera",
    "artist": "Lunay, Chris Jeday, Gaby Music",
    "description": "Reggaeton fiestero con ritmo dembow y letras sobre libertad"
  },
  {
    "id": 25,
    "title": "La Cobra",
    "artist": "Maria Becerra",
    "description": "Trap argentino femenino con actitud y flow agresivo"
  },
  {
    "id": 26,
    "title": "Sal y Perrea",
    "artist": "Sech, Daddy Yankee, J Balvin, Rosalía, Farruko",
    "description": "Reggaeton de perreo con dembow pesado y colaboración estelar"
  },
  {
    "id": 27,
    "title": "Como Si No Importara",
    "artist": "Emilia",
    "description": "Pop urbano argentino con guitarra trap y voz sensual"
  },
  {
    "id": 28,
    "title": "Cenizas",
    "artist": "Duki, Bizarrap",
    "description": "Trap oscuro con 808s y letras sobre superar el pasado"
  },
  {
    "id": 29,
    "title": "Ameri",
    "artist": "Luck Ra, Marcos Ginocchio",
    "description": "Cuarteto cordobés moderno con ritmo rápido y acordeón"
  },
  {
    "id": 30,
    "title": "Cuatro Veinte",
    "artist": "Nicki Nicole, Duki",
    "description": "Trap chill argentino sobre fumar y relajarse"
  },
  {
    "id": 31,
    "title": "Wapo Traketero",
    "artist": "Nicki Nicole",
    "description": "Trap femenino argentino con flow relajado y estilo urbano"
  },
  {
    "id": 32,
    "title": "Envolver",
    "artist": "Anitta",
    "description": "Reggaeton brasileño sensual con dembow y voces sexy"
  },
  {
    "id": 33,
    "title": "Arranca",
    "artist": "Tiago PZK, FMK",
    "description": "Trap fiestero argentino con sintetizadores y actitud rebelde"
  },
  {
    "id": 34,
    "title": "Muñecas",
    "artist": "La Joaqui, Steve Aoki, Alan Gomez, EL Noba",
    "description": "Cumbia electrónica con drops de EDM y ritmo de perreo"
  },
  {
    "id": 35,
    "title": "Rápido Lento",
    "artist": "Chule, Ke Personajes",
    "description": "Cumbia santafesina con ritmo doble tempo y acordeón"
  },
  {
    "id": 36,
    "title": "Salió el Sol",
    "artist": "Don Omar",
    "description": "Reggaeton clásico con dembow y melodía caribeña optimista"
  },
  {
    "id": 37,
    "title": "Ojalá",
    "artist": "Maria Becerra, Luck Ra",
    "description": "Fusión trap-cuarteto argentino con ritmo híbrido y melodía pegadiza"
  },
  {
    "id": 38,
    "title": "Que Más Pues",
    "artist": "J Balvin, Maria Becerra",
    "description": "Reggaeton moderno con sintetizadores y flow colombiano-argentino"
  },
  {
    "id": 39,
    "title": "Turreo Sessions #3",
    "artist": "Bizarrap, L-Gante, DT.Bilardo",
    "description": "Cumbia 420 con letras de barrio y ritmo de trap cumbia"
  },
  {
    "id": 40,
    "title": "Fugitiva",
    "artist": "Kevin Roldan, Luck Ra",
    "description": "Reggaeton romántico con melodía pegadiza y voces suaves"
  },
  {
    "id": 41,
    "title": "Goteo",
    "artist": "Duki, YSY A, Neo Pistea",
    "description": "Trap argentino underground con 808s y flow experimental"
  },
  {
    "id": 42,
    "title": "Ella Dice",
    "artist": "Emilia, Oriana Sabatini, Rusherking",
    "description": "Pop urbano argentino con ritmo reggaeton y coros juveniles"
  },
  {
    "id": 43,
    "title": "Si Veo a Tu Mamá",
    "artist": "Bad Bunny",
    "description": "Reggaeton melancólico con melodía triste sobre desamor"
  },
  {
    "id": 44,
    "title": "Provenza",
    "artist": "Karol G",
    "description": "Reggaeton colombiano bailable con ritmo dembow y mensaje de empoderamiento"
  },
  {
    "id": 45,
    "title": "Me Porto Bonito",
    "artist": "Bad Bunny, Chencho Corleone",
    "description": "Reggaeton boricua con dembow y flow caribeño pegadizo"
  },
  {
    "id": 46,
    "title": "Despechá",
    "artist": "Rosalía",
    "description": "Merengue mambo moderno con ritmo tropical y palmas flamencas"
  },
  {
    "id": 47,
    "title": "Besos Moja2",
    "artist": "Wisin & Yandel",
    "description": "Reggaeton clásico romántico con dembow y voces suaves"
  },
  {
    "id": 48,
    "title": "Pepas",
    "artist": "Farruko",
    "description": "Guaracha house con ritmo electrónico y letras sobre fiesta"
  },
  {
    "id": 49,
    "title": "Tacones Rojos",
    "artist": "Sebastián Yatra",
    "description": "Pop latino romántico con guitarra y melodía pegadiza"
  },
  {
    "id": 50,
    "title": "Linda",
    "artist": "Tokischa, Rosalía",
    "description": "Dembow dominicano explícito con ritmo trap y actitud callejera"
  }
]


================================================================================
5. CÓDIGO PRINCIPAL: recommender.py
================================================================================

---------------------------------------
ARCHIVO: src/recommender.py
---------------------------------------
"""
Recomendador de canciones usando embeddings y ChromaDB
Trabajo Final - Programación Funcional
"""

import json
import os
from typing import List, Dict, Tuple
from dotenv import load_dotenv
import chromadb
from openai import OpenAI

# ============ FUNCIONES PURAS (sin efectos secundarios) ============

def load_songs_from_json(filepath: str) -> List[Dict]:
    """
    Función pura: carga canciones desde JSON
    """
    with open(filepath, 'r', encoding='utf-8') as f:
        return json.load(f)

def format_song_for_embedding(song: Dict) -> str:
    """
    Función pura: convierte canción a texto para embedding
    """
    return f"{song['title']} by {song['artist']}: {song['description']}"

def extract_ids(songs: List[Dict]) -> List[str]:
    """
    Función pura: extrae IDs como strings
    """
    return [str(s['id']) for s in songs]

def extract_texts(songs: List[Dict]) -> List[str]:
    """
    Función pura: extrae textos formateados
    """
    return [format_song_for_embedding(s) for s in songs]

def extract_metadatas(songs: List[Dict]) -> List[Dict]:
    """
    Función pura: extrae metadatos
    """
    return [{'title': s['title'], 'artist': s['artist'], 'id': s['id']} for s in songs]

def format_results(results: Dict, songs: List[Dict]) -> List[Dict]:
    """
    Función pura: formatea resultados de ChromaDB
    """
    if not results or not results.get('ids'):
        return []
    
    formatted = []
    ids = results['ids'][0]
    distances = results['distances'][0]
    metadatas = results['metadatas'][0]
    
    for song_id, distance, metadata in zip(ids, distances, metadatas):
        # Buscar canción completa
        song = next((s for s in songs if str(s['id']) == song_id), None)
        if song:
            formatted.append({
                'title': song['title'],
                'artist': song['artist'],
                'description': song['description'],
                'score': round(1 - distance, 4)  # Convertir distancia a similitud
            })
    
    return formatted

# ============ FUNCIONES CON EFECTOS (IO, HTTP, BD) ============

def get_embedding(client: OpenAI, text: str) -> List[float]:
    """
    Función con efecto: llama a OpenAI API
    """
    response = client.embeddings.create(
        model="text-embedding-3-small",
        input=text
    )
    return response.data[0].embedding

def init_chroma_client(host: str = "localhost", port: int = 8000):
    """
    Función con efecto: conecta a ChromaDB
    """
    return chromadb.HttpClient(host=host, port=port)

def init_collection(client, collection_name: str):
    """
    Función con efecto: crea o recupera colección
    """
    try:
        client.delete_collection(collection_name)
    except:
        pass
    return client.create_collection(name=collection_name)

# ============ CLASE PRINCIPAL ============

class MusicRecommender:
    """
    Recomendador de canciones semántico
    """
    
    def __init__(self, songs_path: str, openai_key: str):
        self.songs = load_songs_from_json(songs_path)
        self.openai_client = OpenAI(api_key=openai_key)
        self.chroma_client = init_chroma_client()
        self.collection = init_collection(self.chroma_client, "songs")
    
    def index_songs(self):
        """
        Indexa todas las canciones en ChromaDB
        """
        # Extraer datos (funciones puras)
        ids = extract_ids(self.songs)
        texts = extract_texts(self.songs)
        metadatas = extract_metadatas(self.songs)
        
        # Generar embeddings (función con efecto)
        print("🎵 Generando embeddings...")
        embeddings = [
            get_embedding(self.openai_client, text) 
            for text in texts
        ]
        
        # Guardar en ChromaDB (función con efecto)
        self.collection.add(
            ids=ids,
            embeddings=embeddings,
            documents=texts,
            metadatas=metadatas
        )
        
        print(f"✅ Indexadas {len(self.songs)} canciones")
    
    def recommend(self, query: str, top_k: int = 5) -> List[Dict]:
        """
        Busca canciones similares a la consulta
        """
        # Generar embedding de la consulta
        query_embedding = get_embedding(self.openai_client, query)
        
        # Buscar en ChromaDB
        results = self.collection.query(
            query_embeddings=[query_embedding],
            n_results=top_k,
            include=['metadatas', 'distances']
        )
        
        # Formatear resultados (función pura)
        return format_results(results, self.songs)

# ============ CLI SIMPLE ============

def main():
    load_dotenv()
    
    # Inicializar
    recommender = MusicRecommender(
        songs_path="data/songs.json",
        openai_key=os.getenv("OPENAI_API_KEY")
    )
    
    # Indexar canciones
    recommender.index_songs()
    
    # Loop de consultas
    print("\n🎵 Recomendador de Canciones Semántico")
    print("Escribí 'salir' para terminar\n")
    
    while True:
        query = input("¿Qué querés escuchar? > ").strip()
        
        if query.lower() in ['salir', 'exit', 'quit']:
            print("¡Chau! 🎧")
            break
        
        if not query:
            continue
        
        # Buscar recomendaciones
        results = recommender.recommend(query, top_k=3)
        
        # Mostrar resultados
        print(f"\n🎶 Top 3 recomendaciones para '{query}':\n")
        for i, song in enumerate(results, 1):
            print(f"{i}. {song['title']} - {song['artist']} (similitud: {song['score']})")
            print(f"   {song['description']}\n")

if __name__ == "__main__":
    main()


================================================================================
6. TESTS: test_recommender.py
================================================================================

---------------------------------------
ARCHIVO: tests/test_recommender.py
---------------------------------------
import pytest
from src.recommender import (
    format_song_for_embedding,
    extract_ids,
    extract_texts,
    extract_metadatas
)

def test_format_song():
    """Test: formateo de canción"""
    song = {
        "id": 1,
        "title": "Imagine",
        "artist": "John Lennon",
        "description": "Balada al piano"
    }
    result = format_song_for_embedding(song)
    assert result == "Imagine by John Lennon: Balada al piano"

def test_extract_ids():
    """Test: extracción de IDs"""
    songs = [{"id": 1}, {"id": 2}]
    assert extract_ids(songs) == ["1", "2"]

def test_extract_texts():
    """Test: extracción de textos"""
    songs = [
        {"id": 1, "title": "A", "artist": "B", "description": "C"}
    ]
    result = extract_texts(songs)
    assert result == ["A by B: C"]

def test_extract_metadatas():
    """Test: extracción de metadatos"""
    songs = [{"id": 1, "title": "Test", "artist": "Artist"}]
    result = extract_metadatas(songs)
    assert result == [{"id": 1, "title": "Test", "artist": "Artist"}]


================================================================================
7. GUÍA PASO A PASO EN VISUAL STUDIO CODE
================================================================================

PASO 1: INSTALAR PROGRAMAS NECESARIOS
--------------------------------------

1.1 Python 3.10+
   - Descargar de: https://www.python.org/downloads/
   - IMPORTANTE: Marcar "Add Python to PATH" en la instalación
   - Verificar: abrir terminal y escribir: python --version

1.2 Visual Studio Code
   - Descargar de: https://code.visualstudio.com/
   - Instalar y abrir

1.3 Docker Desktop
   - Descargar de: https://www.docker.com/products/docker-desktop
   - Instalar y abrir Docker Desktop (dejarlo corriendo)

1.4 Git (opcional)
   - Descargar de: https://git-scm.com/


PASO 2: INSTALAR EXTENSIONES EN VS CODE
----------------------------------------

Abrir VS Code → Ctrl+Shift+X (o Cmd+Shift+X en Mac)

Buscar e instalar:
1. Python (Microsoft)
2. Pylance (Microsoft)
3. Python Debugger (Microsoft)
4. Docker (Microsoft)


PASO 3: CREAR CARPETA DEL PROYECTO
-----------------------------------

Opción A - Desde VS Code:
1. File → Open Folder
2. Navegar a Documentos (o donde quieras)
3. Click derecho → Nueva carpeta → nombre: recomendador-musica
4. Seleccionar y abrir

Opción B - Desde terminal:
cd Documentos
mkdir recomendador-musica
cd recomendador-musica
code .


PASO 4: CREAR ESTRUCTURA DE CARPETAS
-------------------------------------

En VS Code, en el panel izquierdo (Explorer):
- Click derecho → New Folder → nombre: data
- Click derecho → New Folder → nombre: src
- Click derecho → New Folder → nombre: tests

Estructura:
recomendador-musica/
├── data/
├── src/
└── tests/


PASO 5: CREAR ARCHIVOS
-----------------------

Crear cada archivo haciendo:
Click derecho en la carpeta correspondiente → New File → pegar contenido

5.1 docker-compose.yml (en la raíz)
5.2 requirements.txt (en la raíz)
5.3 .env (en la raíz)
5.4 .gitignore (en la raíz)
5.5 data/songs.json
5.6 src/recommender.py
5.7 tests/test_recommender.py

Copiar el contenido de las secciones anteriores.


PASO 6: CREAR AMBIENTE VIRTUAL
-------------------------------

6.1 Abrir terminal en VS Code
    Apretar: Ctrl+` (tecla de acento grave)

6.2 Crear ambiente virtual
    python -m venv venv

6.3 Activar ambiente virtual
    Windows:   venv\Scripts\activate
    Mac/Linux: source venv/bin/activate

    Deberías ver (venv) al inicio de la línea

6.4 Instalar dependencias
    pip install -r requirements.txt

    Esto instala ChromaDB, OpenAI, pytest, etc.


PASO 7: CONFIGURAR API KEY DE OPENAI
-------------------------------------

7.1 Ir a: https://platform.openai.com/api-keys
7.2 Crear cuenta o iniciar sesión
7.3 Click en "Create new secret key"
7.4 Copiar la clave (empieza con sk-...)
7.5 Abrir el archivo .env en VS Code
7.6 Reemplazar "tu_clave_aqui" con tu clave real
7.7 Guardar (Ctrl+S)


PASO 8: LEVANTAR CHROMADB
--------------------------

En la terminal de VS Code:
docker-compose up -d

Verificar que funciona:
curl http://localhost:8000/api/v1/heartbeat

Deberías ver:
{"nanosecond heartbeat": 1234567890}


PASO 9: CONFIGURAR VS CODE
---------------------------

9.1 Formateo automático
    - Ctrl+, (abrir Settings)
    - Buscar "format on save"
    - Activar "Format On Save"

9.2 Seleccionar intérprete Python
    - Ctrl+Shift+P
    - Escribir "Python: Select Interpreter"
    - Elegir el que dice ./venv/bin/python


================================================================================
8. CÓMO EJECUTAR EL PROYECTO
================================================================================

EJECUTAR EL PROGRAMA
---------------------

1. Asegurarse que el ambiente virtual esté activado (ver (venv) en terminal)
2. Asegurarse que ChromaDB esté corriendo (docker-compose up -d)
3. Ejecutar:

   python src/recommender.py

4. Verás:
   🎵 Generando embeddings...
   ✅ Indexadas 50 canciones
   
   🎵 Recomendador de Canciones Semántico
   Escribí 'salir' para terminar
   
   ¿Qué querés escuchar? >

5. Probar consultas:
   - algo triste de piano
   - quiero bailar
   - rock argentino
   - trap de duki
   - cumbia santafesina


EJECUTAR LOS TESTS
-------------------

En una nueva terminal:
1. Activar ambiente: venv\Scripts\activate (Windows) o source venv/bin/activate (Mac/Linux)
2. Ejecutar: pytest tests/ -v

Deberías ver:
tests/test_recommender.py::test_format_song PASSED
tests/test_recommender.py::test_extract_ids PASSED
tests/test_recommender.py::test_extract_texts PASSED
tests/test_recommender.py::test_extract_metadatas PASSED

============ 4 passed in 0.12s ============


DETENER TODO
------------

Para detener ChromaDB:
docker-compose down

Para salir del ambiente virtual:
deactivate

# Simulador de Sistemes de Recomanació — TFG UdG

Simulador modular en Python que reprodueix i compara el comportament de tres models 
de recomanació de contingut (engagement, ètic i aleatori), analitzant els seus efectes 
sobre la diversitat informativa dels usuaris. Desenvolupat com a Treball de Fi de Grau 
a la Universitat de Girona (2026).

## Estructura del projecte

| Fitxer | Descripció |
|--------|------------|
| `main.py` | Punt d'entrada principal. Orquestra tots els mòduls i genera els resultats |
| `config.py` | Paràmetres globals centralitzats (SEED, TOP_K, EXPLORACIO, etc.) |
| `contingut.py` | Generació del catàleg de vídeos sintètics |
| `usuari.py` | Creació i actualització dels perfils d'usuari |
| `models.py` | Implementació dels tres models de recomanació |
| `simulacio.py` | Motor d'execució del bucle de simulació |
| `metriques.py` | Càlcul de l'entropy de Shannon, concentració i índex de Gini |
| `visualitzacio.py` | Generació de figures comparatives en PNG |
| `exportacio.py` | Exportació de resultats a fitxers CSV |
| `analisi_sensibilitat.py` | Avaluació sistemàtica dels hiperparàmetres TOP_K i EXPLORACIO |

## Requisits

- Python 3.8 o superior
- numpy >= 1.24
- matplotlib >= 3.7
- pandas >= 2.0

## Instal·lació

```bash
pip install numpy matplotlib pandas
```

## Execució

```bash
# Simulació principal (un usuari + 50 usuaris + figures + CSV)
python main.py

# Anàlisi de sensibilitat dels hiperparàmetres
python analisi_sensibilitat.py
```

## Resultats

Un cop executat `main.py`, es genera automàticament la carpeta `resultats/` amb:

- **6 figures PNG** — evolució de preferències, distribució de temes, histogrames 
  multi-usuari, comparació global de mètriques i evolució temporal de l'entropy
- **4 fitxers CSV** — resultats detallats per a anàlisi posterior

Un cop executat `analisi_sensibilitat.py`, s'afegeixen a `resultats/`:
- **2 figures PNG** addicionals de sensibilitat
- **1 fitxer CSV** amb els resultats de la graella d'hiperparàmetres

## Configuració

Tots els paràmetres de la simulació es poden modificar a `config.py`:

| Paràmetre | Valor per defecte | Descripció |
|-----------|-------------------|------------|
| `SEED` | 42 | Llavor aleatòria per a la reproductibilitat |
| `NUM_VIDEOS` | 100 | Mida del catàleg de vídeos sintètics |
| `ITERACIONS` | 50 | Nombre de passos per simulació |
| `NUM_USUARIS` | 50 | Usuaris per a la simulació multi-usuari |
| `TOP_K` | 5 | Candidats considerats pel model ètic |
| `EXPLORACIO` | 0.2 | Taxa d'exploració aleatòria del model ètic |

## Models implementats

- **Model engagement** — replica la lògica dels sistemes comercials, maximitzant 
  la probabilitat d'interacció. Genera cambres d'eco de manera sistemàtica.
- **Model ètic** — incorpora criteris de diversitat i penalització per repetició 
  recent, evitant la concentració temàtica sense eliminar la personalització.
- **Model aleatori** — selecció uniforme aleatòria, actua com a baseline neutre 
  de comparació.

## Autor

Aleix Palmada Teixidor  
Grau en Enginyeria Informàtica — Universitat de Girona  
2026

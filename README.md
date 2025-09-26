# Documentation for Plant Compound Scraper

## Overview
This Python script automates the extraction of natural products from the **COCONUT** database and retrieves molecular properties from **PubChem**. The program uses **Selenium** for web scraping and **requests** for API calls. Extracted data is saved to a CSV file.

---

## Dependencies
Ensure you have the following libraries installed before running the script:
```bash
pip install selenium webdriver-manager pandas tqdm requests
```

---

## Features
- Scrapes **COCONUT** for natural products related to user-provided plant names.
- Fetches molecular properties from **PubChem**, including:
  - Molecular Formula
  - Molecular Weight
  - IUPAC Name
  - Canonical SMILES
  - Compound CID
- Uses **ThreadPoolExecutor** for efficient parallel processing.
- Saves extracted data into a CSV file for easy access.

---

## Best Practices to Ensure Optimal Results
1. **Ensure Correct Spelling of Plant Names**: Incorrect spellings can lead to no results or incorrect data.
2. **Run in a Stable Network Environment**: The script relies on API calls and web scraping, which need stable internet connectivity.
3. **Use a Headless Browser for Performance**: The script is optimized for Google Colab with `--headless` mode enabled.
4. **Avoid Overloading Servers**: Excessive requests may lead to temporary bans. Keep `time.sleep(2)` to prevent this.
5. **Verify Data Integrity**: Check the CSV output for missing or incorrect values before proceeding with analysis.
6. **Keep ChromeDriver Updated**: Use `webdriver-manager` to always fetch the latest ChromeDriver version.
7. **Monitor Errors and Logs**: The script prints error messages for debugging in case of failures.

---

## Script Breakdown
### 1. `setup_driver()`
Initializes the **Selenium WebDriver** for scraping data from **COCONUT**.

### 2. `scrape_coconut_database(plant_name: str) -> List[str]`
Searches for compounds related to the input plant in the **COCONUT** database and extracts their names.

### 3. `fetch_pubchem_properties(compound_name: str) -> Tuple[str, str, str, str]`
Queries **PubChem** for molecular properties using the **PUG REST API**.

### 4. `fetch_pubchem_cid(compound_name: str) -> str`
Retrieves the **Compound ID (CID)** for a given compound from **PubChem**.

### 5. `save_results_to_csv(data: Dict[str, List[str]], filename: str)`
Saves the extracted data into a **CSV file**.

### 6. `process_compound(plant: str, compound: str, extracted_data: Dict[str, List[str]])`
Processes each compound in parallel using **ThreadPoolExecutor**.

### 7. `main()`
Handles user input, initiates scraping, and saves data.

---

## Running the Script
Run the script in a Python environment:
```bash
python script.py
```
Follow the prompt and enter plant names as comma-separated values.

---

## Output
A **CSV file (`natural_products.csv`)** containing extracted data with the following columns:
- **Plant**: Name of the input plant.
- **Compound**: Extracted compound name.
- **CID**: PubChem Compound ID.
- **MolecularFormula**: Chemical formula.
- **MolecularWeight**: Molecular weight.
- **IUPACName**: Standard chemical name.
- **CanonicalSMILES**: Machine-readable molecular structure.

---

## Error Handling
- If a compound is **not found** on PubChem, `N/A` is recorded.
- **Exceptions** during scraping or API calls are logged with appropriate messages.
- The script **skips** plants with no identified compounds.

---

## Conclusion
This script is an efficient way to gather phytochemical data for research. Follow the best practices to maximize accuracy and performance.
#Instruction
NCBI’s PubChem API has the following usage limits (as per their guidelines):
Unauthenticated Requests:
Maximum 5 requests per second.

Maximum 10,000 requests per day.

Authenticated Requests (with API key):
Maximum 10 requests per second.

Maximum 100,000 requests per day.

Concurrent Connections: Limited to 5 simultaneous connections per IP.

Make sure you don't cross the limitation otherwise your ip will get blocked and you will not get any result

---
### Some Common Plants 
```
Aloe Vera,Indian Gooseberry (Amla),Curry Leaves,Camphor,Coconut Oil,Bhringraj,Hibiscus,Henna,Neem,Fenugreek,Sage,Prickly Chaff Flower,Onion,Grape Seed Extract,Spikenard,Rosemary,Thyme,Holy Basil (Tulsi),Garlic,Saw Palmetto,Ginseng,Stinging Nettle,Castor Oil,Jojoba Oil,Arnica,Cayenne Pepper,Black Seed,Shikakai,Moringa,Baheda,Ashwagandha,Fo-Ti,Dong Quai,Goji Berry,Reishi Mushroom,Schisandra,Safflower,True Cinnamon,Angelica Root,Brahmi,Mustard,Burdock Root,Madagascar Periwinkle,Chili Pepper,Turmeric,Lemongrass,Nutgrass,Horsetail,Flaxseed,Ginger,Licorice Root,Lavender,Lemon,Tea Tree Oil,Peppermint,Black Pepper,Pumpkin Seed,Rice Extract,Sandalwood,Soapnut,Baikal Skullcap,Sesame,Clove,White Cedar,Ginkgo,Green Tea,Bladderwrack,Japanese Knotweed,Fennel,Astragalus,Celery,Cockscomb,Dahurian Angelica,Rhubarb,Chinese Peony,Perilla,Peach,Japanese Apricot,Bhringraj,Curry,Kalonji,Nimbu (Lemon),Coconut,Gurhal (Hibiscus),Ghrit Kumari (Aloe Vera),Vijaya (Cannabis),Manjistha,Amla (Indian Gooseberry),Malkangani,Vat Jata (Banyan Tree),Methi (Fenugreek),Henna,Shikakai,Brahmi,Castor,Rose hip,Neem,Mandookparni (Gotu Kola),Ratanjot,Charila (Stone Flower),Reetha (Soapnut),Jatamansi (Spikenard),Laal Chandan (Red Sandalwood),Devdaru (Himalayan Cedar),Cajuput

```
### Scientific Name
```
Aloe vera,Phyllanthus emblica,Murraya koenigii,Cinnamomum camphora,Cocos nucifera,Eclipta prostrata,Hibiscus rosa-sinensis,Lawsonia inermis,Azadirachta indica,Trigonella foenum-graecum,Salvia officinalis,Achyranthes aspera,Allium cepa,Vitis vinifera,Nardostachys jatamansi,Rosmarinus officinalis,Thymus vulgaris,Ocimum tenuiflorum,Allium sativum,Serenoa repens,Panax ginseng,Urtica dioica,Ricinus communis,Simmondsia chinensis,Arnica montana,Capsicum annuum,Nigella sativa,Acacia concinna,Moringa oleifera,Terminalia bellirica,Withania somnifera,Polygonum multiflorum,Angelica sinensis,Lycium barbarum,Ganoderma lucidum,Schisandra chinensis,Carthamus tinctorius,Cinnamomum verum,Angelica archangelica,Bacopa monnieri,Brassica juncea,Arctium lappa,Catharanthus roseus,Capsicum frutescens,Curcuma longa,Cymbopogon citratus,Cyperus rotundus,Equisetum arvense,Linum usitatissimum,Zingiber officinale,Glycyrrhiza glabra,Lavandula angustifolia,Citrus limon,Melaleuca alternifolia,Mentha piperita,Piper nigrum,Cucurbita pepo,Oryza sativa,Santalum album,Sapindus mukorossi,Scutellaria baicalensis,Sesamum indicum,Syzygium aromaticum,Thuja occidentalis,Ginkgo biloba,Camellia sinensis,Fucus vesiculosus,Polygonum cuspidatum,Foeniculum vulgare,Astragalus membranaceus,Apium graveolens,Celosia argentea,Angelica dahurica,Rheum palmatum,Paeonia lactiflora,Perilla frutescens,Prunus persica,Prunus mume,Eclipta alba,Murraya koenigii,Nigella sativa,Citrus limon,Cocos nucifera,Hibiscus rosa-sinensis,Aloe barbadensis,Cannabis sativa,Rubia cordifolia,Emblica officinalis,Celastrus paniculatus,Ficus benghalensis,Trigonella foenum-graecum,Lawsonia inermis,Acacia concinna,Bacopa monnieri,Ricinus communis,Rosa moschata,Azadirachta indica,Centella asiatica,Geranium wallichianum,Parmelia perlata,Sapindus trifoliatus,Nardostachys jatamansi,Pterocarpus santalinus,Cedrus deodara,Melaleuca leucadendron
```
---

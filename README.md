# Biohackathon Germany 2024

## Templates

### Simple Schema: example to extract genus and species from text

```bash
ontogpt extract -i examples/lathyrus.txt -t templates/simple_schema.yaml -m ollama/llama3

input_text: |
  Lathyrus is a pea and a pea is a plant. Lathyrus vestitus is a Lathyrus.
raw_completion_output: |-
  Here are the extracted entities in the desired format:

  genus: Lathyrus
  species: vestitus
prompt: |+
  From the text below, extract the following entities in the following format:

  genus: <The genus of an organism given by its common name or latin name>
  species: <A species name corresponding to the genus.>


  Text:
  Lathyrus is a pea and a pea is a plant. Lathyrus vestitus is a Lathyrus.


  ===

extracted_object:
  genus: NCBITaxon:3853
  species: AUTO:vestitus
named_entities:
  - id: NCBITaxon:3853
    label: Lathyrus
    original_spans:
      - 0:7
      - 40:47
      - 63:70
  - id: AUTO:vestitus
    label: vestitus
    original_spans:
      - 49:56

```

### Habitat schema

Tries to extract genus, species and environmental terms independent of the input language.
From the example, it can be seen that works better on the manually translated version:

#### Application on a German habitat description

```bash
ontogpt extract --show-prompt -i examples/habitat.txt -t templates/habitat.yaml -m ollama/llama3
```

```
extracted_object:
  species:
    - AUTO:Helichrysum%20spp.
    - AUTO:Vernonia%20spp.
    - NCBITaxon:3136809
    - AUTO:Echinops%20gigantea
    - NCBITaxon:3136807
  genus:
    - NCBITaxon:32644
  environments:
    - ENVO:01001808
  location:
    - ENVTHES:10346
  characteristics:
    - AUTO:none
named_entities:
  - id: AUTO:Helichrysum%20spp.
    label: Helichrysum spp.
    original_spans:
      - 155:170
  - id: AUTO:Vernonia%20spp.
    label: Vernonia spp.
    original_spans:
      - 173:185
  - id: NCBITaxon:3136809
    label: Gladiolus sp.
    original_spans:
      - 188:200
  - id: AUTO:Echinops%20gigantea
    label: Echinops gigantea
    original_spans:
      - 203:219
  - id: NCBITaxon:3136807
    label: Berkheya sp.
    original_spans:
      - 223:234
  - id: NCBITaxon:32644
    label: none (Helichrysum, Vernonia, Gladiolus, Echinops, and Berkheya are all
      genera)
  - id: ENVO:01001808
    label: montane grassland
  - id: ENVTHES:10346
    label: Montanes Grassgebiet (no specific place name)
  - id: AUTO:none
    label: none
```

#### Application on a translated English habitat description

```bash
ontogpt extract --show-prompt -i examples/habitat_translated.txt -t templates/habitat.yaml -m ollama/llama3
```

```
extracted_object:
  species:
    - AUTO:Helichrysum%20spp.
    - AUTO:Vernonia%20spp.
    - NCBITaxon:3136809
    - AUTO:Echinops%20gigantea
    - NCBITaxon:3136807
    - AUTO:Lippia%20javanicum
  genus:
    - NCBITaxon:59430
    - NCBITaxon:13753
    - NCBITaxon:49747
    - NCBITaxon:32194
    - NCBITaxon:165077
    - NCBITaxon:320344
  environments:
    - ENVO:01001808
  location:
    - ENVTHES:10346
  characteristics:
    - AUTO:stony%2C%20ash-dark%20colored%20sandy%20laterite%20soil
named_entities:
  - id: AUTO:Helichrysum%20spp.
    label: Helichrysum spp.
    original_spans:
      - 146:161
  - id: AUTO:Vernonia%20spp.
    label: Vernonia spp.
    original_spans:
      - 164:176
  - id: NCBITaxon:3136809
    label: Gladiolus sp.
    original_spans:
      - 179:191
  - id: AUTO:Echinops%20gigantea
    label: Echinops gigantea
    original_spans:
      - 194:210
  - id: NCBITaxon:3136807
    label: Berkheya sp.
    original_spans:
      - 214:225
  - id: AUTO:Lippia%20javanicum
    label: Lippia javanicum
  - id: NCBITaxon:59430
    label: Helichrysum
    original_spans:
      - 146:156
  - id: NCBITaxon:13753
    label: Vernonia
    original_spans:
      - 164:171
  - id: NCBITaxon:49747
    label: Gladiolus
    original_spans:
      - 179:187
  - id: NCBITaxon:32194
    label: Echinops
    original_spans:
      - 194:201
  - id: NCBITaxon:165077
    label: Berkheya
    original_spans:
      - 214:221
  - id: NCBITaxon:320344
    label: Lippia
    original_spans:
      - 228:233
  - id: ENVO:01001808
    label: montane grassland
    original_spans:
      - 0:16
  - id: ENVTHES:10346
    label: (no specific place name mentioned)
  - id: AUTO:stony%2C%20ash-dark%20colored%20sandy%20laterite%20soil
    label: stony, ash-dark colored sandy laterite soil
    original_spans:
      - 68:110
```

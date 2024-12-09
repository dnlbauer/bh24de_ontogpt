# Biohackathon Germany 2024

## Simple example to extract genus and species from text

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


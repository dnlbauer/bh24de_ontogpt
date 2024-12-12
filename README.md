# Biohackathon Germany 2024

Investigated the application of [OntoGPT](https://github.com/monarch-initiative/ontogpt) for extracting terms and information from description of [Senckenbergs collection](https://search.senckenberg.de/).

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
There are 3 "versions":

- [templates/habitat.yaml] was an initial attempt
- [templates/habitat_v2.yaml] aimes to improve the extraction accuracy by giving more examples
and more details about how to extract ENVO terms.
- [templates/habitat_noprompt.yaml] has no custom prompts as a base line.

## results

All templates were applied to 3 examples "habitat", "frischwiese" and "pine forest". See folder [results](results).
All results were calculated using ollama/mistral:latest (f974a74358d6):

```bash
ontogpt extract -i <input> -t <template> --show-prompt -m ollama/mistral -o <output>
```

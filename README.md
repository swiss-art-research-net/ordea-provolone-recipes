# PROVenance Ontology for Linked Open PipeliNEs (PROVOLONE)

JSON-LD bit:

```json
{
  "@context": [
    "https://linked.art/ns/v1/linked-art.json",
    {
      "crmdig": "http://www.ics.forth.gr/isl/CRMdig/",
      "DigitalObject":"crmdig:D1_Digital_Object"
    },
    {
      "aaao": "https://ontology.swissartresearch.net/aaao/"
    },
    {
      "crm":"http://www.cidoc-crm.org/cidoc-crm/",
      "has_dependency":"crm:P20_had_specific_purpose"
    },
    {
      "ex":"https://examples.swissartresearch.net/"
    }
  ],
  "id": "ex:digitalobject/1",
  "type": "DigitalObject",
  "identified_by":{
    "type": "Name",
    "id": "ex:appellation/1",
    "content": "model.pkl"
  }
}
```
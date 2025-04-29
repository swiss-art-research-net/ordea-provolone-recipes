# Provolone documentation

## Templates for provenance-related URIs

**Provenance Base URI:** https://resource.swissartresearch.net/prov/

other possibility: `https://resource.swissartresearch.net/{entity type}/prov/`

URI templates for provenance entity types:
- *project*
    - applies to instances of: `PE35 Project`
    - pattern: `{base URI}/project/{project id}`
    - base URI for entity type: https://resource.swissartresearch.net/prov/project/
    - instance example:  https://resource.swissartresearch.net/prov/project/1234
- *digital reading pipeline step*
    - applies to instances of: `ZE17 Digital Reading`
    - pattern: `{base URI}/digitalreading/`
    - base URI for entity type: https://resource.swissartresearch.net/prov/digitalreading/
    - instance example:  https://resource.swissartresearch.net/prov/digitalreading/1234
- *digital object*
    - pattern: `{base URI}/digitalobject/`
    - base URI for entity type: https://resource.swissartresearch.net/prov/digitalobject/
    - instance example:  https://resource.swissartresearch.net/prov/digitalobject/1234
- *classification*
    - pattern: `{base URI}/classificatorystatus/`
    - base URI for entity type: https://resource.swissartresearch.net/prov/classificatorystatus/
    - instance example:  https://resource.swissartresearch.net/prov/classificatorystatus/1234
- *similarity*
    - pattern: `{base URI}/similaritystatus/`
    - base URI for entity type: https://resource.swissartresearch.net/prov/similaritystatus/
    - instance example:  https://resource.swissartresearch.net/prov/similaritystatus/1234

URI templates for entity types that represent attributes of one or more entity types (e.g. the name of a project, the identifier of a digital object, etc.):

- *name* (appellation)
    - pattern: `{base URI}/{entity type}/{id of the instance}/appellation/{appellation id}`
    - instance example:  https://resource.swissartresearch.net/prov/project/1234/appellation/5678
    - applies to entity types: ...
- *target*
    - pattern: `{base URI}/{entity type}/{id of the instance}/target`
    - instance example:  https://resource.swissartresearch.net/prov/classificatorystatus/1234/target
    - applies to entity types: classification, similarity
- *source*
    - pattern: `{base URI}/{entity type}/{id of the instance}/source`
    - instance example:  https://resource.swissartresearch.net/prov/similaritystatus/1234/target
    - applies to entity types: similarity



## Project

**Description**: A project is the context within which a digital reading pipeline is created and implemented.

**Fields:**
 - *Name*: The name of the project (LAF.6)
 - *Actor*: A person or institution participating to he project (SRDF.129)
 - *Actor role*: The role played by a given person or institution in the project (SRDF.130)
 - *Description*: A description of the project (LAF.15)
 - *URL*: The URL of an online resource providing further information about the project (SRDF.369)

 **JSON schema:**
 ```json
 {  
    // The project that constitutes the context 
    "project":{
        "id": "project/1234",
        "name": "Name of the project",
        "description": "Description of the project",
        "url": "URL of the project",
        "contributors": [
            {
                "name": "Person name",
                "role": "Role in the project"
            }
        ]
    }
 }
 ```

 **Intermediate JSON:**
 ```json
 {  
    // The project that constitutes the context 
    "project":{
        "id": "project/1234",
        "name": "Bilder der Schweiz Online (BSO)",
        "description": "The »Bilder der Schweiz online« (Images of Switzerland) initiative is a three-year project at the University of Zurich (2020-2022), jointly undertaken by Swiss Art Research Infrastructure (SARI) and the lecturer for Swiss Art and Museology at the Institute of Art History at the University of Zurich. ",
        "url": "https://www.sari.uzh.ch/en/Projects/bilder-der-schweiz-online.html",
        "contributors": [
            {
                "name": "Florian Kräutli",
                "role": "Knowledge Graph Engineer"
            }
        ]
    }
 }
 ```

**Turtle example:** the BSO project by SARI
(see [examples/project/bso.ttl](examples/project/bso.ttl))
```turtle
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix crmdig: <http://www.ics.forth.gr/isl/CRMdig/> .
@prefix crmpe: <http://parthenos.d4science.org/CRMext/CRMpe.rdfs/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

# Project: A project is the context within which a digital reading pipeline is created and implemented (ANTM.15)
<https://resource.swissartresearch.net/prov/project/1234> a crmpe:PE35_Project ;
    crm:P01i_is_domain_of <https://example.swissartresearch.net/property/SRDF.129_1> ;
    crm:P02i_is_range_of <https://example.swissartresearch.net/reified_property/SRDF.369_1> ;
    crm:P1_is_identified_by <https://resource.swissartresearch.net/prov/project/1234/appellation/1> ;
    crm:P67i_is_referred_to_by <https://resource.swissartresearch.net/prov/project/1234/linguisticobject/1> .

#Actor: A person or institution participating to he project (SRDF.129)
<https://resource.swissartresearch.net/prov/person/1> a crm:E39_Actor ;
    crm:P1_is_identified_by <https://resource.swissartresearch.net/prov/person/1/appellation/1> .

<https://resource.swissartresearch.net/prov/person/1/appellation/1> a crm:E33_E41_Linguistic_Appellation ;
    crm:P190_has_symbolic_content "Florian Kräutli" .

# Description: A description of the project (LAF.15)
<https://resource.swissartresearch.net/prov/project/1234/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "The »Bilder der Schweiz online« (Images of Switzerland) initiative is a three-year project at the University of Zurich (2020-2022), jointly undertaken by Swiss Art Research Infrastructure (SARI) and the lecturer for Swiss Art and Museology at the Institute of Art History at the University of Zurich. " .

# Name: The name of the project (LAF.6)
<https://resource.swissartresearch.net/prov/project/1234/appellation/1> a crm:E33_E41_Linguistic_Appellation ;
    crm:P190_has_symbolic_content "Bilder der Schweiz Online (BSO)" .

# Actor: A person or institution participating to the project (SRDF.129) -->
<https://example.swissartresearch.net/property/SRDF.129_1> a crm:PC14_carried_out_by ;
    crm:P02_has_range <https://resource.swissartresearch.net/prov/person/1> ;
    crm:P14.1_in_the_role_of <https://resource.swissartresearch.net/prov/person/1/role/1> .

# Actor role: The role played by a given person or institution in the project (SRDF.130) -->
<https://resource.swissartresearch.net/prov/person/1/role/1> a crm:E55_Type ;
    rdfs:label "Knowledge Graph Engineer" . 

<https://example.swissartresearch.net/reified_property/SRDF.369_1> a crm:PC67_refers_to ;
    crm:P01_has_domain <https://example.swissartresearch.net/conceptual_object/SRDF.369_2> ;
    crm:P67.1_has_type <https://www.wikidata.org/wiki/Q42253> .

# The URL of an online resource providing further information about the project
<https://example.swissartresearch.net/conceptual_object/SRDF.369_2> a crmdig:D1_Digital_Object ;
    rdfs:label "https://www.sari.uzh.ch/en/Projects/bilder-der-schweiz-online.html" . 

# URL (Q42253): web address to a particular file or page
<https://www.wikidata.org/wiki/Q42253> a crm:E55_Type .
```

**Claude's plain text description generated from the example above:**
> The RDF snippet describes "Bilder der Schweiz Online (BSO)" or "Images of Switzerland," a three-year project (2020-2022) conducted at the University of Zurich. This initiative was a collaborative effort between the Swiss Art Research Infrastructure (SARI) and the lecturer for Swiss Art and Museology at the University's Institute of Art History. Florian Kräutli participated in the project as a Knowledge Graph Engineer, indicating his specialized role in developing semantic data structures. The project appears to serve as a framework for creating and implementing a digital reading pipeline, likely focused on Swiss art resources. Additional information about this initiative is available through a digital resource at https://www.sari.uzh.ch/en/Projects/bilder-der-schweiz-online.html.

## Steps of a digital reading pipeline

Fields applying to any pipeline step:
 - *Type*: The type of the pipeline step (LAF.11)
 - *Label*: A label identifying the pipeline step (TBD)
 - *Description*: A textual description of the pipeline step (TBD)
 - *Timestamp – begin*: The timestamp of the date when a given pipeline step started (LAF.25)
 - *Timestamp – end*: The timestamp of the date when a given pipeline step ended (LAF.26)
 - *Part of project*: The project within which the pipeline step was carried out (LAF.42)
 - *Dependency*: The subsequent step in the pipeline sequence (ANTF.3)
 
### Labeling

**Description**: The step in a digital reading pipeline that involves creating manually labelled examples for evaluation or training a machine learning model.

**Additional fields:**
 - *Tool*: The digital tool to perform data labeling (SEMF.133) 
 - *Input*: The input digital objects (e.g. texts, images, etc.) on which labeling is performed (SEMF.35)
 - *Output*: A collection of manually labeled digital objects. The type of labels directly depends on the ML task at hand (SEMF.34)
 - *Log file*:
 - *Annotator*:
 - *Tool*:
 - *Platform used*:

 **JSON schema:**
 ```json
{
    "pipeline_steps": [
        {
            "type": "",
            "label": "",
            "description": "",
            "timestamp-begin": "",
            "timestamp-end": "",
            "part-of-project": "", // ID of the containing project
            "dependency": "", // ID of the following step in the pipeline
            "uses-tool": "",
            "has-input": "",
            "has-output": "" 
        }
    ]
}
 ```

 **Intermediate JSON:**
 ```json
 {
    "pipeline_steps": [
        {
            "type": "labeling",
            "label": "BSO Image Labeling",
            "description": "",
            "timestamp-begin": "2023-05-12T10:15:30Z",
            "timestamp-end": "2023-05-31T10:15:30Z",
            "part-of-project": "project/1234", // ID of the containing project
            "dependency": "", // ID of the following step in the pipeline
            "uses-tool": "",
            "has-input": "",
            "has-output": "" 
        }
    ]
}
 ```

**Turtle example:**
```turtle
TBD
```

### Model training

### Data transformation

### Prediction

## Types of predictions

### Classification

### Similarity

## Digital objects

**Description:** Any digital object that is consumed/generated/used by a digital reading pipeline.

**Fields:**
- ...
- ...

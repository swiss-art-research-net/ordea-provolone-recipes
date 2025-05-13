# Provolone documentation

## Templates for provenance-related URIs

**Base URI:** https://resource.swissartresearch.net/

**Base URI for examples:** https://examples.swissartresearch.net/

URI templates for provenance entity types:
- *project*
    - applies to instances of: `PE35 Project`
    - pattern: `{base URI}/project/{project id}`
    - base URI for entity type: https://examples.swissartresearch.net/project/
    - instance example:  https://examples.swissartresearch.net/project/1234
- *digital reading pipeline step*
    - applies to instances of: `ZE17 Digital Reading`
    - pattern: `{base URI}/digitalreading/`
    - base URI for entity type: https://examples.swissartresearch.net/digitalreading/
    - instance example:  https://examples.swissartresearch.net/digitalreading/1234
- *digital object*
    - pattern: `{base URI}/digitalobject/`
    - base URI for entity type: https://examples.swissartresearch.net/digitalobject/
    - instance example:  https://examples.swissartresearch.net/digitalobject/1234
- *software*
    - pattern: `{base URI}/software/`
    - base URI for entity type: https://examples.swissartresearch.net/software/
    - instance example:  https://examples.swissartresearch.net/software/1234
- *classification*
    - pattern: `{base URI}/classificatorystatus/`
    - base URI for entity type: https://examples.swissartresearch.net/classificatorystatus/
    - instance example:  https://examples.swissartresearch.net/classificatorystatus/1234
- *similarity*
    - pattern: `{base URI}/similaritystatus/`
    - base URI for entity type: https://examples.swissartresearch.net/similaritystatus/
    - instance example:  https://examples.swissartresearch.net/similaritystatus/1234

URI templates for entity types that represent attributes of one or more entity types (e.g. the name of a project, the identifier of a digital object, etc.):

- *appellation* (name)
    - pattern: `{base URI}/{entity type}/{id of the instance}/appellation/{appellation id}`
    - instance example:  https://examples.swissartresearch.net/project/1234/appellation/5678
    - applies to entity types: ...
- *linguistic object* (description)
    - pattern: `{base URI}/{entity type}/{id of the instance}/linguisticobject/{linguistic object id}`
    - instance example:  https://examples.swissartresearch.net/project/1234/linguisticobject/1
    - applies to entity types: ...
- *identifier* (e.g. URL)
    - ...
- *target*
    - pattern: `{base URI}/{entity type}/{id of the instance}/target`
    - instance example:  https://examples.swissartresearch.net/classificatorystatus/1234/target
    - applies to entity types: classification, similarity
- *source*
    - pattern: `{base URI}/{entity type}/{id of the instance}/source`
    - instance example:  https://examples.swissartresearch.net/similaritystatus/1234/target
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
        "id": "Project identifier",
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
<https://examples.swissartresearch.net/project/1234> a crmpe:PE35_Project ;
    crm:P01i_is_domain_of <https://example.swissartresearch.net/property/SRDF.129_1> ;
    crm:P02i_is_range_of <https://example.swissartresearch.net/reified_property/SRDF.369_1> ;
    crm:P1_is_identified_by <https://examples.swissartresearch.net/project/1234/appellation/1> ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/project/1234/linguisticobject/1> .

#Actor: A person or institution participating to he project (SRDF.129)
<https://examples.swissartresearch.net/person/1> a crm:E39_Actor ;
    crm:P1_is_identified_by <https://examples.swissartresearch.net/person/1/appellation/1> .

<https://examples.swissartresearch.net/person/1/appellation/1> a crm:E33_E41_Linguistic_Appellation ;
    crm:P190_has_symbolic_content "Florian Kräutli" .

# Description: A description of the project (LAF.15)
<https://examples.swissartresearch.net/project/1234/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "The »Bilder der Schweiz online« (Images of Switzerland) initiative is a three-year project at the University of Zurich (2020-2022), jointly undertaken by Swiss Art Research Infrastructure (SARI) and the lecturer for Swiss Art and Museology at the Institute of Art History at the University of Zurich. " .

# Name: The name of the project (LAF.6)
<https://examples.swissartresearch.net/project/1234/appellation/1> a crm:E33_E41_Linguistic_Appellation ;
    crm:P190_has_symbolic_content "Bilder der Schweiz Online (BSO)" .

# Actor: A person or institution participating to the project (SRDF.129) -->
<https://example.swissartresearch.net/property/SRDF.129_1> a crm:PC14_carried_out_by ;
    crm:P02_has_range <https://examples.swissartresearch.net/person/1> ;
    crm:P14.1_in_the_role_of <https://examples.swissartresearch.net/person/1/role/1> .

# Actor role: The role played by a given person or institution in the project (SRDF.130) -->
<https://examples.swissartresearch.net/person/1/role/1> a crm:E55_Type ;
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

## Digital object

**Description:** Any digital object that is consumed/generated/used by a digital reading pipeline.

**Fields:**
- ...
- ...

## Steps of a digital reading pipeline

Fields applying to any pipeline step:
 - *Type*: The type of the pipeline step (LAF.11)
 - *Label*: A label identifying the pipeline step (TBD)
 - *Description*: A brief description of the pipeline step (TBD)
 - *Timestamp – begin*: The timestamp of the date when a given pipeline step started (LAF.25)
 - *Timestamp – end*: The timestamp of the date when a given pipeline step ended (LAF.26)
 - *Part of project*: The project within which the pipeline step was carried out (LAF.42)
 - *Dependency*: The subsequent step in the pipeline sequence (ANTF.3)

 **JSON schema:**
 ```json
{
    "pipeline_steps": [
        {
            "id": "A unique identifier for the pipeline step",
            "type": "The type of the pipeline step",
            "label": "A label identifying the pipeline step",
            "description": "A brief description of the pipeline step",
            "timestamp-begin": "The timestamp of the date when a given pipeline step started",
            "timestamp-end": "The timestamp of the date when a given pipeline step ended",
            "part-of-project": "The (ID of the) project within which the pipeline step was carried out",
            "dependency": "The (ID of the) subsequent step in the pipeline sequence"
        }
    ]
}
 ```
 
### Labeling

**Description**: The step in a digital reading pipeline that involves creating manually labelled examples for evaluating or training a machine learning model.

**Additional fields:**
 - *Tool*: The digital tool to perform data labeling (SEMF.133) 
 - *Input*: The input digital objects (e.g. texts, images, etc.) on which labeling is performed (SEMF.35)
 - *Output*: A collection of manually labeled digital objects. The type of labels directly depends on the ML task at hand (SEMF.34)
 - *Log file*: Optionally, the labeling process may produce a log file where system and user actions are logged (ANTF.1)
 - *Annotator*: The human annotator(s) involved in the labeling process (LAF.21)
 - *Tool*: The digital tool to perform data labeling (SEMF.133)
 - *Platform used*: The platform where a given tool is hosted and offered as a service (TBD)

 **JSON schema:**
 ```json
{
    "pipeline_steps": [
        {
            // all applicable generic fields here
            "has-input": "",
            "has-output": "",
            "annotators": [
                {
                    "id": "",
                    "name": ""
                }
            ],
            "uses-tool": "",
            "uses-platform": ""
        }
    ]
}
 ```

 **Intermediate JSON:**
 ```json
 {
    "pipeline_steps": [
        {
            "id": "digitalreading/1234",
            "type": "labeling",
            "label": "BSO Image Labeling",
            "description": "Images are manually labelled as `landscape` or `not landscape`.",
            "timestamp-begin": "2023-05-12T10:15:30Z",
            "timestamp-end": "2023-05-31T10:15:30Z",
            "part-of-project": "project/1234",
            "dependency": "digitalreading/45678",
            "has-input": {
                "id": "digitalobject/1234",
                "description": "Folder containing downloaded images",
                "label": "images/",
                "url": "https://raw.githubusercontent.com/swiss-art-research-net/bso-image-classification/refs/heads/main/images/"
            },
            "has-output": {
                "id": "digitalobject/5678",
                "description": "CSV file containing labeled image classifications",
                "label": "data/imageAnnotations.csv",
                "url": "https://raw.githubusercontent.com/swiss-art-research-net/bso-image-classification/refs/heads/main/data/imageAnnotations.csv"
            }
        }
    ]
}
 ```

**Turtle example:**
```turtle
@prefix aaao: <https://ontology.swissartresearch.net/aaao/> .
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix crmdig: <http://www.ics.forth.gr/isl/CRMdig/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://examples.swissartresearch.net/digitalreading/1234> a aaao:ZE17_Digital_Reading ;
    rdfs:label "BSO Image Labeling" ;
    crm:L10_had_input <https://examples.swissartresearch.net/digitalobject/1234> ;
    crm:L11_had_output <https://examples.swissartresearch.net/digitalobject/5678> ;
    crm:P20_had_specific_purpose <https://examples.swissartresearch.net/digitalreading/5678> ;
    crm:P2_has_type <https://example.swissartresearch.net/type/11_1> ;
    crm:P4_has_time-span <https://examples.swissartresearch.net/digitalreading/1234/timestamp> ;
    crm:P9i_forms_part_of <https://examples.swissartresearch.net/project/1234>.

# the digital objects used as input by the labelling step of the BSO pipeline
<https://examples.swissartresearch.net/digitalobject/1234> a crmdig:D1_digital_object ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalobject/1234/linguisticobject/1> ;
    rdfs:label "images/" .

<https://examples.swissartresearch.net/digitalobject/1234/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "Folder containing downloaded images" .

# the digital object produced as output by the labelling step of the BSO pipeline
<https://examples.swissartresearch.net/digitalobject/5678> a crmdig:D1_Digital_Object ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalobject/5678/linguisticobject/1> ;
    rdfs:label "data/imageAnnotations.csv" .

<https://examples.swissartresearch.net/digitalobject/5678/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "CSV file containing labeled image classifications" .

# The timestamp of the date when the labelling step of the BSO pipeline started and ended
<https://examples.swissartresearch.net/digitalreading/1234/timestamp> a crm:E52_Time-Span ;
    crm:P82a_begin_of_the_begin "2023-05-12T10:15:30Z" ;
    crm:P82b_end_of_the_end "2023-05-31T10:15:30Z" .

<https://example.swissartresearch.net/type/11_1> a crm:E55_Type .
```

### Model training

**Description**: The step of a digital reading pipeline that consists in training a machine learning statistical model for performing a given task, typically by means of a manually labelled dataset. 

**Additional fields:**
 - *Input*: The labeled data (e.g. texts, images, etc.) that was used to train the model (SEMF.35)
 - *Output*: The trained model produced (SEMF.34)
 - *Log file*: Optionally, the model training process may produce a log file (ANTF.1)
 - *Code*: Script/notebook used to train the model. (SEMF.133)
 - *Service*: External platform used to train the model (e.g. Roboflow Train) (TBD)

 **Intermediate JSON:**
 ```json
 {
    "pipeline_steps": [
        {
            "id": "digitalreading/5678",
            "type": "model-training",
            "label": "BSO Model Training",
            "description": "The model training follows the approach described in https://towardsdatascience.com/image-classification-using-fastai-v2-on-colab-33f3ebe9b5a3. For training using a GPU (if none is available locally), Google Colab can be used.",
            "timestamp-begin": "2023-05-12T10:15:30Z",
            "timestamp-end": "2023-05-12T10:19:30Z",
            "part-of-project": "project/1234",
            "dependency": "digitalreading/91011", 
            "code": {
                "id": "digitalobject/101112",
                "description": "The Jupyter notebooked used to train the model.",
                "label": "model training.ipynb",
                "url": "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/notebooks/model%20training.ipynb"
            },
            "has-input": "digitalobject/5678",
            "has-output": {
                "id": "digitalobject/91011",
                "description": "Image classification model trained on manually labelled BSO data.",
                "label": "model.pkl",
                "url": "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/models/model.pkl"
            } 
        }
    ]
}
 ```

 **Turtle example:**
```turtle
@prefix aaao: <https://ontology.swissartresearch.net/aaao/> .
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix crmdig: <http://www.ics.forth.gr/isl/CRMdig/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

# the model training step in the BSO digital reading pipeline
<https://examples.swissartresearch.net/digitalreading/5678> a crmdig:D7_Digital_Machine_Event ;
    rdfs:label "BSO Model Training" ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalreading/5678/linguisticobject/1> ;
    crm:L10_had_input <https://examples.swissartresearch.net/digitalobject/5678> ;
    crm:L11_had_output <https://examples.swissartresearch.net/digitalobject/91011> ;
    crm:L23_used_software_or_firmware <https://examples.swissartresearch.net/software/1234> ;
    crm:P20_had_specific_purpose <https://examples.swissartresearch.net/digitalreading/XYZ> ;
    crm:P2_has_type <https://example.swissartresearch.net/type/11_1> ;
    crm:P4_has_time-span <https://examples.swissartresearch.net/digitalreading/5678/timestamp> ;
    crm:P9i_forms_part_of <https://examples.swissartresearch.net/project/1234>.

# description of the BSO model training step
<https://examples.swissartresearch.net/digitalreading/5678/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "The model training follows the approach described in https://towardsdatascience.com/image-classification-using-fastai-v2-on-colab-33f3ebe9b5a3. For training using a GPU (if none is available locally), Google Colab can be used." .

# The timestamp of the date when the model training step of the BSO pipeline started and ended
<https://examples.swissartresearch.net/digitalreading/5678/timestamp> a crm:E52_Time-Span ;
    crm:P82a_begin_of_the_begin "2023-05-12T10:15:30Z" ;
    crm:P82b_end_of_the_end "2023-05-12T10:19:30Z" .

# the trained model produced
<https://examples.swissartresearch.net/digitalobject/91011> a crmdig:D1_Digital_Object ;
    crm:P1_is_identified_by <https://examples.swissartresearch.net/digitalobject/91011/identifier/1> ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalobject/91011/linguisticobject/1> ;
    rdfs:label "model.pkl" .

# description of the trained model
<https://examples.swissartresearch.net/digitalobject/91011/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "Image classification model trained on manually labelled BSO data." .

# URL of the trained model
<https://examples.swissartresearch.net/digitalobject/91011/identifier/1> a crm:E42_Identifier ; 
    crm:P190_has_symbolic_content "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/models/model.pkl" ;
    crm:P2_has_type <https://vocab.getty.edu/aat/300404630> .

# Notebook used to train the model
<https://examples.swissartresearch.net/software/1234> crmdig:D14_Software ;
    rdfs:label "model training.ipynb" ;
    crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/software/1234/linguisticobject/1> .

# Description of the notebook
<https://examples.swissartresearch.net/software/1234/linguisticobject/1> a crm:E33_Linguistic_Object ;
    crm:P190_has_symbolic_content "Image classification model trained on manually labelled BSO data." .

# URL of the notebook
<https://examples.swissartresearch.net/software/1234/identifier/1> a crm:E42_Identifier ; 
    crm:P190_has_symbolic_content "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/notebooks/model%20training.ipynb" ;
    crm:P2_has_type <https://vocab.getty.edu/aat/300404630> .

<https://example.swissartresearch.net/type/11_1> a crm:E55_Type .

<https://vocab.getty.edu/aat/300404630> a crm:E55_Type ;
    rdfs:label "URL" .
```

### Data transformation

### Prediction

**Description:** The step of a digital reading pipeline at which a statistical machine learning model makes predictions on unseen data.

**Additional fields:**
- *Input data*: A set of input digital objects (SEMF.35)
- *Output*: Digital object (file) containing the model's predictions (SEMF.34)
- *Log file*: Optionally, the prediction process may produce a log file (ANTF.1)
- *Code*: Script/notebook used to obtain the predictions (SEMF.133)
- *Model*: The trained model used to generate predictions (SEMF.35)
- *API*: External API service used to obtain the predictions, as an alternative to a (local) model (TBD).

**Intermediate JSON:**
 ```json
 {
    "pipeline_steps": [
        {
            "id": "digitalreading/91011",
            "type": "prediction",
            "label": "BSO Prediction",
            "description": "Prediction of image classes on unseen data from the BSO project.",
            "timestamp-begin": "2023-05-12T10:15:30Z",
            "timestamp-end": "2023-05-12T10:19:30Z",
            "part-of-project": "project/1234",
            "model": "digitalobject/91011",
            "has-input-data": "digitalobject/1234",
            "code": {
               "id": "digitalobject/121314",
               "description": "Notebook containing examples of how to load the trained model and perform image classification.",
               "label": "classify images.ipynb",
               "url": "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/notebooks/classify%20images.ipynb"
           },
            "has-output": {
                "id": "digitalobject/151617",
                "description": "The file where the image classification results are written.",
                "label": "output/predictions.csv",
                "url": "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/output/predictions.csv"
            }
        }
    ]
}
 ```

**Turtle example:**
```turtle
@prefix aaao: <https://ontology.swissartresearch.net/aaao/> .
@prefix crm: <http://www.cidoc-crm.org/cidoc-crm/> .
@prefix crmdig: <http://www.ics.forth.gr/isl/CRMdig/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<https://examples.swissartresearch.net/digitalreading/91011> a aaao:ZE17_Digital_Reading ;
    rdfs:label "BSO image classification (prediction)" ;
    
    # Input data
    crm:L10_had_input <https://examples.swissartresearch.net/digitalobject/1234> ;
    
    # Trained model used for prediction
    crm:L10_had_input <https://examples.swissartresearch.net/digitalobject/91011> ;
    
    # Code
    crm:L23_used_software_or_firmware <https://examples.swissartresearch.net/digitalobject/121314> ;
    
    # Output
    crm:L11_had_output <https://examples.swissartresearch.net/digitalobject/151617> ;
    
    crm:P4_has_time-span <https://examples.swissartresearch.net/digitalreading/91011/timestamp> ;
    crm:P9i_forms_part_of <https://examples.swissartresearch.net/project/1234>.


    # Notebook used to classify images (new predicitons)
    <https://examples.swissartresearch.net/digitalobject/121314> crmdig:D14_Software ;
        rdfs:label "classify images.ipynb" ;
        crm:P1_is_identified_by <https://examples.swissartresearch.net/digitalobject/121314/identifier/1> ;
        crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalobject/121314/linguisticobject/1> .

    # Description of the notebook
    <https://examples.swissartresearch.net/digitalobject/121314/linguisticobject/1> a crm:E33_Linguistic_Object ;
        crm:P190_has_symbolic_content "Notebook containing examples of how to load the trained model and perform image classification." .

    # URL of the notebook
    <https://examples.swissartresearch.net/digitalobject/121314/identifier/1> a crm:E42_Identifier ; 
        crm:P190_has_symbolic_content "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/notebooks/classify%20images.ipynb" ;
        crm:P2_has_type <https://vocab.getty.edu/aat/300404630> .

    # Output data
    <https://examples.swissartresearch.net/digitalobject/151617> crmdig:D1_Digital_Object ;
        rdfs:label "output/predictions.csv" ;
        crm:P1_is_identified_by <https://examples.swissartresearch.net/digitalobject/151617/identifier/1> ;
        crm:P67i_is_referred_to_by <https://examples.swissartresearch.net/digitalobject/151617/linguisticobject/1> .

    # Description of output data
    <https://examples.swissartresearch.net/digitalobject/151617/linguisticobject/1> a crm:E33_Linguistic_Object ;
        crm:P190_has_symbolic_content "The file where the image classification results are written." .

    # URL of the output data
    <https://examples.swissartresearch.net/digitalobject/151617/identifier/1> a crm:E42_Identifier ; 
        crm:P190_has_symbolic_content "https://github.com/swiss-art-research-net/bso-image-classification/blob/main/output/predictions.csv" ;
        crm:P2_has_type <https://vocab.getty.edu/aat/300404630> .

    # The timestamp of the date when the prediction step of the BSO pipeline started and ended
    <https://examples.swissartresearch.net/digitalreading/91011/timestamp> a crm:E52_Time-Span ;
        crm:P82a_begin_of_the_begin "2023-05-12T10:15:30Z" ;
        crm:P82b_end_of_the_end "2023-05-31T10:15:30Z" .
```

## Types of predictions

### Classification

### Similarity


![Zendro logo](figures/Zendro_logo_horizontal.png)

# Zendro

Zendro is a software tool to quickly create a data warehouse tailored to your specifications. You tell Zendro what the structure of your data is, in the form of models, and where the data is or shall be stored. Zendro will then automatically create two standardized interfaces for your data models. Both interfaces provide access to the standard CRUD, create, read, update, and delete functions, available for each of the defined data models. One of the two interfaces is an intuitive graphical browser based single page application implemented in Google's standard material design. The other is an exhaustive application programming interface built with Facebook's efficient GraphQL framework, enabling a connection to your data warehouse from any programming language or data analysis pipeline with utmost ease, simply by sending HTTP requests to your GraphQL server. Data can be distributed over several databases and servers without losing the relationships between your data records, even if they are not stored in the same place.

Zendro consists of two main components, backend and frontend. The backend component has its [base project](https://github.com/ScienceDb/graphql-server) and a [code generator](https://github.com/ScienceDb/graphql-server-model-codegen). The frontend of SPA (Single Page Application) also has its [base project](https://github.com/ScienceDb/single-page-app) and a [code generator](https://github.com/ScienceDb/single-page-app-codegen).
See the guides below on how to use Zendro.

Also find Zendro-dev on [github](https://github.com/Zendro-dev).  

If you have any questions or comments, please don't hesitate to contact us via an issue [here](https://github.com/Zendro-dev/Zendro-dev.github.io/issues). Tag your issue as a question and we will try to answer as quick as possible.

[<p align="center"><img src="./figures/quick.png" /></p>](quickstart.md) [<p align="center"><img src="./figures/gettingstarted.png"/></p>](setup_root.md)

### HOW-TO GUIDES:
* [How to define data models: for developers](setup_data_scheme.md). Detailed technical specifications on how to define data models for Zendro, aimed at software developers and system administrators.
* [How to define data models: for non-developers](non-developer_documentation.md). A brief, illustrated guide of data model specifications, data formatting and data uploading options, aimed at data modelers or managers to facilitate collaboration with developers.
* [How to use Zendro command line interface (CLI)](zendro_cli.md). A tutorial of Zendro CLI, aimed at software developers.
* [How to query and extract data](fromGraphQlToR.html). A concise guide on how to use the Zendro API from R to extract data and perform queries, aimed at data managers or data scientists.
* [How to setup Authentication / Authorization](oauth.md). A concise guide on how to use and setup the Zendro authorization / authentication services.
* [API documentation](api_root.md).

### REPOSITORIES:

* [GraphQL server](https://github.com/ScienceDb/graphql-server)
* [GraphQL server model generator](https://github.com/ScienceDb/graphql-server-model-codegen)
* [Single page application](https://github.com/ScienceDb/single-page-app)
* [Single page application model generator](https://github.com/ScienceDb/single-page-app-codegen)

### CONTRIBUTIONS
Zendro is the product of a joint effort between the Forschungszentrum Jülich, Germany and the Comisión Nacional para el Conocimiento y Uso de la Biodiversidad, México, to generate a tool that allows efficiently building data warehouses capable of dealing with diverse data generated by different research groups in the context of the FAIR principles and multidisciplinary projects. The name Zendro comes from the words Zenzontle and Drossel, which are Mexican and German words denoting a mockingbird, a bird capable of “talking” different languages, similar to how Zendro can connect your data warehouse from any programming language or data analysis pipeline.

#### Zendro contributors in alphabetical order
Francisca Acevedo<sup>1</sup>, Vicente Arriaga<sup>1</sup>, Katja Dohm<sup>3</sup>, Constantin Eiteneuer<sup>2</sup>, Sven Fahrner<sup>2</sup>, Frank Fischer<sup>4</sup>, Asis Hallab<sup>2</sup>, Alicia Mastretta-Yanes<sup>1</sup>, Roland Pieruschka<sup>2</sup>, Alejandro Ponce<sup>1</sup>, Yaxal Ponce<sup>2</sup>, Francisco Ramírez<sup>1</sup>, Irene Ramos<sup>1</sup>, Bernardo Terroba<sup>1</sup>, Tim Rehberg<sup>3</sup>, Verónica Suaste<sup>1</sup>, Björn Usadel<sup>2</sup>, David Velasco<sup>2</sup>, Thomas Voecking<sup>3</sup>

##### Author affiliations
1. CONABIO - Comisión Nacional para el Conocimiento y Uso de la Biodiversidad, México
2. Forschungszentrum Jülich - Germany
3. auticon - www.auticon.com
4. InterTech - www.intertech.de

#### Zendro author contributions
Asis Hallab and Alicia Mastretta-Yanes coordinated the project. Asis Hallab designed the software. Programming of code generators, the browser based single page application interface, and the GraphQL application programming interface was done by Katja Dohm, Constantin Eiteneuer, Francisco Ramírez, Tim Rehberg, Veronica Suaste, David Velasco, Thomas Voecking, and Dan Wang. Counselling and use case definitions were contributed by Francisca Acevedo, Vicente Arriaga, Frank Fischer, Roland Pieruschka, Alejandro Ponce, Irene Ramos, and Björn Usadel. User experience and application of Zendro on data management projects was carried out by Asis Hallab, Alicia Mastretta-Yanes, Yaxal Ponce, Irene Ramos, Verónica Suaste, and David Velasco. Logo design was made by Bernardo Terroba.

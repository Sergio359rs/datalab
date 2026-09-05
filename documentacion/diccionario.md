| Entidad | Atributo | Tipo | PK/FK | Descripción |
|---------|----------|------|-------|-------------|
| DATASET | id_dataset | INT | PK | Identificador único |
| DATASET | nombre | VARCHAR(100) |  | Nombre del dataset |
| EXPERIMENTO | id_exp | INT | PK | ID experimento |
| EXPERIMENTO | fecha | DATETIME |  |  |
| EXPERIMENTO | resultado | VARCHAR (100) | | ID experimento |
| EXPERIMENTO | proyecto_id | INT |FK| ID experimento |
| EXPERIMENTO | cientifico_datos_id |INT|FK| ID experimento |
| PROYECTOS | id proyecto | INT | PK | ID proyecto |
| PROYECTOS | nombre del proyecto | VARCHAR (45)|  | ID proyecto |
| PROYECTOS | area encargada | VARCHAR (45)|  | ID proyecto |
| PROYECTOS | fecha de inicio | DATETIME|  | ID proyecto |
| PROYECTOS | fecha de finalizacion | DATETIME|  | ID proyecto |
| PROYECTOS | codigo del proyecto | VARCHAT (45)|  | ID proyecto |
| USA | id | INT| PK | ID proyecto |
| USA | experimento_id | INT| FK | ID usa |
| USA | dataset_id | INT| FK | ID proyecto |
| PARTICIPA | id_participa|INT| PK | ID participa |
| PARTICIPA |fecha_inicio|DATETIME|  | ID participa |
| PARTICIPA |fecha_fin|DATETIME|  | ID participa |
| PARTICIPA |cientifico_datos_id|INT| FK | ID participa |
| PARTICIPA |proyectos_id|INT| FK | ID participa |
| CIENTIFICO_DATOS |cientifico de dato id|INT| PK | ID cientifico de dato |
| CIENTIFICO_DATOS |nombre|VARCHAR (60)|  | ID cientifico de dato |
| CIENTIFICO_DATOS |email|VARCHAR (45)| | ID cientifico de dato |
| CIENTIFICO_DATOS |documento de identidad|VARCHAR (30)| | ID cientifico de dato |
| CIENTIFICO_DATOS |area encargada|VARCHAR (30)| | ID cientifico de dato |
| CIENTIFICO_DATOS |numero de telefono|VARCHAR (45)| | ID cientifico de dato |
| CIENTIFICO_DATOS |apellido|VARCHAR (45)| | ID cientifico de dato |
| MODELOS |id modelo|INT|PK| ID modelo |
| MODELOS |experimentos_id|INT|FK| ID modelo |
| MODELOS |tipo de modelo|VARCHAR (45)|| ID modelo |
| MODELOS |nombre del modelo|VARCHAR (45)|| ID modelo |
| MODELOS |codigo de modelo|VARCHAR (45)|| ID modelo |
| METRICA |id metrica|INT|PK| ID metrica |
| METRICA |informacion|VARCHAR (100)|| ID metrica |
| METRICA |modelos_id|INT|FK| ID metrica |
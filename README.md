# library_annotator
Annotates library files for CRISPR/Cas9 knockout screens.

Author: Collin Schlager (Summer 2018)

___________

### Purpose:

Uses web-based gene databases to annotate a library file with relevant data. Currently, MyGene is being used, although soon other information sources will be interacted into this API wrapper.

### Usage:

The annotate.py file is fully modular and can be imported into any script.

Import the annotator with:
    `import annotate`
    
### Documentation:

##### Variables:
    
`annotate.fields` is a list of the fields you want to be annotated for each guide.
              - values: ['name,',
                        'summary',
                        'other_names',
                        'MGI',
                        'Vega',
                        'accession',
                        'alias',
                        'ensembl',
                        'entrezgene',
                        'homologene',
                        'refseq',
                        'symbol',
                        'type_of_gene']

`annotate.fields_simple` is a subset of `annotate.fields` that includes only name information:
              - values: ['name,',
                        'summary',
                        'other_names',
                        'alias',
                        'symbol',
                        'type_of_gene']
                        
###### Functions:

1) `annotate.annotate_df( <library dataframe> , <column>, embellish_on_type=<query term type>, fields=<fields_list>, verbose=<True/False>)`
    * Takes a library dataframe and a column to perform the queries on as input. Returns an annotated library dataframe.

    * `library dataframe` = a dataframe with your library guides and some identification information (see `column`).
    * `column` = the name of the column that holds the identification information to be used in a query (e.g. entrez-id).
    * `embellish_on_type` = for the mygene database, what type of id are the data in `column`. Default is "entrezid".
    * `fields` = a list of fields to annotate for each entry. Terms are found in the mygene documentation.
                - default: `annotate.fields`
    * `verbose` = <True/False>. On True, displays some information about the queries being performed. Helpful to track how close the annotation job is to completion.

2) `annotate.annotate_file( <library_file_path>, <column>, embellish_on_type=<query term type>, fields=<fields_list>,
verbose<True/False>)`
* Takes a library file path (.csv) and a column to perform the queries on as input. Writes another file to the same path location with "_annotated" added to the end of the original library file name.

    * `library dataframe` = a dataframe with your library guides and some identification information (see `column`).
    * `column` = the name of the column that holds the identification information to be used in a query (e.g. entrez-id).
    * `embellish_on_type` = for the mygene database, what type of id are the data in `column`. Default is "entrezid".
    * `fields` = a list of fields to annotate for each entry. Terms are found in the mygene documentation.
                - default: `annotate.fields`
    * `verbose` = <True/False>. On True, displays some information about the queries being performed. Helpful to track how close the annotation job is to completion.

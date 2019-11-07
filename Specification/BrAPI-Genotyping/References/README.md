# Group References



## Get - /references/{ID}/bases [/brapi/v1//references/{referenceDbId}/bases] 



### /references/{referenceDbId}/bases [GET /brapi/v1/references/{referenceDbId}/bases{?start}{?end}{?pageToken}]

`POST /listreferencebases` will return a JSON version of
`ListReferenceBasesResponse`.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|nextPageToken|string|The continuation token, which is used to page through large result sets. Provide this value in a subsequent request to return the next page of results. This field will be empty if there aren't any additional results.|
|offset|string (int64)|The offset position (0-based) of the given sequence from the start of this `Reference`. This value will differ for each page in a paginated request.|
|sequence|string|A substring of the bases that make up this reference. Bases are represented as IUPAC-IUB codes; this string matches the regexp `[ACGTMRWSYKVHDBN]*`.|


 

+ Parameters
    + referenceDbId (Required, ) ... The ID of the `Reference` to be retrieved.
    + start (Optional, ) ... The start position (0-based) of this query. Defaults to 0.Genomic positions are non-negative integers less than reference length.Requests spanning the join of circular genomes are represented astwo requests one on each side of the join (position 0).
    + end (Optional, ) ... The end position (0-based, exclusive) of this query. Defaults to the length of this `Reference`.
    + pageToken (Optional, ) ... The continuation token, which is used to page through large result sets.To get the next page of results, set this parameter to the value of`next_page_token` from the previous response.
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "nextPageToken": "nextPageToken",
        "offset": "",
        "sequence": "sequence"
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```

+ Response 404 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - The requested object DbId is not found"
```


## Post - /search/references [/brapi/v1//search/references] 



### /search/references [POST /brapi/v1/search/references]

`POST /references/search` must accept a JSON version of
`SearchReferencesRequest` as the post body and will return a JSON
version of `SearchReferencesResponse`.

**Request Fields** 

|Field|Type|Description|
|---|---|---| 
|accession|string|If specified, return the references for which the `accession` matches this string (case-sensitive, exact match).|
|md5checksum|string|If specified, return the references for which the `md5checksum` matches this string (case-sensitive, exact match). See `ReferenceSet::md5checksum` for details.|
|page_size|integer (int32)|Specifies the maximum number of results to return in a single page. If unspecified, a system default will be used.|
|page_token|string|The continuation token, which is used to page through large result sets. To get the next page of results, set this parameter to the value of `next_page_token` from the previous response.|
|referenceSetDbId|string|The `ReferenceSet` to search.|


**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|searchResultDbId|string||


 

+ Parameters
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>


 
+ Request (application/json)
```
{
    "accession": "accession",
    "md5checksum": "md5checksum",
    "page_size": 0,
    "page_token": "page_token",
    "referenceSetDbId": "referenceSetDbId"
}
```



+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "searchResultDbId": "551ae08c"
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Get - /referencesets [/brapi/v1//referencesets] 



### /referencesets [GET /brapi/v1/referencesets{?referenceSetDbId}{?accession}{?assemblyPUI}{?md5checksum}{?page}{?pageSize}]

`GET /referencesets/{reference_set_id}` will return a JSON version of
`ReferenceSet`.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|data|array[object]||
|additionalInfo|object|Additional arbitrary info|
|assemblyPUI|string|The remaining information is about the source of the sequences Public id of this reference set, such as `GRCh37`.|
|description|string|Optional free text description of this reference set.|
|isDerived|boolean (boolean)|A reference set may be derived from a source if it contains additional sequences, or some of the sequences within it are derived (see the definition of `isDerived` in `Reference`).|
|md5checksum|string|Order-independent MD5 checksum which identifies this `ReferenceSet`.  To compute this checksum, make a list of `Reference.md5checksum` for all `Reference` s in this set. Then sort that list, and take the MD5 hash of all the strings concatenated together. Express the hash as a lower-case hexadecimal string.|
|referenceSetDbId|string|The reference set ID. Unique in the repository.|
|referenceSetName|string|The reference set name.|
|sourceAccessions|array[string]|All known corresponding accession IDs in INSDC (GenBank/ENA/DDBJ) ideally with a version number, e.g. `NC_000001.11`.|
|sourceURI|string|Specifies a FASTA format file/string.|
|species|object||
|term|string|Ontology term - the label of the ontology term the termId is pointing to.|
|termURI|string|Ontology term identifier - the CURIE for an ontology term. It differs from the standard GA4GH schema's :ref:`id ` in that it is a CURIE pointing to an information resource outside of the scope of the schema or its resource implementation.|


 

+ Parameters
    + referenceSetDbId (Optional, ) ... The ID of the `ReferenceSet` to be retrieved.
    + accession (Optional, ) ... If unset, return the reference sets for which the `accession`matches this string (case-sensitive, exact match).
    + assemblyPUI (Optional, ) ... If unset, return the reference sets for which the `assemblyId`matches this string (case-sensitive, exact match).
    + md5checksum (Optional, ) ... If unset, return the reference sets for which the`md5checksum` matches this string (case-sensitive, exact match).See `ReferenceSet::md5checksum` for details.
    + page (Optional, ) ... Which result page is requested. The page indexing starts at 0 (the first page is 'page'= 0). Default is `0`.
    + pageSize (Optional, ) ... The size of the pages to be returned. Default is `1000`.
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "data": [
            {
                "additionalInfo": {},
                "assemblyPUI": "assemblyPUI",
                "description": "description",
                "md5checksum": "md5checksum",
                "referenceSetDbId": "referenceSetDbId",
                "referenceSetName": "referenceSetName",
                "sourceAccessions": [
                    "sourceAccessions1",
                    "sourceAccessions2"
                ],
                "sourceURI": "sourceURI",
                "species": {
                    "term": "term",
                    "termURI": "termURI"
                }
            }
        ]
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Get - /search/references/{ID} [/brapi/v1//search/references/{searchResultsDbId}] 



### /search/references/{searchResultsDbId} [GET /brapi/v1/search/references/{searchResultsDbId}{?page}{?pageSize}]

`POST /references/search` must accept a JSON version of
`SearchReferencesRequest` as the post body and will return a JSON
version of `SearchReferencesResponse`.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|data|array[object]||
|additionalInfo|object|Additional arbitrary info|
|isDerived|boolean (boolean)|A sequence X is said to be derived from source sequence Y, if X and Y are of the same length and the per-base sequence divergence at A/C/G/T bases is sufficiently small. Two sequences derived from the same official sequence share the same coordinates and annotations, and can be replaced with the official sequence for certain use cases.|
|length|string (int64)|The length of this reference's sequence.|
|md5checksum|string|The MD5 checksum uniquely representing this `Reference` as a lower-case hexadecimal string, calculated as the MD5 of the upper-case sequence excluding all whitespace characters (this is equivalent to SQ:M5 in SAM).|
|referenceDbId|string|The reference ID. Unique within the repository.|
|referenceName|string|The unique name of this reference within the Reference Set (e.g. '22').|
|sourceAccessions|array[string]|All known corresponding accession IDs in INSDC (GenBank/ENA/DDBJ) which must include a version number, e.g. `GCF_000001405.26`.|
|sourceDivergence|number (float)|The `sourceDivergence` is the fraction of non-indel bases that do not match the reference this message was derived from.|
|sourceURI|string|The URI from which the sequence was obtained. Specifies a FASTA format file/string with one name, sequence pair. In most cases, clients should call the `getReferenceBases()` method to obtain sequence bases for a `Reference` instead of attempting to retrieve this URI.|
|species|object||
|term|string|Ontology term - the label of the ontology term the termId is pointing to.|
|termURI|string|Ontology term identifier - the CURIE for an ontology term. It differs from the standard GA4GH schema's :ref:`id ` in that it is a CURIE pointing to an information resource outside of the scope of the schema or its resource implementation.|


 

+ Parameters
    + searchResultsDbId (Required, ) ... Permanent unique identifier which references the search results
    + page (Optional, ) ... Which result page is requested. The page indexing starts at 0 (the first page is 'page'= 0). Default is `0`.
    + pageSize (Optional, ) ... The size of the pages to be returned. Default is `1000`.
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "data": [
            {
                "additionalInfo": {},
                "length": "",
                "md5checksum": "md5checksum",
                "referenceDbId": "referenceDbId",
                "referenceName": "referenceName",
                "sourceAccessions": [
                    "sourceAccessions1",
                    "sourceAccessions2"
                ],
                "sourceURI": "sourceURI",
                "species": {
                    "term": "term",
                    "termURI": "termURI"
                }
            }
        ]
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Post - /search/referencesets [/brapi/v1//search/referencesets] 



### /search/referencesets [POST /brapi/v1/search/referencesets]

`POST /referencesets/search` must accept a JSON version of
`SearchReferenceSetsRequest` as the post body and will return a JSON
version of `SearchReferenceSetsResponse`.

**Request Fields** 

|Field|Type|Description|
|---|---|---| 
|accession|string|If unset, return the reference sets for which the `accession` matches this string (case-sensitive, exact match).|
|assemblyPUI|string|If unset, return the reference sets for which the `assemblyId` matches this string (case-sensitive, exact match).|
|md5checksum|string|If unset, return the reference sets for which the `md5checksum` matches this string (case-sensitive, exact match). See `ReferenceSet::md5checksum` for details.|
|page_size|integer (int32)|Specifies the maximum number of results to return in a single page. If unspecified, a system default will be used.|
|page_token|string|The continuation token, which is used to page through large result sets. To get the next page of results, set this parameter to the value of `next_page_token` from the previous response.|


**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|searchResultDbId|string||


 

+ Parameters
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>


 
+ Request (application/json)
```
{
    "accession": "accession",
    "assemblyPUI": "assemblyPUI",
    "md5checksum": "md5checksum",
    "page_size": 0,
    "page_token": "page_token"
}
```



+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "searchResultDbId": "551ae08c"
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Get - /references [/brapi/v1//references] 



### /references [GET /brapi/v1/references{?referenceDbId}{?referenceSetDbId}{?accession}{?md5checksum}{?isDerived}{?minLength}{?maxLength}{?page}{?pageSize}]

`GET /references` will return a filtered list of `Reference` JSON objects.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|data|array[object]||
|additionalInfo|object|Additional arbitrary info|
|isDerived|boolean (boolean)|A sequence X is said to be derived from source sequence Y, if X and Y are of the same length and the per-base sequence divergence at A/C/G/T bases is sufficiently small. Two sequences derived from the same official sequence share the same coordinates and annotations, and can be replaced with the official sequence for certain use cases.|
|length|string (int64)|The length of this reference's sequence.|
|md5checksum|string|The MD5 checksum uniquely representing this `Reference` as a lower-case hexadecimal string, calculated as the MD5 of the upper-case sequence excluding all whitespace characters (this is equivalent to SQ:M5 in SAM).|
|referenceDbId|string|The reference ID. Unique within the repository.|
|referenceName|string|The unique name of this reference within the Reference Set (e.g. '22').|
|sourceAccessions|array[string]|All known corresponding accession IDs in INSDC (GenBank/ENA/DDBJ) which must include a version number, e.g. `GCF_000001405.26`.|
|sourceDivergence|number (float)|The `sourceDivergence` is the fraction of non-indel bases that do not match the reference this message was derived from.|
|sourceURI|string|The URI from which the sequence was obtained. Specifies a FASTA format file/string with one name, sequence pair. In most cases, clients should call the `getReferenceBases()` method to obtain sequence bases for a `Reference` instead of attempting to retrieve this URI.|
|species|object||
|term|string|Ontology term - the label of the ontology term the termId is pointing to.|
|termURI|string|Ontology term identifier - the CURIE for an ontology term. It differs from the standard GA4GH schema's :ref:`id ` in that it is a CURIE pointing to an information resource outside of the scope of the schema or its resource implementation.|


 

+ Parameters
    + referenceDbId (Optional, ) ... The ID of the `Refernce` to be retrieved.
    + referenceSetDbId (Optional, ) ... The ID of the `RefernceSet` to be retrieved.
    + accession (Optional, ) ... If unset, return the reference sets for which the `accession`matches this string (case-sensitive, exact match).
    + md5checksum (Optional, ) ... If specified, return the references for which the`md5checksum` matches this string (case-sensitive, exact match).See `Reference::md5checksum` for details.
    + isDerived (Optional, ) ... If the reference is derived from a source sequence
    + minLength (Optional, ) ... The minimum length of the reference sequences to be retrieved.
    + maxLength (Optional, ) ... The maximum length of the reference sequences to be retrieved.
    + page (Optional, ) ... Which result page is requested. The page indexing starts at 0 (the first page is 'page'= 0). Default is `0`.
    + pageSize (Optional, ) ... The size of the pages to be returned. Default is `1000`.
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "data": [
            {
                "additionalInfo": {},
                "length": "",
                "md5checksum": "md5checksum",
                "referenceDbId": "referenceDbId",
                "referenceName": "referenceName",
                "sourceAccessions": [
                    "sourceAccessions1",
                    "sourceAccessions2"
                ],
                "sourceURI": "sourceURI",
                "species": {
                    "term": "term",
                    "termURI": "termURI"
                }
            }
        ]
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Get - /references/{ID} [/brapi/v1//references/{referenceDbId}] 



### /references/{referenceDbId} [GET /brapi/v1/references/{referenceDbId}]

`GET /references/{reference_id}` will return a JSON version of
`Reference`.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|additionalInfo|object|Additional arbitrary info|
|isDerived|boolean (boolean)|A sequence X is said to be derived from source sequence Y, if X and Y are of the same length and the per-base sequence divergence at A/C/G/T bases is sufficiently small. Two sequences derived from the same official sequence share the same coordinates and annotations, and can be replaced with the official sequence for certain use cases.|
|length|string (int64)|The length of this reference's sequence.|
|md5checksum|string|The MD5 checksum uniquely representing this `Reference` as a lower-case hexadecimal string, calculated as the MD5 of the upper-case sequence excluding all whitespace characters (this is equivalent to SQ:M5 in SAM).|
|referenceDbId|string|The reference ID. Unique within the repository.|
|referenceName|string|The unique name of this reference within the Reference Set (e.g. '22').|
|sourceAccessions|array[string]|All known corresponding accession IDs in INSDC (GenBank/ENA/DDBJ) which must include a version number, e.g. `GCF_000001405.26`.|
|sourceDivergence|number (float)|The `sourceDivergence` is the fraction of non-indel bases that do not match the reference this message was derived from.|
|sourceURI|string|The URI from which the sequence was obtained. Specifies a FASTA format file/string with one name, sequence pair. In most cases, clients should call the `getReferenceBases()` method to obtain sequence bases for a `Reference` instead of attempting to retrieve this URI.|
|species|object||
|term|string|Ontology term - the label of the ontology term the termId is pointing to.|
|termURI|string|Ontology term identifier - the CURIE for an ontology term. It differs from the standard GA4GH schema's :ref:`id ` in that it is a CURIE pointing to an information resource outside of the scope of the schema or its resource implementation.|


 

+ Parameters
    + referenceDbId (Required, ) ... The ID of the `Reference` to be retrieved.




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "additionalInfo": {},
        "length": "",
        "md5checksum": "md5checksum",
        "referenceDbId": "referenceDbId",
        "referenceName": "referenceName",
        "sourceAccessions": [
            "sourceAccessions1",
            "sourceAccessions2"
        ],
        "sourceURI": "sourceURI",
        "species": {
            "term": "term",
            "termURI": "termURI"
        }
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```

+ Response 404 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - The requested object DbId is not found"
```


## Get - /search/referencesets/{ID} [/brapi/v1//search/referencesets/{searchResultsDbId}] 



### /search/referencesets/{searchResultsDbId} [GET /brapi/v1/search/referencesets/{searchResultsDbId}{?page}{?pageSize}]

`POST /referencesets/search` must accept a JSON version of
`SearchReferenceSetsRequest` as the post body and will return a JSON
version of `SearchReferenceSetsResponse`.



**Response Fields** 

|Field|Type|Description|
|---|---|---| 
|data|array[object]||
|additionalInfo|object|Additional arbitrary info|
|assemblyPUI|string|The remaining information is about the source of the sequences Public id of this reference set, such as `GRCh37`.|
|description|string|Optional free text description of this reference set.|
|isDerived|boolean (boolean)|A reference set may be derived from a source if it contains additional sequences, or some of the sequences within it are derived (see the definition of `isDerived` in `Reference`).|
|md5checksum|string|Order-independent MD5 checksum which identifies this `ReferenceSet`.  To compute this checksum, make a list of `Reference.md5checksum` for all `Reference` s in this set. Then sort that list, and take the MD5 hash of all the strings concatenated together. Express the hash as a lower-case hexadecimal string.|
|referenceSetDbId|string|The reference set ID. Unique in the repository.|
|referenceSetName|string|The reference set name.|
|sourceAccessions|array[string]|All known corresponding accession IDs in INSDC (GenBank/ENA/DDBJ) ideally with a version number, e.g. `NC_000001.11`.|
|sourceURI|string|Specifies a FASTA format file/string.|
|species|object||
|term|string|Ontology term - the label of the ontology term the termId is pointing to.|
|termURI|string|Ontology term identifier - the CURIE for an ontology term. It differs from the standard GA4GH schema's :ref:`id ` in that it is a CURIE pointing to an information resource outside of the scope of the schema or its resource implementation.|


 

+ Parameters
    + searchResultsDbId (Required, ) ... Permanent unique identifier which references the search results
    + page (Optional, ) ... Which result page is requested. The page indexing starts at 0 (the first page is 'page'= 0). Default is `0`.
    + pageSize (Optional, ) ... The size of the pages to be returned. Default is `1000`.
    + Authorization (Optional, ) ... HTTP HEADER - Token used for Authorization <strong> Bearer {token_string} </strong>




+ Response 200 (application/json)
```
{
    "metadata": {
        "datafiles": [
            {
                "fileDescription": "This is an Excel data file",
                "fileMD5Hash": "c2365e900c81a89cf74d83dab60df146",
                "fileName": "datafile.xslx",
                "fileSize": 4398,
                "fileType": "application/vnd.ms-excel",
                "fileURL": "https://wiki.brapi.org/examples/datafile.xslx"
            }
        ],
        "pagination": {
            "currentPage": 0,
            "pageSize": 1000,
            "totalCount": 1,
            "totalPages": 1
        },
        "status": [
            {
                "message": "Request accepted, response successful",
                "messageType": "INFO"
            }
        ]
    },
    "result": {
        "data": [
            {
                "additionalInfo": {},
                "assemblyPUI": "assemblyPUI",
                "description": "description",
                "md5checksum": "md5checksum",
                "referenceSetDbId": "referenceSetDbId",
                "referenceSetName": "referenceSetName",
                "sourceAccessions": [
                    "sourceAccessions1",
                    "sourceAccessions2"
                ],
                "sourceURI": "sourceURI",
                "species": {
                    "term": "term",
                    "termURI": "termURI"
                }
            }
        ]
    }
}
```

+ Response 400 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Malformed JSON Request Object\n\nERROR - 2018-10-08T18:15:11Z - Invalid query parameter\n\nERROR - 2018-10-08T18:15:11Z - Required parameter is missing"
```

+ Response 401 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - Missing or expired authorization token"
```

+ Response 403 (application/json)
```
"ERROR - 2018-10-08T18:15:11Z - User does not have permission to perform this action"
```


## Get - /referencesets/{ID} [/brapi/v1//referencesets/{referenceSetDbId}] 



### /referencesets/{referenceSetDbId} [GET /brapi/v1/referencesets/{referenceSetDbId}]

`GET /referencesets/{reference_set_id}` will return a JSON version of
`ReferenceSet`.





 

+ Parameters
    + referenceSetDbId (Required, ) ... The ID of the `ReferenceSet` to be retrieved.




+ Response 200 (application/json)
```
{
    "additionalInfo": {},
    "assemblyPUI": "assemblyPUI",
    "description": "description",
    "md5checksum": "md5checksum",
    "referenceSetDbId": "referenceSetDbId",
    "referenceSetName": "referenceSetName",
    "sourceAccessions": [
        "sourceAccessions1",
        "sourceAccessions2"
    ],
    "sourceURI": "sourceURI",
    "species": {
        "term": "term",
        "termURI": "termURI"
    }
}
```

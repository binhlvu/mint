# List first 100 datasets

```
PREFIX dcat: <http://www.w3.org/ns/dcat#>

select * where { 
    ?s a dcat:Dataset .
} limit 100 
```

# List first 100 datasets from South Sudan

```
PREFIX dcat: <http://www.w3.org/ns/dcat#>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>

select * where { 
    ?s a dcat:Dataset ;
        dct:spatial ?loc.
    ?loc foaf:name "South Sudan".
} limit 100 
```

# Enable GeoSPARQL

```
PREFIX : <http://www.ontotext.com/plugins/geosparql#>

INSERT DATA {
  _:s :enabled "true" .
}
```

# List first 100 datasets within a bounding box


```
PREFIX dcat: <http://www.w3.org/ns/dcat#>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>
PREFIX geof: <http://www.opengis.net/def/function/geosparql/>

select * where { 
    ?s a dcat:Dataset ;
        dct:spatial ?loc.
    ?loc geo:asWKT ?polygon . 
    FILTER(geof:sfContains(?polygon, "Polygon ((11.0 25.0, 11.0 30.0, 4.0 30.0, 4.0 25.0, 11.0 25.0 ))"^^geo:wktLiteral)) .
} limit 100 
```
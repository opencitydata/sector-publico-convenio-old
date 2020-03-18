## Ejemplos de consultas sobre convenios

A continuación se presentan algunos ejemplos de consultas utilizando como referencia un extracto de los  conjuntos de datos de convenios publicados por el ayuntamiento de Madrid y el ayuntamiento de Zaragoza como datos abiertos. Además se han tomado algunos ejemplos  adicionales del portal Web del ayuntamiento de A Coruña.

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid%0D%0A%23+Fecha+fin+posterior+a+1%2F10%2F2019+%28Activos+al+1%2F10%2F2019%29%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT++%3Fnumero+%3Fobjeto+%3FfechaInicio+%3FfechaFin+%3FareaGobierno+%3FnombreEntidad+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A+++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A+++++++%3Forganizacion1+orges%3AambitoCompetencias+%0D%0A++++++++++++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E+.%0D%0A++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio.%0D%0A++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+%0D%0A++++++FILTER%28%3FfechaFin+%3E%3D+%222019-10-01%22%5E%5Exsd%3Adate%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se preguntan los convenios activos del ayuntamiento de Madrid.  
```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>

SELECT  ?numero ?objeto ?fechaInicio ?fechaFin ?areaGobierno ?nombreEntidad 
WHERE {
       ?convenio a esconv:Convenio .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin}
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto }.
       OPTIONAL {?convenio esconv:fechaInicio ?fechaInicio} .
       ?convenio esconv:gestionadoPor ?organizacion1 .
       ?organizacion1 foaf:name ?areaGobierno .
       ?organizacion1 orges:ambitoCompetencias 
            <https://datos.ign.es/recurso/btn100/municipio/28079> .
      ?convenioEntidad esconv:convenioSuscrito  ?convenio.
      ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
      ?organizacion2 foaf:name ?nombreEntidad 
      FILTER(?fechaFin >= "2019-10-01"^^xsd:date)
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A%0D%0A%0D%0A%0D%0ASELECT+DISTINCT++%3Fobjeto+%3FareaGobierno+%3FfechaInicio++%3FfechaFin+%3FnombreEntidad+%3Fcosto%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto%7D+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.+%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto%7D+.++++++++++++++++++++++%0D%0A++++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno++%0D%0A+++++++++FILTER%28+%3Fnumero+%3D+%222019-00716-42B-00001%22%29++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los convenios finalizados del ayuntamiento de Zaragoza que se suscribieron en el año 2019.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>

SELECT  ?numero ?objeto ?fechaInicio ?fechaFin ?fechaSuscripcion ?areaGobierno ?nombreEntidad 
WHERE {
       ?convenio a esconv:Convenio .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin} .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto }.
       OPTIONAL { ?convenio esconv:fechaInicio ?fechaInicio} .
       OPTIONAL { ?convenio esconv:fechaSuscripcion ?fechaSuscripcion} .
       ?convenio esconv:gestionadoPor ?organizacion1 .
       ?organizacion1 foaf:name ?areaGobierno .
       ?organizacion1 orges:ambitoCompetencias <https://datos.ign.es/recurso/btn100/municipio/50297> .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio .
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad 
       FILTER(?fechaFin <= "2019-12-31"^^xsd:date && ?fechaSuscripcion >= "2019-01-01" && ?fechaSuscripcion <= "2019-12-31"^^xsd:date)
}

```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid%0D%0A%23+Materia+Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%0D%0A%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+skos-materia%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprograma-gasto%3E%0D%0A%0D%0A%0D%0ASELECT+DISTINCT+%3Fnumero+%3Fobjeto+%3FfechaFin+%3FnombreEntidad+%3Fcosto%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Amateria+%3Fmateria+.%0D%0A+++++++%3Fmateria+a+skos%3AConcept+.%0D%0A+++++++%3Fmateria+skos%3AprefLabel+%22Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%22%40es+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.++++++++++++++++++++++%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A++++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E++%0D%0A++++++++FILTER%28+%3FfechaFin+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate+%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen  los convenios activos del ayuntamiento de Madrid en materia de actuación de protección y promoción social con coste económico y el total del coste.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX skos-materia:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programa-gasto>


SELECT DISTINCT ?numero ?objeto ?fechaFin ?nombreEntidad ?costo
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:materia ?materia .
       ?materia a skos:Concept .
       ?materia skos:prefLabel "Actuación de protección y promoción social"@es .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin} .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto } .
       ?convenio esconv:obligacionEconomicaAyuntamiento ?costo .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio .
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad .                      
       ?convenio esconv:gestionadoPor ?organizacion1 .
        ?organizacion1 foaf:name ?areaGobierno .
        ?organizacion1 orges:ambitoCompetencias <https://datos.ign.es/recurso/btn100/municipio/28079>  
        FILTER( ?fechaFin <= "2019-12-31"^^xsd:date )
}


```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid%0D%0A%23+Materia+Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%0D%0A%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+skos-materia%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprograma-gasto%3E%0D%0A%0D%0A%0D%0ASELECT+DISTINCT+%3Fnumero+%3Fobjeto+%3FfechaFin+%3FnombreEntidad+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Amateria+%3Fmateria+.%0D%0A+++++++%3Fmateria+a+skos%3AConcept+.%0D%0A+++++++%3Fmateria+skos%3AprefLabel+%22Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%22%40es+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto%7D+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.+%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto%7D+.++++++++++++++++++++++%0D%0A++++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A++++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E++%0D%0A+++++++++FILTER%28+%3FfechaFin+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate+%26%26++%21bound%28%3Fcosto%29++%29++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen  los convenios activos del ayuntamiento de Madrid en materia de actuación de protección y promoción social sin coste económico.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX skos-materia:<http://vocab.linkeddata.es/datosabiertos/kos/hacienda/presupuesto/programa-gasto>


SELECT DISTINCT ?numero ?objeto ?fechaFin ?nombreEntidad 
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:materia ?materia .
       ?materia a skos:Concept .
       ?materia skos:prefLabel "Actuación de protección y promoción social"@es .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin} .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto} .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio .
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad . 
       OPTIONAL {?convenio esconv:obligacionEconomicaAyuntamiento ?costo} .                      
        ?convenio esconv:gestionadoPor ?organizacion1 .
        ?organizacion1 foaf:name ?areaGobierno .
        ?organizacion1 orges:ambitoCompetencias <https://datos.ign.es/recurso/btn100/municipio/28079>  
         FILTER( ?fechaFin <= "2019-12-31"^^xsd:date &&  !bound(?costo)  )  
}


```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A%0D%0A%0D%0A%0D%0ASELECT+DISTINCT++%3Fobjeto+%3FareaGobierno+%3FfechaInicio++%3FfechaFin+%3FnombreEntidad+%3Fcosto%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto%7D+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.+%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto%7D+.++++++++++++++++++++++%0D%0A++++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno++%0D%0A+++++++++FILTER%28+%3Fnumero+%3D+%222019-00716-42B-00001%22%29++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los detalles de un determinado convenio del ayuntamiento de A Coruña.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>



SELECT DISTINCT  ?objeto ?areaGobierno ?fechaInicio  ?fechaFin ?nombreEntidad ?costo
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio  esconv:fechaInicio ?fechaInicio} .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin} .
       OPTIONAL {?convenio esconv:objeto ?objeto} .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio .
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad . 
       OPTIONAL {?convenio esconv:obligacionEconomicaAyuntamiento ?costo} .                      
        ?convenio esconv:gestionadoPor ?organizacion1 .
        ?organizacion1 foaf:name ?areaGobierno  
         FILTER( ?numero = "2019-00716-42B-00001")  
}

```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid+%0D%0A%23+Fecha+fin+posterior+a+1%2F10%2F2019+%28Activos+al+1%2F10%2F2019%29%0D%0A%23+Area+de+gobierno+de+Salud%2C+Seguridad+y+Emergencias%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT++%3Fnumero+%3Fobjeto+%3FfechaInicio+%3FfechaFin++%3FnombreEntidad+%3Fcosto+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D.%0D%0A+++++++OPTIONAL+%7B+%3Fconvenio+esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto+.%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A+++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A+++++++%3Forganizacion1+orges%3AambitoCompetencias+%0D%0A++++++++++++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E+.+%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad%0D%0A+++++++FILTER%28%3FfechaFin+%3E%3D+%222019-10-01%22+%26%26+%3FareaGobierno+%3D+%22%C3%81rea+de+Gobierno+de+Salud%2C+Seguridad+y+Emergencias%22%40es+%29%0D%0A+++++++%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los convenios activos gestionados en Madrid por el área de gobierno de Salud, Seguridad y Emergencia con coste económico y cuánto dinero se destina para cada uno de estos convenios.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>

SELECT  ?numero ?objeto ?fechaInicio ?fechaFin  ?nombreEntidad ?costo 
WHERE {
       ?convenio a esconv:Convenio .
       OPTIONAL {?convenio  esconv:fechaFinalizacion ?fechaFin} .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto }.
       OPTIONAL { ?convenio esconv:fechaInicio ?fechaInicio} .
       ?convenio esconv:obligacionEconomicaAyuntamiento ?costo .
       ?convenio esconv:gestionadoPor ?organizacion1 .
       ?organizacion1 foaf:name ?areaGobierno .
       ?organizacion1 orges:ambitoCompetencias 
            <https://datos.ign.es/recurso/btn100/municipio/28079> . 
       ?convenioEntidad esconv:convenioSuscrito  ?convenio.
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad
       FILTER(?fechaFin >= "2019-10-01" && ?areaGobierno = "Área de Gobierno de Salud, Seguridad y Emergencias"@es )
       }



```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT++%3Fanio+count%28%3Fnumero%29+as+%3FnumeroConvenios+sum%28%3Fcosto%29+as+%3FcosteTotal+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++%3Fconvenio+esconv%3AfechaInicio+%3FfechaInicio+.%0D%0A+++++++%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto+.%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A+++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A+++++++++%3Forganizacion1+orges%3AambitoCompetencias+%0D%0A++++++++++++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E+.+%0D%0A+++++++BIND+%28year%28%3FfechaInicio%29+AS+%3Fanio%29%0D%0A+++++++FILTER+%28%3FfechaInicio+%3E%3D+%222018-01-01%22%5E%5E%0D%0A+++++++xsd%3Adate+%26%26+%3FfechaInicio+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate%29%0D%0A+++++++%7D%0D%0AGROUP+BY+%3Fanio%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene el número de convenios en Madrid y la cuantía en los años 2018 y 2019.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>

SELECT  ?anio count(?numero) as ?numeroConvenios sum(?costo) as ?costeTotal 
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:numero ?numero .
       ?convenio esconv:fechaInicio ?fechaInicio .
       ?convenio esconv:obligacionEconomicaAyuntamiento ?costo .
       ?convenio esconv:gestionadoPor ?organizacion1 .
         ?organizacion1 foaf:name ?areaGobierno .
         ?organizacion1 orges:ambitoCompetencias 
            <https://datos.ign.es/recurso/btn100/municipio/28079> . 
       BIND (year(?fechaInicio) AS ?anio)
       FILTER (?fechaInicio >= "2018-01-01"^^
       xsd:date && ?fechaInicio <= "2019-12-31"^^xsd:date)
       }
GROUP BY ?anio


```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0A%0D%0A%0D%0ASELECT++DISTINCT+%3Fnumero+%3Fobjeto+%3FfechaSuscripcion+%3FfechaFin+%3FareaGobierno+%3FnombreEntidad+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaSuscripcion+%3FfechaSuscripcion%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.%0D%0A+++++++%3Forganizacion2+org%3Aclassification+%3FtipoEntidad+.%0D%0A+++++++%3FtipoEntidad+a+skos%3AConcept+.%0D%0A+++++++%3FtipoEntidad+skos%3AprefLabel+%22Universidad%22%40es++.+++++++++++++++++++++%0D%0A++++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A++++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+++%0D%0A+++++++++++++++++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los convenios suscritos por el ayuntamiento de Zaragoza con universidades.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX org:<http://www.w3.org/ns/org#>


SELECT  DISTINCT ?numero ?objeto ?fechaSuscripcion ?fechaFin ?areaGobierno ?nombreEntidad 
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto } .
       OPTIONAL {?convenio esconv:fechaSuscripcion ?fechaSuscripcion} .
       OPTIONAL {?convenio esconv:fechaFinalizacion ?fechaFin} .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio.
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name ?nombreEntidad .
       ?organizacion2 org:classification ?tipoEntidad .
       ?tipoEntidad a skos:Concept .
       ?tipoEntidad skos:prefLabel "Universidad"@es  .                     
        ?convenio esconv:gestionadoPor ?organizacion1 .
        ?organizacion1 foaf:name ?areaGobierno .
        ?organizacion1 orges:ambitoCompetencias <https://datos.ign.es/recurso/btn100/municipio/50297>   
                 
}


```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0A%0D%0A%0D%0ASELECT++DISTINCT+%3Fnumero+%3Fobjeto+%3FfechaSuscripcion+%3FfechaFin+%3FareaGobierno++%3Fcosto%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaSuscripcion+%3FfechaSuscripcion%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto%7D+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%22UNI%C3%93N+GENERAL+DE+TRABAJADORES+DE+ARAG%C3%93N%22%40es+.++++++++++++++++++++%0D%0A++++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A++++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+++%0D%0A+++++++++++++++++%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los convenios suscritos por el ayuntamiento de Zaragoza con la Unión General de trabajadores de Aragón.

```
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX orges:<http://vocab.linkeddata.es/datosabiertos/def/sector-publico/organizacion#>
PREFIX esconv:<http://vocab.ciudadesabiertas.es/def/sector-publico/convenio#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX skos:<http://www.w3.org/2004/02/skos/core#>
PREFIX org:<http://www.w3.org/ns/org#>


SELECT  DISTINCT ?numero ?objeto ?fechaSuscripcion ?fechaFin ?areaGobierno  ?costo
WHERE {
       ?convenio a esconv:Convenio .
       ?convenio esconv:numero ?numero .
       OPTIONAL {?convenio esconv:objeto ?objeto } .
       OPTIONAL {?convenio esconv:fechaSuscripcion ?fechaSuscripcion} .
       OPTIONAL {?convenio esconv:fechaFinalizacion ?fechaFin} .
       OPTIONAL {?convenio esconv:obligacionEconomicaAyuntamiento ?costo} .
       ?convenioEntidad esconv:convenioSuscrito  ?convenio.
       ?convenioEntidad esconv:entidadSuscriptora ?organizacion2 .
       ?organizacion2 foaf:name "UNIÓN GENERAL DE TRABAJADORES DE ARAGÓN"@es .                    
        ?convenio esconv:gestionadoPor ?organizacion1 .
        ?organizacion1 foaf:name ?areaGobierno .
        ?organizacion1 orges:ambitoCompetencias <https://datos.ign.es/recurso/btn100/municipio/50297>   
                 
}

```




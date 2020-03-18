## Ejemplos de consultas sobre convenios

A continuación se presentan algunos ejemplos de consultas utilizando como referencia un extracto de los  conjuntos de datos de convenios publicados por el ayuntamiento de Madrid y el ayuntamiento de Zaragoza como datos abiertos. Además se han tomado algunos ejemplos  adicionales del portal Web del ayuntamiento de A Coruña.

Por ejemplo, en esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid%0D%0A%23+Fecha+fin+posterior+a+1%2F10%2F2019+%28Activos+al+1%2F10%2F2019%29%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT++%3Fnumero+%3Fobjeto+%3FfechaInicio+%3FfechaFin+%3FareaGobierno+%3FnombreEntidad+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A+++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A+++++++%3Forganizacion1+orges%3AambitoCompetencias+%0D%0A++++++++++++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E+.%0D%0A++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio.%0D%0A++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+%0D%0A++++++FILTER%28%3FfechaFin+%3E%3D+%222019-10-01%22%5E%5Exsd%3Adate%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se preguntan los convenios activos del ayuntamiento de Madrid.  
```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
# Madrid
# Fecha fin posterior a 1/10/2019 (Activos al 1/10/2019)
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
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Zaragoza%0D%0A%23+A%C3%B1o+suscripcion+2019%0D%0A%23+Fecha+fin+%3C%3D+31%2F12%2F2019%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A%0D%0ASELECT++%3Fnumero+%3Fobjeto+%3FfechaInicio+%3FfechaFin+%3FfechaSuscripcion+%3FareaGobierno+%3FnombreEntidad+%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D.%0D%0A+++++++OPTIONAL+%7B+%3Fconvenio+esconv%3AfechaInicio+%3FfechaInicio%7D+.%0D%0A+++++++OPTIONAL+%7B+%3Fconvenio+esconv%3AfechaSuscripcion+%3FfechaSuscripcion%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A+++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A+++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+%0D%0A+++++++FILTER%28%3FfechaFin+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate+%26%26+%3FfechaSuscripcion+%3E%3D+%222019-01-01%22+%26%26+%3FfechaSuscripcion+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se oobtienen los convenios finalizados que se suscribieron en el año 2019.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX org:<http://www.w3.org/ns/org#>

SELECT ?nombreEvento ?fechaInicio  
WHERE{
         ?membresia org:member ?persona .
         ?membresia org:role ?role .
         ?role rdfs:label "Concejala"@es .
         ?membresia org:organization ?unidad .
         ?unidad foaf:name "DELEGACION AREA DE GOBIERNO DE EQUIDAD  DERECHOS SOCIALES Y"@es .
         ?rolIntegranteEvento esagm:integra ?persona .             
	       ?rolIntegranteEvento esagm:evento ?evento .
	       ?evento schema:name ?nombreEvento .
	       ?evento schema:startDate ?fechaInicio .
         FILTER(?fechaInicio >= '2018-04-13T00:00:00'^^xsd:dateTime && ?fechaInicio <= '2018-04-13T23:59:59'^^xsd:dateTime)			
}


```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+esagm-skos-rol%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Frol-integrante%3E%0D%0A%0D%0ASELECT+%3Fdescripcion++%3FfechaInicio+%3FfechaFin+%3FdireccionLugar+%3FnombreIntegrante+%3FcargoLabel+%3ForgNombre+%3FrolLabel+%0D%0AWHERE%7B%0D%0A+++++++++++%3Fevento+schema%3Aname+%22Proyecto+Zaragoza+2018%22%40es+.+%0D%0A%09+OPTIONAL+%7B%3Fevento+schema%3Adescription+%3Fdescripcion%7D+.%0D%0A%09+%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%09+OPTIONAL+%7B%3Fevento+schema%3AendDate+%3FfechaFin%7D+.%0D%0A%09+OPTIONAL+%7B%3Fevento+schema%3Alocation+%3Flugar+.+%3Flugar+schema%3Aaddress+%3FdireccionLugar%7D+.%0D%0A+++++++++++%3FrolIntegranteEvento+esagm%3Aevento++%3Fevento+.+%0D%0A%09%3FrolIntegranteEvento+esagm%3Arol++%3Frol+.%0D%0A+++++++++++%3Frol+skos%3AprefLabel+%3FrolLabel+.%0D%0A+++++++++++%3FrolIntegranteEvento+esagm%3Aintegra+%3Fpersona+.%0D%0A+++++++++++%3Fpersona+foaf%3Aname+%3FnombreIntegrante+.%0D%0A%09+OPTIONAL+%7B%3Fmembresia+org%3Amember+%3Fpersona+.%0D%0A%09%3Fmembresia+org%3Arole+%3Fcargo+.%0D%0A+++++++++++%3Fcargo+rdfs%3Alabel+%3FcargoLabel+.%7D%0D%0A+++++++++++OPTIONAL+%7B%3Fmembresia+org%3Aorganization+%3Forg+.+%3Forg+foaf%3Aname+%3ForgNombre%7D%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los detalles del evento llamado “Proyecto Zaragoza 2018”.

```
# Zaragoza
# Año suscripcion 2019
# Fecha fin <= 31/12/2019
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
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=%23+Madrid%0D%0A%23+Materia+Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%0D%0A%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+orges%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fdef%2Fsector-publico%2Forganizacion%23%3E%0D%0APREFIX+esconv%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fconvenio%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+skos%3A%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+skos-materia%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fhacienda%2Fpresupuesto%2Fprograma-gasto%3E%0D%0A%0D%0A%0D%0ASELECT+DISTINCT+%3Fnumero+%3Fobjeto+%3FfechaFin+%3FnombreEntidad+%3Fcosto%0D%0AWHERE+%7B%0D%0A+++++++%3Fconvenio+a+esconv%3AConvenio+.%0D%0A+++++++%3Fconvenio+esconv%3Amateria+%3Fmateria+.%0D%0A+++++++%3Fmateria+a+skos%3AConcept+.%0D%0A+++++++%3Fmateria+skos%3AprefLabel+%22Actuaci%C3%B3n+de+protecci%C3%B3n+y+promoci%C3%B3n+social%22%40es+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio++esconv%3AfechaFinalizacion+%3FfechaFin%7D+.%0D%0A+++++++%3Fconvenio+esconv%3Anumero+%3Fnumero+.%0D%0A+++++++OPTIONAL+%7B%3Fconvenio+esconv%3Aobjeto+%3Fobjeto+%7D+.%0D%0A+++++++%3Fconvenio+esconv%3AobligacionEconomicaAyuntamiento+%3Fcosto+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AconvenioSuscrito++%3Fconvenio+.%0D%0A+++++++%3FconvenioEntidad+esconv%3AentidadSuscriptora+%3Forganizacion2+.%0D%0A+++++++%3Forganizacion2+foaf%3Aname+%3FnombreEntidad+.++++++++++++++++++++++%0D%0A+++++++%3Fconvenio+esconv%3AgestionadoPor+%3Forganizacion1+.%0D%0A++++++++%3Forganizacion1+foaf%3Aname+%3FareaGobierno+.%0D%0A++++++++%3Forganizacion1+orges%3AambitoCompetencias+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E++%0D%0A++++++++FILTER%28+%3FfechaFin+%3C%3D+%222019-12-31%22%5E%5Exsd%3Adate+%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene Cuales son los convenios activos en materia de Protección y Promoción Social con coste económico y cuál es el total del coste.

```
# Madrid
# Materia Actuación de protección y promoción social

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
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3FnombreEvento+%3FfechaInicio+%0D%0AWHERE%7B%0D%0A%3FrolIntegranteEvento+esagm%3Aintegra+%3Fpersona+.%0D%0A%3Fmembresia+org%3Amember+%3Fpersona+.%0D%0A%3Fmembresia+org%3Arole+%3Fcargo+.%0D%0A%3Fcargo+rdfs%3Alabel+%3FcargoLabel+.+FILTER%28%3FcargoLabel+%3D+%22Alcalde%22%40es+%7C%7C+%3FcargoLabel+%3D+%22Alcaldesa%22%40es%29%0D%0A%3FrolIntegranteEvento+esagm%3Aevento+%3Fevento+.%0D%0A%3Fevento+schema%3Aname+%3FnombreEvento+.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%3Fevento+esagm%3AambitoEvento++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F28079%3E%0D%0AFILTER+%28%3FfechaInicio+%3E%3D+%272018-04-21%27%5E%5Exsd%3AdateTime+%26%26+%3FfechaInicio+%3C+%272018-04-28%27%5E%5Exsd%3AdateTime%29%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene información de cuáles son los eventos que ha tenido el/la alcalde/sa del ayuntamiento de Madrid durante la semana del 21 al 28 de abril de 2018.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX org:<http://www.w3.org/ns/org#>

SELECT DISTINCT ?nombreEvento ?fechaInicio
WHERE{
     ?membresia org:member ?persona .
     ?membresia org:role ?cargo .
     ?cargo rdfs:label ?cargoLabel . FILTER(?cargoLabel = "Alcalde"@es || ?cargoLabel = "Alcaldesa"@es)
     ?rolIntegranteEvento esagm:evento ?evento .
     ?evento schema:name ?nombreEvento .
     ?evento schema:startDate ?fechaInicio .
     ?evento esagm:ambitoEvento  <https://datos.ign.es/recurso/btn100/municipio/28079>
     FILTER (?fechaInicio >= '2018-04-21'^^xsd:dateTime && ?fechaInicio < '2018-04-28'^^xsd:dateTime)
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+foaf%3A%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0A%0D%0ASELECT+DISTINCT+%3FnombreEvento+%3FfechaInicio+%0D%0AWHERE%7B%0D%0A%3FrolIntegranteEvento+esagm%3Aintegra+%3Fpersona+.%0D%0A%3Fmembresia+org%3Amember+%3Fpersona+.%0D%0A%3Fmembresia+org%3Arole+%3Fcargo+.%0D%0A%3Fcargo+rdfs%3Alabel+%3FcargoLabel+.+FILTER%28%3FcargoLabel+%3D+%22Alcalde%22%40es+%7C%7C+%3FcargoLabel+%3D+%22Alcaldesa%22%40es%29%0D%0A%3FrolIntegranteEvento+esagm%3Aevento+%3Fevento+.%0D%0A%3Fevento+schema%3Aname+%3FnombreEvento+.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%3Fevento+esagm%3AambitoEvento+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F09112%3E+.%0D%0AFILTER+%28%3FfechaInicio+%3E%3D+%272018-04-05%27%5E%5Exsd%3AdateTime+%26%26+%3FfechaInicio+%3C+%272018-04-12%27%5E%5Exsd%3AdateTime%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los eventos que ha tenido el/la alcalde/sa del ayuntamiento de A Coruña durante la semana del 5 al 12 de abril de 2018.
```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX foaf:<http://xmlns.com/foaf/0.1/>
PREFIX org:<http://www.w3.org/ns/org#>

SELECT DISTINCT ?nombreEvento ?fechaInicio
WHERE{
     ?rolIntegranteEvento esagm:integra ?persona .
     ?membresia org:member ?persona .
     ?membresia org:role ?cargo .
     ?cargo rdfs:label ?cargoLabel . FILTER(?cargoLabel = "Alcalde"@es || ?cargoLabel = "Alcaldesa"@es)
     ?rolIntegranteEvento esagm:evento ?evento .
     ?evento schema:name ?nombreEvento .
     ?evento schema:startDate ?fechaInicio .
     ?evento esagm:ambitoEvento <https://datos.ign.es/recurso/btn100/municipio/09112> .
     FILTER (?fechaInicio >= '2018-04-05'^^xsd:dateTime && ?fechaInicio < '2018-04-12'^^xsd:dateTime)
}
```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0A%0D%0ASELECT++DISTINCT+%3FnombreEvento+%3FfechaInicio+WHERE+%7B%0D%0A%3Fevento+esagm%3AtipoEvento++esagm-skos-evento%3Apleno+.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%3Fevento+esagm%3AambitoEvento+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+.%0D%0A%3Fevento+schema%3Aname+%3FnombreEvento+.%0D%0AFILTER+%28year%28%3FfechaInicio%29%3E%3D++year%28NOW%28%29%29++%26%26+month%28%3FfechaInicio%29%3E%3D++04+%26%26+year%28%3FfechaInicio%29%3E%3D++01+%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene cuándo se realizarán los próximos eventos de tipo "Sesión de Pleno" del ayuntamiento de Zaragoza (Fecha actual se toma como 01/04/2019).

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>

SELECT  DISTINCT ?nombreEvento ?fechaInicio WHERE {
     ?evento esagm:tipoEvento  esagm-skos-evento:pleno .
     ?evento schema:startDate ?fechaInicio .
     ?evento esagm:ambitoEvento <https://datos.ign.es/recurso/btn100/municipio/50297> .
     ?evento schema:name ?nombreEvento .
     FILTER (year(?fechaInicio)>=  year(NOW())  && month(?fechaInicio)>=  04 && year(?fechaInicio)>=  01 )
}

```
En esta [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0A%0D%0ASELECT+COUNT%28%3Fevento%29+as+%3FnumeroVeces++WHERE+%7B%0D%0A%3Fevento+esagm%3AtipoEvento++esagm-skos-evento%3Acomision-plenaria+.%0D%0A%3Fevento+esagm%3AambitoEvento+%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0AFILTER+%28year%28%3FfechaInicio%29%3E%3D++year%28NOW%28%29%29%29%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se muestra cuántas veces se han reunido las comisiones plenarias de Zaragoza durante el año 2019.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>

SELECT COUNT(?evento) as ?numeroVeces  WHERE {
     ?evento esagm:tipoEvento  esagm-skos-evento:comision-plenaria .
     ?evento esagm:ambitoEvento <https://datos.ign.es/recurso/btn100/municipio/50297> .
     ?evento schema:startDate ?fechaInicio .
     FILTER (year(?fechaInicio)>=  year(NOW()))
}

```
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0A%0D%0ASELECT++%3FnombreEvento+%3FnombreDoc+%3Furi++WHERE+%7B%0D%0A%3Fevento+esagm%3AtipoEvento++esagm-skos-evento%3Aconsejo-de-administracion-empresas-municipales+.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%3Fevento+schema%3Aname+%3FnombreEvento+.%0D%0A%3Fevento+esagm%3Adocumentacion+%3Fdocumentacion+.%0D%0A%3Fevento+esagm%3AambitoEvento++%3Chttps%3A%2F%2Fdatos.ign.es%2Frecurso%2Fbtn100%2Fmunicipio%2F50297%3E+.%0D%0A%3Fdocumentacion+esagm%3AnombreDoc+%3FnombreDoc+.%0D%0A%3Fdocumentacion+esagm%3AuriDoc+%3Furi+.%0D%0A%3Fdocumentacion+esagm%3Apublico+%22true%22%5E%5Exsd%3Aboolean+.+%0D%0AFILTER+%28year%28%3FfechaInicio%29+%3D+2019%29%0D%0A%7D%0D%0A%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtiene la documentación de acceso público asociada con las reuniones de consejos de administración de empresas municipales en el año 2019.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>

SELECT  ?nombreEvento ?nombreDoc ?uri  WHERE {
     ?evento esagm:tipoEvento  esagm-skos-evento:consejo-de-administracion-empresas-municipales .
     ?evento schema:startDate ?fechaInicio .
     ?evento schema:name ?nombreEvento .
     ?evento esagm:documentacion ?documentacion .
     ?evento esagm:ambitoEvento  <https://datos.ign.es/recurso/btn100/municipio/50297> .
     ?documentacion esagm:nombreDoc ?nombreDoc .
     ?documentacion esagm:uriDoc ?uri .
     ?documentacion esagm:publico "true"^^xsd:boolean .
     FILTER (year(?fechaInicio) = 2019)
}
```
En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+skos%3A%3Chttps%3A%2F%2Fwww.w3.org%2F2008%2F05%2Fskos%3E%0D%0APREFIX+org%3A%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Forg%23%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0APREFIX+esagm-skos-rol%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Frol-integrante%2F%3E%0D%0APREFIX+esagm-skos-sesion%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-sesion%2F%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0A%0D%0ASELECT+%3FeventoNombre+%3FfechaInicio+%3FasistenteNombre+%3FasistenteCargo++WHERE+%7B%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.+FILTER+%28%3FfechaInicio+%3E%3D+%272018-01-01T00%3A00%3A00%27%5E%5Exsd%3AdateTime+%29%0D%0A%3Fevento+schema%3Aname+%3FeventoNombre++.%0D%0A%3Fevento+esagm%3AtipoEvento+esagm-skos-evento%3Acomision-plenaria-especial+.%0D%0A%3Fevento+esagm%3AtipoSesion+esagm-skos-sesion%3Aextraordinaria+.%0D%0A%3FrolIntegrante+esagm%3Aevento+%3Fevento+.%0D%0A%3FrolIntegrante+esagm%3Aintegra+%3Fagente+.%0D%0A%3Fagente+foaf%3Aname+%3FasistenteNombre+.%0D%0AOPTIONAL+%7B%3Fmembresia+org%3Amember+%3Fagente+.%0D%0A%3Fmembresia+org%3Arole+%3Fcargo+.%0D%0A%3Fcargo+rdfs%3Alabel+%3FasistenteCargo+.%0D%0A+%7D%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen los asistentes a las reuniones de comisiones plenarias especiales que se han celebrado con carácter extraordinario durante el año 2019.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX skos:<https://www.w3.org/2008/05/skos>
PREFIX org:<http://www.w3.org/ns/org#>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>
PREFIX esagm-skos-rol:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/rol-integrante/>
PREFIX esagm-skos-sesion:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-sesion/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>

SELECT ?eventoNombre ?fechaInicio ?asistenteNombre ?asistenteCargo  WHERE {
     ?evento schema:startDate ?fechaInicio . FILTER (?fechaInicio >= '2018-01-01T00:00:00'^^xsd:dateTime )
     ?evento schema:name ?eventoNombre  .
     ?evento esagm:tipoEvento esagm-skos-evento:comision-plenaria-especial .
     ?evento esagm:tipoSesion esagm-skos-sesion:extraordinaria .
     ?rolIntegrante esagm:evento ?evento .
     ?rolIntegrante esagm:integra ?agente .
     ?agente foaf:name ?asistenteNombre .
     OPTIONAL {?membresia org:member ?agente .
     ?membresia org:role ?cargo .
     ?cargo rdfs:label ?asistenteCargo .
}
}
```

En la siguiente [consulta](http://ciudadesabiertas.linkeddata.es/sparql?default-graph-uri=&query=PREFIX+esagm%3A%3Chttp%3A%2F%2Fvocab.ciudadesabiertas.es%2Fdef%2Fsector-publico%2Fagenda-municipal%23%3E%0D%0APREFIX+schema%3A%3Chttp%3A%2F%2Fschema.org%2F%3E%0D%0APREFIX+esagm-skos-evento%3A%3Chttp%3A%2F%2Fvocab.linkeddata.es%2Fdatosabiertos%2Fkos%2Fsector-publico%2Fagenda-municipal%2Ftipo-evento%2F%3E%0D%0A%0D%0ASELECT+%3FeventoNombre+%3FfechaInicio++WHERE+%7B%0D%0A%3Fevento+schema%3Aname+%3FeventoNombre++.%0D%0A%3Fevento+schema%3AstartDate+%3FfechaInicio+.%0D%0A%3Fevento+esagm%3AtipoEvento+esagm-skos-evento%3Areunion-con-empresas+.%0D%0A%3Fevento+esagm%3AreunionLobby+%22true%22%5E%5Exsd%3Aboolean+.+%0D%0A%7D%0D%0A&format=text%2Fhtml&timeout=0&debug=on&run=+Run+Query+) se obtienen las reuniones de Lobby que se han realizado con empresas.

```
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX skos:<https://www.w3.org/2008/05/skos>
PREFIX org:<http://www.w3.org/ns/org#>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>
PREFIX esagm-skos-rol:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/rol-integrante/>
PREFIX esagm-skos-sesion:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-sesion/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>
PREFIX esagm:<http://vocab.ciudadesabiertas.es/def/sector-publico/agenda-municipal#>
PREFIX schema:<http://schema.org/>
PREFIX esagm-skos-evento:<http://vocab.linkeddata.es/datosabiertos/kos/sector-publico/agenda-municipal/tipo-evento/>

SELECT ?eventoNombre ?fechaInicio  WHERE {
     ?evento schema:name ?eventoNombre  .
     ?evento schema:startDate ?fechaInicio .
     ?evento esagm:tipoEvento esagm-skos-evento:reunion-con-empresas .
     ?evento esagm:reunionLobby "true"^^xsd:boolean .
}

```


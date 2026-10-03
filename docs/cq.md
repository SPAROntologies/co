## Competency Questions

CO can be used for answering several questions related to different ways entities can be grouped into aggregates and organized into collections.
In the following subsections, some of them are introduced together with their respective SPARQL queries. 

The prefixes that are used in all the SPARQL queries provided below are defined as follows:
        
        PREFIX : <http://www.sparontologies.net/example/>
        PREFIX co: <http://purl.org/co/>

### CQ1

What are the entities that belong to a collection?

        SELECT DISTINCT ?collection ?element
        WHERE {
            ?collection co:element|co:item/co:itemContent ?element .
        }

### CQ2

How many times does each entity appear in a bag?

        SELECT ?element (COUNT(?item) AS ?occurrences)
        WHERE {
            :citations co:item ?item .
            ?item co:itemContent ?element .
        }
        GROUP BY ?element

### CQ3

What is the size of a collection?

        SELECT ?collection ?size
        WHERE {
            ?collection co:size ?size .
        }

### CQ4

What are the first entity and the last entity of a list?

        SELECT ?first ?last
        WHERE {
            :authors co:firstItem/co:itemContent ?first ;
                co:lastItem/co:itemContent ?last .
        }

### CQ5

Which entity is at a given position of a list?

        SELECT ?element
        WHERE {
            :authors co:item ?item .
            ?item co:index ?index ;
                co:itemContent ?element .
            FILTER (?index = 2)
        }
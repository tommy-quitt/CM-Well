# Function: *Delete or Replace Values in a Named Sub-Graph* #

## Description ##

If you have created a named sub-graph, you can replace the entire sub-graph with a single API call, using the special **#replaceGraph** predicate. You can choose to just delete the sub-graph, or to delete the existing values and add new values in the same call.

In the call's payload, you first supply a triple that deletes the sub-graph, and then optionally add quads that contain the new graph values.

>**Note:** You can also create a simple string alias for the graph name URI. See [Using String Labels as Sub-Graph Aliases](DevGuide.WorkingWithNamedSub-Graphs.md#NamedGraphAliases) to learn more.

## Syntax ##

**URL:** \<cm-well-host\>/_in
**REST verb:** POST
**Mandatory parameters:** <> <cmwell://meta/sys#replaceGraph> <graph to delete/replace> <optional: quads to add>

----------

**Template:**

    curl -X POST "<cm-well-host>/_in?format=nquads" -H "Content-Type: text/plain" --data 
    '<> <cmwell://meta/sys#replaceGraph> <graph to replace>.
    <quads to add>'

**URL example:** N/A

**Curl example (REST API):**

    curl -X POST "<cm-well-host>/_in?format=nquads" -H "Content-Type: text/plain" --data-binary @curlInput.txt

### File Contents ###
    <> <cmwell://meta/sys#replaceGraph> <http://MyOntology/MovieGoers>. 
    <http://example.org/movies/ET> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.
    <http://example.org/movies/GoneWithTheWind> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.
    <http://example.org/movies/TheAvenger> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.

## Code Example ##

### Call ###

    curl -X POST "<cm-well-host>/_in?format=nquads" -H "Content-Type: text/plain" --data-binary @curlInput.txt

### File Contents ###
    <> <cmwell://meta/sys#replaceGraph> <http://MyOntology/MovieGoers>. 
    <http://example.org/movies/ET> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.
    <http://example.org/movies/GoneWithTheWind> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.
    <http://example.org/movies/TheAvenger> <http://MyOntology/Score> "10" <http://MyOntology/MovieGoers>.

### Results ###
    
    {"success":true}

## Notes ##

If you want to replace values in a sub-graph, the best practice is to delete the old values and add the new values, all in the same call. This is because for every change made to an infoton, CM-Well retains a historical infoton version. If you split the operation into two calls, one to delete and one to add, the version after the delete is saved. This version is not interesting when tracing the infoton's history, and just takes up storage needlessly. 

## Related Topics ##
[Working with Named Sub-Graphs](DevGuide.WorkingWithNamedSub-Graphs.md)
[Add Infotons and Fields to a Sub-Graph](API.Update.AddInfotonsAndFieldsToSubGraph.md)

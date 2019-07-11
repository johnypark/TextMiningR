First lesson.
================
John Park
July 11, 2019

Get metadata from journal
-------------------------

This is the first tutorial about using crossref API for getting text data from literatures. CrossRef API <https://github.com/CrossRef/rest-api-doc>.

``` r
## example of work retrieving from jouranl 'landscape ecology'
all.lands.ecol<-cr_works(filter=c(issn='15729761-09212973'))
```

using crossref api: the command is, <https://api.crossref.org/works?facet=license:*&filter=issn:15729761-09212973>

result is the same for crossref api and rcrossref.

I have digged this for an hour, but not sure how to list the data in this format I want:

id |title | year | citation

the result

``` r
all.lands.ecol$data$title
```

    ##  [1] "High-resolution maps of forest-urban watersheds present an opportunity for ecologists and managers"                                                        
    ##  [2] "Northern prairie songbirds are more strongly influenced by grassland configuration than grassland amount"                                                  
    ##  [3] "Wildfire and exotic grass invasion alter plant productivity in response to climate variability in the Mojave Desert"                                       
    ##  [4] "Landscape and local correlates with anuran taxonomic, functional and phylogenetic diversity in rice crops"                                                 
    ##  [5] "The impact of urban expansion on the regional environment in Myanmar: a case study of two capital cities"                                                  
    ##  [6] "Forest management impacts on capercaillie (Tetrao urogallus) habitat distribution and connectivity in the Carpathians"                                     
    ##  [7] "Landscape Ecology"                                                                                                                                         
    ##  [8] "Spatial prioritisation for conserving ecosystem services: comparing hotspots with heuristic optimisation"                                                  
    ##  [9] "Patterns of bird predation on reptiles in small woodland remnant edges in peri-urban north-western Sydney, Australia"                                      
    ## [10] "Global analysis and simulation of land-use change associated with urbanization"                                                                            
    ## [11] "Towards a comprehensive framework for modeling urban spatial dynamics"                                                                                     
    ## [12] "Targeting and evaluating biodiversity conservation action within fragmented landscapes: an approach based on generic focal species and least-cost networks"
    ## [13] "Landscape of culture and culture of landscape: does landscape ecology need culture?"                                                                       
    ## [14] "Aligning landscape structure with ecosystem services along an urban<U+2013>rural gradient. Trade-offs and transitions towards cultural services"           
    ## [15] "Effects of Intensive Forest Management on Stand and Landscape Characteristics in Northern New Brunswick, Canada (1945<U+2013>2027)"                        
    ## [16] "How does the landscape context of occurrence data influence models of invasion risk? A comparison of independent datasets in Massachusetts, USA"           
    ## [17] "Perceived land use patterns and landscape values"                                                                                                          
    ## [18] "Linking ecosystem services with landscape history"                                                                                                         
    ## [19] "Differences in time and space in vegetation patterning: analysis of pollen data from Dartmoor, UK"                                                         
    ## [20] "Network analysis reveals strong seasonality in the dispersal of a marine parasite and identifies areas for coordinated management"

Only gives the title of 20 article, whereas

``` r
all.lands.ecol$meta
```

    ##   total_results search_terms start_index items_per_page
    ## 1          2374           NA           0             20

Gives total search results of 2374 journals. It must have something to do with items\_per\_page entry, which is 20. I just need to figure out how to fetch the data, I guess.

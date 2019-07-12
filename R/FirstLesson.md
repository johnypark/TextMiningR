First lesson.
================
John Park
July 11, 2019

Get metadata from journal
-------------------------

This is the first tutorial about using crossref API for getting text data from literatures. CrossRef API <https://github.com/CrossRef/rest-api-doc>.

``` r
## example of work retrieving from jouranl 'landscape ecology'
issn.target='15729761-09212973'
DownPubs=cr_works(filter=c(issn=issn.target))
```

using crossref api: the command is, <https://api.crossref.org/works?facet=license:*&filter=issn:15729761-09212973>

result is the same for crossref api and rcrossref.

Since cr\_works only takes first 20 data points, set offset and do recurrent download based on the total number of publications found in the journal.

``` r
n_pages <- ceiling(DownPubs$meta$total_results / DownPubs$meta$items_per_page)

ls.pubs<-c(1:n_pages)%>%lapply(.,function(x){ n_line <- (x - 1)*20 + 1;
return( cr_works(filter = c(issn=issn.target), offset = n_line)$data )
})
```

    ## Warning: 500 (server error): /works - Direct buffer memory

    ## Warning: 500 (server error): /works - Direct buffer memory

    ## Warning: 500 (server error): /works - Direct buffer memory

    ## Warning: 500 (server error): /works - Direct buffer memory

    ## Warning: 500 (server error): /works - Direct buffer memory

``` r
for (i in 1:n_pages){
  if(is.null(ls.pubs[[i]])==FALSE){
  ls.pubs[[i]]<-ls.pubs[[i]]%>%select(title,author,issued)
  }
}
ls.pubs<-do.call("rbind",ls.pubs)
ls.pubs
```

    ## # A tibble: 2,273 x 3
    ##    title                                             author        issued  
    ##  * <chr>                                             <list>        <chr>   
    ##  1 Northern prairie songbirds are more strongly inf~ <tibble [2 x~ 2018-07~
    ##  2 Wildfire and exotic grass invasion alter plant p~ <tibble [2 x~ 2016-11~
    ##  3 Urban sustainability: an inevitable goal of land~ <tibble [1 x~ 2009-12~
    ##  4 Landscape services as a bridge between landscape~ <tibble [2 x~ 2009-01~
    ##  5 Processes and driving forces in changing cultura~ <tibble [11 ~ 2017-04~
    ##  6 "Driving forces of landscape change \u2013 curre~ <tibble [3 x~ 2004-11 
    ##  7 Urban landscape sustainability and resilience: t~ <tibble [1 x~ 2012-09~
    ##  8 Interaction of food resources and landscape stru~ <tibble [2 x~ 2007-12~
    ##  9 The impact of urbanization and climate change on~ <tibble [5 x~ 2017-08~
    ## 10 Quantifying Spatiotemporal Patterns of Urban Lan~ <tibble [2 x~ 2005-11 
    ## # ... with 2,263 more rows

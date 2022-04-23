Data Inspection for Final Project
================
2022-04-20

First, I will load in the packages (tidyverse, lemon, knitr). This code
is in the script but not knit to the markdown document for readability.

I also read in the “DS-KROK4BDJ.txt” file, which is a tsv downloaded
from our paper of choice and (I believe) contains all the data we will
need to work with, including sample IDs, geographic information, and
sequences.

After reading in the file, I inspect the column dimensions

``` r
dim(bdj)
```

    ## [1] 124  80

There are 80 columns and 124 rows in this file. Next check out column
names.

``` r
kable(column_names)
```

| x                          |
|:---------------------------|
| processid                  |
| sampleid                   |
| recordID                   |
| catalognum                 |
| fieldnum                   |
| institution_storing        |
| collection_code            |
| bin_uri                    |
| phylum_taxID               |
| phylum_name                |
| class_taxID                |
| class_name                 |
| order_taxID                |
| order_name                 |
| family_taxID               |
| family_name                |
| subfamily_taxID            |
| subfamily_name             |
| genus_taxID                |
| genus_name                 |
| species_taxID              |
| species_name               |
| subspecies_taxID           |
| subspecies_name            |
| identification_provided_by |
| identification_method      |
| identification_reference   |
| tax_note                   |
| voucher_status             |
| tissue_type                |
| collection_event_id        |
| collectors                 |
| collectiondate_start       |
| collectiondate_end         |
| collectiontime             |
| collection_note            |
| site_code                  |
| sampling_protocol          |
| lifestage                  |
| sex                        |
| reproduction               |
| habitat                    |
| associated_specimens       |
| associated_taxa            |
| extrainfo                  |
| notes                      |
| lat                        |
| lon                        |
| coord_source               |
| coord_accuracy             |
| elev                       |
| depth                      |
| elev_accuracy              |
| depth_accuracy             |
| country                    |
| province_state             |
| region                     |
| sector                     |
| exactsite                  |
| image_ids                  |
| image_urls                 |
| media_descriptors          |
| captions                   |
| copyright_holders          |
| copyright_years            |
| copyright_licenses         |
| copyright_institutions     |
| photographers              |
| sequenceID                 |
| markercode                 |
| genbank_accession          |
| nucleotides                |
| trace_ids                  |
| trace_names                |
| trace_links                |
| run_dates                  |
| sequencing_centers         |
| directions                 |
| seq_primers                |
| marker_codes               |

Let’s look at the first 5 rows in this file. It’s a large chunk, but
very interesting. Scroll side to side to see the whole chunk.

``` r
kable(bdj[1:5, ])
```

| processid  | sampleid | recordID | catalognum | fieldnum | institution_storing                           | collection_code | bin_uri      | phylum_taxID | phylum_name | class_taxID | class_name | order_taxID | order_name | family_taxID | family_name | subfamily_taxID | subfamily_name | genus_taxID | genus_name   | species_taxID | species_name             | subspecies_taxID | subspecies_name | identification_provided_by | identification_method | identification_reference | tax_note | voucher_status | tissue_type | collection_event_id | collectors                                                | collectiondate_start | collectiondate_end | collectiontime | collection_note | site_code | sampling_protocol   | lifestage | sex | reproduction | habitat              | associated_specimens | associated_taxa | extrainfo | notes |    lat |    lon | coord_source | coord_accuracy | elev | depth | elev_accuracy | depth_accuracy | country  | province_state | region   | sector | exactsite            | image_ids | image_urls | media_descriptors | captions | copyright_holders | copyright_years | copyright_licenses | copyright_institutions | photographers | sequenceID | markercode | genbank_accession | nucleotides                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | trace_ids          | trace_names                                | trace_links                                                                                                          | run_dates                                | sequencing_centers                 | directions | seq_primers      | marker_codes   |
|:-----------|:---------|---------:|:-----------|:---------|:----------------------------------------------|:----------------|:-------------|-------------:|:------------|------------:|:-----------|------------:|:-----------|-------------:|:------------|----------------:|:---------------|------------:|:-------------|--------------:|:-------------------------|:-----------------|:----------------|:---------------------------|:----------------------|:-------------------------|:---------|:---------------|:------------|:--------------------|:----------------------------------------------------------|:---------------------|:-------------------|:---------------|:----------------|:----------|:--------------------|:----------|:----|:-------------|:---------------------|:---------------------|:----------------|:----------|:------|-------:|-------:|:-------------|:---------------|-----:|:------|:--------------|:---------------|:---------|:---------------|:---------|:-------|:---------------------|----------:|:-----------|:------------------|:---------|:------------------|----------------:|:-------------------|:-----------------------|:--------------|-----------:|:-----------|:------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------|:-------------------------------------------|:---------------------------------------------------------------------------------------------------------------------|:-----------------------------------------|:-----------------------------------|:-----------|:-----------------|:---------------|
| KROK004-19 | CLPT-004 | 10924772 | CLPT-004   | NA       | University of Ljubljana, Biotechnical Faculty | NA              | BOLD:ABA5411 |           20 | Arthropoda  |          82 | Insecta    |         413 | Coleoptera |          948 | Carabidae   |            2933 | Harpalinae     |      403088 | Licinus      |        403089 | Licinus hoffmannseggii   | NA               | NA              | Urska Ratajc               | Stereomicroscope      | NA                       | NA       | NA             | NA          | NA                  | Zan Kuralt, Neza Pajek Arambasic, Maja Ferle, Franc Kljun | NA                   | NA                 | NA             | NA              | NA        | pitfall traps       | adult     | F   | NA           | Dinaric beech forest | NA                   | NA              | NA        | NA    | 45.539 | 14.760 | NA           | NA             | 1108 | NA    | NA            | NA             | Slovenia | NA             | Kocevska | NA     | Borovec mountain     |        NA | NA         | NA                | NA       | NA                |              NA | NA                 | NA                     | NA            |   12447477 | COI-5P     | MT994111          | AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT | 11609303\|11609302 | CLPT-004_LCO1490.ab1\|CLPT-004_HCO2198.ab1 | <http://trace.boldsystems.org/traceIO/bold.org/13428409&#124;http://trace.boldsystems.org/traceIO/bold.org/13428408> | 2019-10-25 10:24:30\|2019-10-25 12:37:54 | Macrogen, Europe\|Macrogen, Europe | F\|R       | LCO1490\|HCO2198 | COI-5P\|COI-5P |
| KROK005-19 | CLPT-005 | 10924773 | CLPT-005   | NA       | University of Ljubljana, Biotechnical Faculty | NA              | BOLD:AAX7561 |           20 | Arthropoda  |          82 | Insecta    |         413 | Coleoptera |          948 | Carabidae   |            2933 | Harpalinae     |        2920 | Pterostichus |        373903 | Pterostichus burmeisteri | NA               | NA              | Urska Ratajc               | Stereomicroscope      | NA                       | NA       | NA             | NA          | NA                  | Zan Kuralt, Neza Pajek Arambasic, Maja Ferle, Franc Kljun | NA                   | NA                 | NA             | NA              | NA        | pitfall traps       | adult     | F   | NA           | Dinaric beech forest | NA                   | NA              | NA        | NA    | 45.539 | 14.760 | NA           | NA             | 1108 | NA    | NA            | NA             | Slovenia | NA             | Kocevska | NA     | Borovec mountain     |        NA | NA         | NA                | NA       | NA                |              NA | NA                 | NA                     | NA            |   12447478 | COI-5P     | MT994134          | AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGATCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCCATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT | 11609304\|11609305 | CLPT-005_HCO2198.ab1\|CLPT-005_LCO1490.ab1 | <http://trace.boldsystems.org/traceIO/bold.org/13428410&#124;http://trace.boldsystems.org/traceIO/bold.org/13428411> | 2019-10-25 12:37:54\|2019-10-25 10:24:30 | Macrogen, Europe\|Macrogen, Europe | R\|F       | HCO2198\|LCO1490 | COI-5P\|COI-5P |
| KROK008-19 | CLPT-015 | 10924776 | CLPT-015   | NA       | University of Ljubljana, Biotechnical Faculty | NA              | BOLD:AAN9386 |           20 | Arthropoda  |          82 | Insecta    |         413 | Coleoptera |          948 | Carabidae   |            2933 | Harpalinae     |      226200 | Abax         |        226201 | Abax ovalis              | NA               | NA              | Urska Ratajc               | Stereomicroscope      | NA                       | NA       | NA             | NA          | NA                  | Zan Kuralt, Neza Pajek Arambasic, Maja Ferle, Franc Kljun | NA                   | NA                 | NA             | NA              | NA        | pitfall traps       | adult     | F   | NA           | Dinaric beech forest | NA                   | NA              | NA        | NA    | 45.539 | 14.764 | NA           | NA             | 1113 | NA    | NA            | NA             | Slovenia | NA             | Kocevska | NA     | Krokar virgin forest |        NA | NA         | NA                | NA       | NA                |              NA | NA                 | NA                     | NA            |   12447481 | COI-5P     | MT994068          | AAGATATTGGAACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCCATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTAGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATA    | 11609310\|11609311 | CLPT-015_HCO2198.ab1\|CLPT-015_LCO1490.ab1 | <http://trace.boldsystems.org/traceIO/bold.org/13428416&#124;http://trace.boldsystems.org/traceIO/bold.org/13428417> | 2019-10-25 12:37:54\|2019-10-25 10:24:30 | Macrogen, Europe\|Macrogen, Europe | R\|F       | HCO2198\|LCO1490 | COI-5P\|COI-5P |
| KROK010-19 | CLPT-017 | 10924778 | CLPT-017   | NA       | University of Ljubljana, Biotechnical Faculty | NA              | BOLD:AAO0964 |           20 | Arthropoda  |          82 | Insecta    |         413 | Coleoptera |          948 | Carabidae   |          312806 | Nebriinae      |       90118 | Notiophilus  |        167827 | Notiophilus biguttatus   | NA               | NA              | Urska Ratajc               | Stereomicroscope      | Fabricius                | NA       | NA             | NA          | NA                  | Zan Kuralt, Neza Pajek Arambasic, Maja Ferle, Franc Kljun | NA                   | NA                 | NA             | NA              | NA        | leaf litter sifting | adult     | NA  | NA           | Dinaric beech forest | NA                   | NA              | NA        | NA    | 45.539 | 14.765 | NA           | NA             | 1134 | NA    | NA            | NA             | Slovenia | NA             | Kocevska | NA     | Krokar virgin forest |        NA | NA         | NA                | NA       | NA                |              NA | NA                 | NA                     | NA            |   12447483 | COI-5P     | MT994131          | AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATAT | 11609314\|11609315 | CLPT-017_HCO2198.ab1\|CLPT-017_LCO1490.ab1 | <http://trace.boldsystems.org/traceIO/bold.org/13428420&#124;http://trace.boldsystems.org/traceIO/bold.org/13428421> | 2019-10-25 12:37:54\|2019-10-25 10:24:30 | Macrogen, Europe\|Macrogen, Europe | R\|F       | HCO2198\|LCO1490 | COI-5P\|COI-5P |
| KROK011-19 | CLPT-018 | 10924779 | CLPT-018   | NA       | University of Ljubljana, Biotechnical Faculty | NA              | BOLD:ACR9475 |           20 | Arthropoda  |          82 | Insecta    |         413 | Coleoptera |          948 | Carabidae   |           89439 | Carabinae      |        3019 | Carabus      |        660646 | Carabus creutzeri        | NA               | NA              | Urska Ratajc               | Stereomicroscope      | NA                       | NA       | NA             | NA          | NA                  | Zan Kuralt, Neza Pajek Arambasic, Maja Ferle, Franc Kljun | NA                   | NA                 | NA             | NA              | NA        | pitfall traps       | adult     | F   | NA           | Dinaric beech forest | NA                   | NA              | NA        | NA    | 45.539 | 14.765 | NA           | NA             | 1134 | NA    | NA            | NA             | Slovenia | NA             | Kocevska | NA     | Krokar virgin forest |        NA | NA         | NA                | NA       | NA                |              NA | NA                 | NA                     | NA            |   12447484 | COI-5P     | MT994074          | AACTTTATATTTTATTTTTGGTGCTTGATCAGGAATAGTGGGAACTTCTTTAAGAATACTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTAACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGAGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTAGGAATAACCTTTGATCGAATACCTTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTACTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTCTAACAGACCGTAATTTAAATACTTCTTTTTTCGATCCAGCTGGGGGAGGTGACCCAATTTTATACCAACATTTATTT | 11609316\|11609317 | CLPT-018_HCO2198.ab1\|CLPT-018_LCO1490.ab1 | <http://trace.boldsystems.org/traceIO/bold.org/13428422&#124;http://trace.boldsystems.org/traceIO/bold.org/13428423> | 2019-10-25 12:37:54\|2019-10-25 10:24:30 | Macrogen, Europe\|Macrogen, Europe | R\|F       | HCO2198\|LCO1490 | COI-5P\|COI-5P |

From this point, we can pick out columns that we want to work with. For
practice, I will select the phylum-subspecies taxID and name columns (14
columns total) and convert them to factor. After this (hidden) code
chunk, the “bdj” object (our data) columns with these names will be
converted from “numeric” or “character” to “factor”. Since they are now
factors, we can run other analyses on them and visualize how many of
each, etc.

(The code is here, trust me. Check the Rmd file if you want to see it)

Next check out the various family names in this file.

(note: I’m just doing all this to inspect the file, we don’t have to use
these processes.)

``` r
unique(bdj$family_name) %>% as.matrix(family_name) -> family_name_view
kable(family_name_view)
```

|                   |
|:------------------|
| Carabidae         |
| Geophilidae       |
| Linotaeniidae     |
| Mecistocephalidae |
| Lithobiidae       |
| Cryptopidae       |
| Agelenidae        |
| Anapidae          |
| Clubionidae       |
| Dysderidae        |
| Gnaphosidae       |
| Theridiidae       |
| Linyphiidae       |
| Lycosidae         |
| Miturgidae        |
| Segestriidae      |
| Schendylidae      |
| Araneidae         |
| Staphylinidae     |
| Elateridae        |
| Amaurobiidae      |
| Hahniidae         |

I’d like to visualize how many samples per family we have. In other
words, how many “Therididae”? How many “Anapidae”?

I’ll use ggplot to do this.

``` r
ggplot(bdj, aes(x=reorder(family_name, family_name, function(x)-length(x)),fill=family_name)) +
  geom_bar() +
  labs(title="Individuals per Family", 
         x="Family Name", y = "Count") +
  theme(axis.text.x = element_text(angle = 90))
```

![](data_inspection_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

That looks so cool and I want to do another one. This one will be genus.

``` r
ggplot(bdj, aes(x=reorder(genus_name, genus_name, function(x)-length(x)),fill=genus_name)) +
  geom_bar() +
  labs(title="Individuals per Genus", 
         x="Family Name", y = "Count") +
  theme(axis.text.x = element_text(angle = 90)) +
  theme(legend.position="none") 
```

![](data_inspection_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

Not very easy to read but the colors are colorful.

``` r
phylo <- bdj
view(phylo)
```

Now we prepare to retrieve the BOLD sequence data.

``` r
phylo1 <- phylo%>%add_column(retrieved_seq = NA )%>%select(1:8,81,everything())
view(phylo1)
```

We have created the empty column where sequences from BOLD will be put.

``` r
slicey <- phylo1%>%slice(1:10)
view(slicey)
```

Created slicey to practice on

``` r
check<- bold_seq(bin=slicey$bin_uri)
check
```

    ## [[1]]
    ## [[1]]$id
    ## [1] "COLFE328-12"
    ## 
    ## [[1]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[1]]$gene
    ## [1] "COLFE328-12"
    ## 
    ## [[1]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[2]]
    ## [[2]]$id
    ## [1] "EUCAR1265-15"
    ## 
    ## [[2]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[2]]$gene
    ## [1] "EUCAR1265-15"
    ## 
    ## [[2]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGA"
    ## 
    ## 
    ## [[3]]
    ## [[3]]$id
    ## [1] "EUCAR1269-15"
    ## 
    ## [[3]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[3]]$gene
    ## [1] "EUCAR1269-15"
    ## 
    ## [[3]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[4]]
    ## [[4]]$id
    ## [1] "EUCAR1375-15"
    ## 
    ## [[4]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[4]]$gene
    ## [1] "EUCAR1375-15"
    ## 
    ## [[4]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[5]]
    ## [[5]]$id
    ## [1] "EUCAR1378-15"
    ## 
    ## [[5]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[5]]$gene
    ## [1] "EUCAR1378-15"
    ## 
    ## [[5]]$sequence
    ## [1] "GCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[6]]
    ## [[6]]$id
    ## [1] "EUCAR1401-15"
    ## 
    ## [[6]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[6]]$gene
    ## [1] "EUCAR1401-15"
    ## 
    ## [[6]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[7]]
    ## [[7]]$id
    ## [1] "EUCAR1402-15"
    ## 
    ## [[7]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[7]]$gene
    ## [1] "EUCAR1402-15"
    ## 
    ## [[7]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[8]]
    ## [[8]]$id
    ## [1] "EUCAR1599-16"
    ## 
    ## [[8]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[8]]$gene
    ## [1] "EUCAR1599-16"
    ## 
    ## [[8]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[9]]
    ## [[9]]$id
    ## [1] "EUCAR1758-17"
    ## 
    ## [[9]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[9]]$gene
    ## [1] "EUCAR1758-17"
    ## 
    ## [[9]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[10]]
    ## [[10]]$id
    ## [1] "EUCAR1759-17"
    ## 
    ## [[10]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[10]]$gene
    ## [1] "EUCAR1759-17"
    ## 
    ## [[10]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[11]]
    ## [[11]]$id
    ## [1] "EUCAR1760-17"
    ## 
    ## [[11]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[11]]$gene
    ## [1] "EUCAR1760-17"
    ## 
    ## [[11]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[12]]
    ## [[12]]$id
    ## [1] "EUCAR1771-17"
    ## 
    ## [[12]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[12]]$gene
    ## [1] "EUCAR1771-17"
    ## 
    ## [[12]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[13]]
    ## [[13]]$id
    ## [1] "FBCOA331-10"
    ## 
    ## [[13]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[13]]$gene
    ## [1] "FBCOA331-10"
    ## 
    ## [[13]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[14]]
    ## [[14]]$id
    ## [1] "FBCOA591-10"
    ## 
    ## [[14]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[14]]$gene
    ## [1] "FBCOA591-10"
    ## 
    ## [[14]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATCCGGGCTGAATTAGGTAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCGGTTGACTTGGCTATTTTTAGTTTGCATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[15]]
    ## [[15]]$id
    ## [1] "FBCOD003-11"
    ## 
    ## [[15]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[15]]$gene
    ## [1] "FBCOD003-11"
    ## 
    ## [[15]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[16]]
    ## [[16]]$id
    ## [1] "FBCOD036-11"
    ## 
    ## [[16]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[16]]$gene
    ## [1] "FBCOD036-11"
    ## 
    ## [[16]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[17]]
    ## [[17]]$id
    ## [1] "FBCOF1119-12"
    ## 
    ## [[17]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[17]]$gene
    ## [1] "FBCOF1119-12"
    ## 
    ## [[17]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[18]]
    ## [[18]]$id
    ## [1] "FBCOH261-12"
    ## 
    ## [[18]]$name
    ## [1] "Platynus scrobiculatus"
    ## 
    ## [[18]]$gene
    ## [1] "FBCOH261-12"
    ## 
    ## [[18]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCATGATCAGGGATAGTAGGAACTTCATTAAGAATATTAATTCGATTAGAGTTAGGTAGTCCTGGGTCATTGATTGGAGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTATTATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCCCCTGATATAGCATTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCCCCATCTTTAACATTGCTTTTAATGAGCAGAATAGTAGAAAGAGGTGCTGGAACTGGATGAACAGTTTACCCTCCCCTATCATCTGGAATTGCCCATGCTGGAGCTTCAGTTGATTTAGCTATTTTTAGATTACATCTAGCTGGAATTTCATCTATTTTAGGAGCTGTAAATTTTATTACTACTATTATTAATATACGATCAGTGGGAATAACTTTTGATCGAATACCTTTATTTGTTTGATCAGTTGGAATTACTGCTTTATTATTACTTTTATCTTTACCTGTTTTAGCAGGGGCTATTACAATATTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCTGCTGGAGGAGGAGACCCAATTTTATATCA----------"
    ## 
    ## 
    ## [[19]]
    ## [[19]]$id
    ## [1] "FBCOH643-12"
    ## 
    ## [[19]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[19]]$gene
    ## [1] "FBCOH643-12"
    ## 
    ## [[19]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[20]]
    ## [[20]]$id
    ## [1] "FBCOI721-12"
    ## 
    ## [[20]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[20]]$gene
    ## [1] "FBCOI721-12"
    ## 
    ## [[20]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCCTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[21]]
    ## [[21]]$id
    ## [1] "FBCOK374-13"
    ## 
    ## [[21]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[21]]$gene
    ## [1] "FBCOK374-13"
    ## 
    ## [[21]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTNTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGNTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCA----------"
    ## 
    ## 
    ## [[22]]
    ## [[22]]$id
    ## [1] "GBCL24393-15"
    ## 
    ## [[22]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[22]]$gene
    ## [1] "GBCL24393-15"
    ## 
    ## [[22]]$sequence
    ## [1] "CTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTGACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGGGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTGGGAATAACCTTTGATCGAATACCGTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTGCTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGA"
    ## 
    ## 
    ## [[23]]
    ## [[23]]$id
    ## [1] "GBCL24394-15"
    ## 
    ## [[23]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[23]]$gene
    ## [1] "GBCL24394-15"
    ## 
    ## [[23]]$sequence
    ## [1] "CTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTGTTACCCCCTTCTTTGACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGGGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTGGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTGGGAATAACCTTTGATCGAATACCGTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTGCTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGA"
    ## 
    ## 
    ## [[24]]
    ## [[24]]$id
    ## [1] "GBCL31241-19"
    ## 
    ## [[24]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[24]]$gene
    ## [1] "GBCL31241-19"
    ## 
    ## [[24]]$sequence
    ## [1] "GGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTTTGA"
    ## 
    ## 
    ## [[25]]
    ## [[25]]$id
    ## [1] "GBCL31242-19"
    ## 
    ## [[25]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[25]]$gene
    ## [1] "GBCL31242-19"
    ## 
    ## [[25]]$sequence
    ## [1] "GGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTTTGA"
    ## 
    ## 
    ## [[26]]
    ## [[26]]$id
    ## [1] "GBCOE854-13"
    ## 
    ## [[26]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[26]]$gene
    ## [1] "GBCOE854-13"
    ## 
    ## [[26]]$sequence
    ## [1] "-------------------------------GGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[27]]
    ## [[27]]$id
    ## [1] "GBCOE873-13"
    ## 
    ## [[27]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[27]]$gene
    ## [1] "GBCOE873-13"
    ## 
    ## [[27]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[28]]
    ## [[28]]$id
    ## [1] "GBCOE897-13"
    ## 
    ## [[28]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[28]]$gene
    ## [1] "GBCOE897-13"
    ## 
    ## [[28]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[29]]
    ## [[29]]$id
    ## [1] "GBCOG078-13"
    ## 
    ## [[29]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[29]]$gene
    ## [1] "GBCOG078-13"
    ## 
    ## [[29]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[30]]
    ## [[30]]$id
    ## [1] "GBCOG135-13"
    ## 
    ## [[30]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[30]]$gene
    ## [1] "GBCOG135-13"
    ## 
    ## [[30]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[31]]
    ## [[31]]$id
    ## [1] "GBCOL648-12"
    ## 
    ## [[31]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[31]]$gene
    ## [1] "GBCOL648-12"
    ## 
    ## [[31]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[32]]
    ## [[32]]$id
    ## [1] "GBCOL649-12"
    ## 
    ## [[32]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[32]]$gene
    ## [1] "GBCOL649-12"
    ## 
    ## [[32]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[33]]
    ## [[33]]$id
    ## [1] "GBCOU2763-13"
    ## 
    ## [[33]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[33]]$gene
    ## [1] "GBCOU2763-13"
    ## 
    ## [[33]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGCTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTTCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCGGGAGGAGGTGATCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[34]]
    ## [[34]]$id
    ## [1] "GBCOU5574-14"
    ## 
    ## [[34]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[34]]$gene
    ## [1] "GBCOU5574-14"
    ## 
    ## [[34]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[35]]
    ## [[35]]$id
    ## [1] "GBCOU6598-14"
    ## 
    ## [[35]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[35]]$gene
    ## [1] "GBCOU6598-14"
    ## 
    ## [[35]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[36]]
    ## [[36]]$id
    ## [1] "GBCOU7781-14"
    ## 
    ## [[36]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[36]]$gene
    ## [1] "GBCOU7781-14"
    ## 
    ## [[36]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGTTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAACTGGCTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATGCGATCAGAAGGAATAACTTTTGATCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCTGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGACCCCGCGGGAGGAGGTGACCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[37]]
    ## [[37]]$id
    ## [1] "GBCOU7786-14"
    ## 
    ## [[37]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[37]]$gene
    ## [1] "GBCOU7786-14"
    ## 
    ## [[37]]$sequence
    ## [1] "AACACTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAACTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATTATAATTGGAGGTTTTGGTAATTGATTGATTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTGAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTGGGAATTACTGCTTTGTTATTACTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAACACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[38]]
    ## [[38]]$id
    ## [1] "GBMIN41066-14"
    ## 
    ## [[38]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[38]]$gene
    ## [1] "GBMIN41066-14"
    ## 
    ## [[38]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTGGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[39]]
    ## [[39]]$id
    ## [1] "GBMIN41068-14"
    ## 
    ## [[39]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[39]]$gene
    ## [1] "GBMIN41068-14"
    ## 
    ## [[39]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAATTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[40]]
    ## [[40]]$id
    ## [1] "GBMIN41071-14"
    ## 
    ## [[40]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[40]]$gene
    ## [1] "GBMIN41071-14"
    ## 
    ## [[40]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[41]]
    ## [[41]]$id
    ## [1] "GBMIN41285-14"
    ## 
    ## [[41]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[41]]$gene
    ## [1] "GBMIN41285-14"
    ## 
    ## [[41]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGATTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTACCAACATTTA"
    ## 
    ## 
    ## [[42]]
    ## [[42]]$id
    ## [1] "GBMIX2254-15"
    ## 
    ## [[42]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[42]]$gene
    ## [1] "GBMIX2254-15"
    ## 
    ## [[42]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[43]]
    ## [[43]]$id
    ## [1] "GCOL1156-16"
    ## 
    ## [[43]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[43]]$gene
    ## [1] "GCOL1156-16"
    ## 
    ## [[43]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[44]]
    ## [[44]]$id
    ## [1] "GCOL1785-16"
    ## 
    ## [[44]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[44]]$gene
    ## [1] "GCOL1785-16"
    ## 
    ## [[44]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[45]]
    ## [[45]]$id
    ## [1] "GCOL2184-16"
    ## 
    ## [[45]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[45]]$gene
    ## [1] "GCOL2184-16"
    ## 
    ## [[45]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[46]]
    ## [[46]]$id
    ## [1] "GCOL3294-16"
    ## 
    ## [[46]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[46]]$gene
    ## [1] "GCOL3294-16"
    ## 
    ## [[46]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[47]]
    ## [[47]]$id
    ## [1] "GCOL354-16"
    ## 
    ## [[47]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[47]]$gene
    ## [1] "GCOL354-16"
    ## 
    ## [[47]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[48]]
    ## [[48]]$id
    ## [1] "GCOL4195-16"
    ## 
    ## [[48]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[48]]$gene
    ## [1] "GCOL4195-16"
    ## 
    ## [[48]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[49]]
    ## [[49]]$id
    ## [1] "GCOL4448-16"
    ## 
    ## [[49]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[49]]$gene
    ## [1] "GCOL4448-16"
    ## 
    ## [[49]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[50]]
    ## [[50]]$id
    ## [1] "GCOL4727-16"
    ## 
    ## [[50]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[50]]$gene
    ## [1] "GCOL4727-16"
    ## 
    ## [[50]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[51]]
    ## [[51]]$id
    ## [1] "GCOL5208-16"
    ## 
    ## [[51]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[51]]$gene
    ## [1] "GCOL5208-16"
    ## 
    ## [[51]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[52]]
    ## [[52]]$id
    ## [1] "GCOL654-16"
    ## 
    ## [[52]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[52]]$gene
    ## [1] "GCOL654-16"
    ## 
    ## [[52]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[53]]
    ## [[53]]$id
    ## [1] "GCOL9638-16"
    ## 
    ## [[53]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[53]]$gene
    ## [1] "GCOL9638-16"
    ## 
    ## [[53]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[54]]
    ## [[54]]$id
    ## [1] "KROK004-19"
    ## 
    ## [[54]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[54]]$gene
    ## [1] "KROK004-19"
    ## 
    ## [[54]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[55]]
    ## [[55]]$id
    ## [1] "KROK005-19"
    ## 
    ## [[55]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[55]]$gene
    ## [1] "KROK005-19"
    ## 
    ## [[55]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGATCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCCATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[56]]
    ## [[56]]$id
    ## [1] "KROK008-19"
    ## 
    ## [[56]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[56]]$gene
    ## [1] "KROK008-19"
    ## 
    ## [[56]]$sequence
    ## [1] "AAGATATTGGAACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCCATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTAGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATA"
    ## 
    ## 
    ## [[57]]
    ## [[57]]$id
    ## [1] "KROK010-19"
    ## 
    ## [[57]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[57]]$gene
    ## [1] "KROK010-19"
    ## 
    ## [[57]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATAT"
    ## 
    ## 
    ## [[58]]
    ## [[58]]$id
    ## [1] "KROK011-19"
    ## 
    ## [[58]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[58]]$gene
    ## [1] "KROK011-19"
    ## 
    ## [[58]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCTTGATCAGGAATAGTGGGAACTTCTTTAAGAATACTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTAACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGAGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTAGGAATAACCTTTGATCGAATACCTTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTACTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTCTAACAGACCGTAATTTAAATACTTCTTTTTTCGATCCAGCTGGGGGAGGTGACCCAATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[59]]
    ## [[59]]$id
    ## [1] "KROK015-19"
    ## 
    ## [[59]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[59]]$gene
    ## [1] "KROK015-19"
    ## 
    ## [[59]]$sequence
    ## [1] "AACATTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGTTTTGGTAATTGATTGGTTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTAGGAATTACTGCTTTGTTATTGCTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[60]]
    ## [[60]]$id
    ## [1] "KROK018-19"
    ## 
    ## [[60]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[60]]$gene
    ## [1] "KROK018-19"
    ## 
    ## [[60]]$sequence
    ## [1] "AACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[61]]
    ## [[61]]$id
    ## [1] "KROK019-19"
    ## 
    ## [[61]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[61]]$gene
    ## [1] "KROK019-19"
    ## 
    ## [[61]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATACTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCAGGAGGAGGTGACCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[62]]
    ## [[62]]$id
    ## [1] "KROK022-19"
    ## 
    ## [[62]]$name
    ## [1] "Platynus scrobiculatus"
    ## 
    ## [[62]]$gene
    ## [1] "KROK022-19"
    ## 
    ## [[62]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCATGATCAGGGATAGTAGGAACTTCATTAAGAATATTAATTCGATTAGAGTTAGGTAGTCCTGGGTCATTGATTGGAGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTATTATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCCCCTGATATAGCATTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCCCCATCTTTAACATTGCTTTTAATGAGCAGAATAGTAGAAAGAGGTGCTGGAACTGGATGAACAGTTTACCCTCCCCTATCATCTGGAATTGCCCATGCTGGAGCTTCAGTTGATTTAGCTATTTTTAGATTACATCTAGCTGGAATTTCATCTATTTTAGGAGCTGTAAATTTTATTACTACTATTATTAATATACGATCAGTGGGAATAACTTTTGATCGAATACCTTTATTTGTTTGATCAGTTGGAATTACTGCTTTATTATTACTTTTATCTTTACCTGTTTTAGCAGGGGCTATTACAATATTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCCGCTGGAGGAGGAGACCCAATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[63]]
    ## [[63]]$id
    ## [1] "TDAAT1173-20"
    ## 
    ## [[63]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[63]]$gene
    ## [1] "TDAAT1173-20"
    ## 
    ## [[63]]$sequence
    ## [1] "AATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT-------------------------------------------------------------------------------"
    ## 
    ## 
    ## [[64]]
    ## [[64]]$id
    ## [1] "TDAOE288-21"
    ## 
    ## [[64]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[64]]$gene
    ## [1] "TDAOE288-21"
    ## 
    ## [[64]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[65]]
    ## [[65]]$id
    ## [1] "COLFF784-13"
    ## 
    ## [[65]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[65]]$gene
    ## [1] "COLFF784-13"
    ## 
    ## [[65]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[66]]
    ## [[66]]$id
    ## [1] "COLFH2111-16"
    ## 
    ## [[66]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[66]]$gene
    ## [1] "COLFH2111-16"
    ## 
    ## [[66]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[67]]
    ## [[67]]$id
    ## [1] "EUCAR1376-15"
    ## 
    ## [[67]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[67]]$gene
    ## [1] "EUCAR1376-15"
    ## 
    ## [[67]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGG"
    ## 
    ## 
    ## [[68]]
    ## [[68]]$id
    ## [1] "EUCAR1377-15"
    ## 
    ## [[68]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[68]]$gene
    ## [1] "EUCAR1377-15"
    ## 
    ## [[68]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTG"
    ## 
    ## 
    ## [[69]]
    ## [[69]]$id
    ## [1] "EUCAR1403-15"
    ## 
    ## [[69]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[69]]$gene
    ## [1] "EUCAR1403-15"
    ## 
    ## [[69]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[70]]
    ## [[70]]$id
    ## [1] "EUCAR1404-15"
    ## 
    ## [[70]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[70]]$gene
    ## [1] "EUCAR1404-15"
    ## 
    ## [[70]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[71]]
    ## [[71]]$id
    ## [1] "EUCAR1772-17"
    ## 
    ## [[71]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[71]]$gene
    ## [1] "EUCAR1772-17"
    ## 
    ## [[71]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[72]]
    ## [[72]]$id
    ## [1] "FBCOB095-10"
    ## 
    ## [[72]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[72]]$gene
    ## [1] "FBCOB095-10"
    ## 
    ## [[72]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[73]]
    ## [[73]]$id
    ## [1] "FBCOD1052-11"
    ## 
    ## [[73]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[73]]$gene
    ## [1] "FBCOD1052-11"
    ## 
    ## [[73]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[74]]
    ## [[74]]$id
    ## [1] "FBCOD1053-11"
    ## 
    ## [[74]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[74]]$gene
    ## [1] "FBCOD1053-11"
    ## 
    ## [[74]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[75]]
    ## [[75]]$id
    ## [1] "FBCOD1096-11"
    ## 
    ## [[75]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[75]]$gene
    ## [1] "FBCOD1096-11"
    ## 
    ## [[75]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGNATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[76]]
    ## [[76]]$id
    ## [1] "FBCOF1118-12"
    ## 
    ## [[76]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[76]]$gene
    ## [1] "FBCOF1118-12"
    ## 
    ## [[76]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[77]]
    ## [[77]]$id
    ## [1] "FBCOO765-13"
    ## 
    ## [[77]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[77]]$gene
    ## [1] "FBCOO765-13"
    ## 
    ## [[77]]$sequence
    ## [1] "-------------------------------------------------------------------------------AATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCNGTTGACTTGGCTATTTTTAGTTTGCATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[78]]
    ## [[78]]$id
    ## [1] "GBCL24386-15"
    ## 
    ## [[78]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[78]]$gene
    ## [1] "GBCL24386-15"
    ## 
    ## [[78]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAACCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATGGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAAGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGAATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[79]]
    ## [[79]]$id
    ## [1] "GBCL24387-15"
    ## 
    ## [[79]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[79]]$gene
    ## [1] "GBCL24387-15"
    ## 
    ## [[79]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[80]]
    ## [[80]]$id
    ## [1] "GBCL24388-15"
    ## 
    ## [[80]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[80]]$gene
    ## [1] "GBCL24388-15"
    ## 
    ## [[80]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[81]]
    ## [[81]]$id
    ## [1] "GBCOE103-13"
    ## 
    ## [[81]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[81]]$gene
    ## [1] "GBCOE103-13"
    ## 
    ## [[81]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[82]]
    ## [[82]]$id
    ## [1] "GBCOL593-12"
    ## 
    ## [[82]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[82]]$gene
    ## [1] "GBCOL593-12"
    ## 
    ## [[82]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[83]]
    ## [[83]]$id
    ## [1] "GBCOL658-12"
    ## 
    ## [[83]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[83]]$gene
    ## [1] "GBCOL658-12"
    ## 
    ## [[83]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGGGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[84]]
    ## [[84]]$id
    ## [1] "GBCOU1760-13"
    ## 
    ## [[84]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[84]]$gene
    ## [1] "GBCOU1760-13"
    ## 
    ## [[84]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[85]]
    ## [[85]]$id
    ## [1] "GBCOU2622-13"
    ## 
    ## [[85]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[85]]$gene
    ## [1] "GBCOU2622-13"
    ## 
    ## [[85]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTAACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTAGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAGCATCTGTTT"
    ## 
    ## 
    ## [[86]]
    ## [[86]]$id
    ## [1] "GBCOU2645-13"
    ## 
    ## [[86]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[86]]$gene
    ## [1] "GBCOU2645-13"
    ## 
    ## [[86]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[87]]
    ## [[87]]$id
    ## [1] "GBCOU3377-13"
    ## 
    ## [[87]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[87]]$gene
    ## [1] "GBCOU3377-13"
    ## 
    ## [[87]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[88]]
    ## [[88]]$id
    ## [1] "GBCOU5576-14"
    ## 
    ## [[88]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[88]]$gene
    ## [1] "GBCOU5576-14"
    ## 
    ## [[88]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAAATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTGGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATGCCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAG--------------------------------"
    ## 
    ## 
    ## [[89]]
    ## [[89]]$id
    ## [1] "GBCOU6597-14"
    ## 
    ## [[89]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[89]]$gene
    ## [1] "GBCOU6597-14"
    ## 
    ## [[89]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCA------------------------------------"
    ## 
    ## 
    ## [[90]]
    ## [[90]]$id
    ## [1] "GBCOU7780-14"
    ## 
    ## [[90]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[90]]$gene
    ## [1] "GBCOU7780-14"
    ## 
    ## [[90]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGCTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTTCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTATTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCGGGAGGAGGTGATCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[91]]
    ## [[91]]$id
    ## [1] "GBCOU7785-14"
    ## 
    ## [[91]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[91]]$gene
    ## [1] "GBCOU7785-14"
    ## 
    ## [[91]]$sequence
    ## [1] "AACACTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAACTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATCATAATTGGAGGTTTTGGTAATTGATTGATTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTGGGAATTACTGCTTTGTTATTACTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAACACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[92]]
    ## [[92]]$id
    ## [1] "GBCOU8633-14"
    ## 
    ## [[92]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[92]]$gene
    ## [1] "GBCOU8633-14"
    ## 
    ## [[92]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[93]]
    ## [[93]]$id
    ## [1] "GBMIN22488-13"
    ## 
    ## [[93]]$name
    ## [1] "Carabus catenulatus catenulatus"
    ## 
    ## [[93]]$gene
    ## [1] "GBMIN22488-13"
    ## 
    ## [[93]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGTTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAAGGGGGCAGGTACAGGATGAACAGTTTACCCCCCACTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCCTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATGCGATCAGAAGGAATAACTTTTGATCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCTGCGGGAGGAGGTGACCCAATTCTTTAC"
    ## 
    ## 
    ## [[94]]
    ## [[94]]$id
    ## [1] "GBMIN35988-13"
    ## 
    ## [[94]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[94]]$gene
    ## [1] "GBMIN35988-13"
    ## 
    ## [[94]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[95]]
    ## [[95]]$id
    ## [1] "GBMIN41067-14"
    ## 
    ## [[95]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[95]]$gene
    ## [1] "GBMIN41067-14"
    ## 
    ## [[95]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAATTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[96]]
    ## [[96]]$id
    ## [1] "GBMIN41069-14"
    ## 
    ## [[96]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[96]]$gene
    ## [1] "GBMIN41069-14"
    ## 
    ## [[96]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[97]]
    ## [[97]]$id
    ## [1] "GBMIN41070-14"
    ## 
    ## [[97]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[97]]$gene
    ## [1] "GBMIN41070-14"
    ## 
    ## [[97]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[98]]
    ## [[98]]$id
    ## [1] "GBMIN41283-14"
    ## 
    ## [[98]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[98]]$gene
    ## [1] "GBMIN41283-14"
    ## 
    ## [[98]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTA"
    ## 
    ## 
    ## [[99]]
    ## [[99]]$id
    ## [1] "GBMIN41284-14"
    ## 
    ## [[99]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[99]]$gene
    ## [1] "GBMIN41284-14"
    ## 
    ## [[99]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTGATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGATTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTACCAACATTTA"
    ## 
    ## 
    ## [[100]]
    ## [[100]]$id
    ## [1] "GBMIN41286-14"
    ## 
    ## [[100]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[100]]$gene
    ## [1] "GBMIN41286-14"
    ## 
    ## [[100]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTA"
    ## 
    ## 
    ## [[101]]
    ## [[101]]$id
    ## [1] "GBMIX1115-14"
    ## 
    ## [[101]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[101]]$gene
    ## [1] "GBMIX1115-14"
    ## 
    ## [[101]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[102]]
    ## [[102]]$id
    ## [1] "GBMIX1140-14"
    ## 
    ## [[102]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[102]]$gene
    ## [1] "GBMIX1140-14"
    ## 
    ## [[102]]$sequence
    ## [1] "-----------------------------CAGGAATAGTGGGAACTTCTTTAAGAATACTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGGGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTAACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGAGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTAGGAATAACCTTTGATCGAATACCTTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTACTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGATCCAGCTGGGGGAGGTGACCCAATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[103]]
    ## [[103]]$id
    ## [1] "GCOL1620-16"
    ## 
    ## [[103]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[103]]$gene
    ## [1] "GCOL1620-16"
    ## 
    ## [[103]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAATACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[104]]
    ## [[104]]$id
    ## [1] "GCOL1650-16"
    ## 
    ## [[104]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[104]]$gene
    ## [1] "GCOL1650-16"
    ## 
    ## [[104]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[105]]
    ## [[105]]$id
    ## [1] "GCOL1841-16"
    ## 
    ## [[105]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[105]]$gene
    ## [1] "GCOL1841-16"
    ## 
    ## [[105]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[106]]
    ## [[106]]$id
    ## [1] "GCOL1988-16"
    ## 
    ## [[106]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[106]]$gene
    ## [1] "GCOL1988-16"
    ## 
    ## [[106]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[107]]
    ## [[107]]$id
    ## [1] "GCOL2384-16"
    ## 
    ## [[107]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[107]]$gene
    ## [1] "GCOL2384-16"
    ## 
    ## [[107]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[108]]
    ## [[108]]$id
    ## [1] "GCOL2385-16"
    ## 
    ## [[108]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[108]]$gene
    ## [1] "GCOL2385-16"
    ## 
    ## [[108]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[109]]
    ## [[109]]$id
    ## [1] "GCOL260-16"
    ## 
    ## [[109]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[109]]$gene
    ## [1] "GCOL260-16"
    ## 
    ## [[109]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[110]]
    ## [[110]]$id
    ## [1] "GCOL3295-16"
    ## 
    ## [[110]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[110]]$gene
    ## [1] "GCOL3295-16"
    ## 
    ## [[110]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[111]]
    ## [[111]]$id
    ## [1] "GCOL4103-16"
    ## 
    ## [[111]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[111]]$gene
    ## [1] "GCOL4103-16"
    ## 
    ## [[111]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[112]]
    ## [[112]]$id
    ## [1] "GCOL4444-16"
    ## 
    ## [[112]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[112]]$gene
    ## [1] "GCOL4444-16"
    ## 
    ## [[112]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[113]]
    ## [[113]]$id
    ## [1] "GCOL4447-16"
    ## 
    ## [[113]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[113]]$gene
    ## [1] "GCOL4447-16"
    ## 
    ## [[113]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[114]]
    ## [[114]]$id
    ## [1] "GCOL4460-16"
    ## 
    ## [[114]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[114]]$gene
    ## [1] "GCOL4460-16"
    ## 
    ## [[114]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAATATAGTTGAAAACGGATCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[115]]
    ## [[115]]$id
    ## [1] "GCOL696-16"
    ## 
    ## [[115]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[115]]$gene
    ## [1] "GCOL696-16"
    ## 
    ## [[115]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[116]]
    ## [[116]]$id
    ## [1] "GCOL697-16"
    ## 
    ## [[116]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[116]]$gene
    ## [1] "GCOL697-16"
    ## 
    ## [[116]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[117]]
    ## [[117]]$id
    ## [1] "GCOL698-16"
    ## 
    ## [[117]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[117]]$gene
    ## [1] "GCOL698-16"
    ## 
    ## [[117]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[118]]
    ## [[118]]$id
    ## [1] "GCOL701-16"
    ## 
    ## [[118]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[118]]$gene
    ## [1] "GCOL701-16"
    ## 
    ## [[118]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[119]]
    ## [[119]]$id
    ## [1] "GCOL720-16"
    ## 
    ## [[119]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[119]]$gene
    ## [1] "GCOL720-16"
    ## 
    ## [[119]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCCATTCTAGGGGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[120]]
    ## [[120]]$id
    ## [1] "GCOL729-16"
    ## 
    ## [[120]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[120]]$gene
    ## [1] "GCOL729-16"
    ## 
    ## [[120]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[121]]
    ## [[121]]$id
    ## [1] "GCOL750-16"
    ## 
    ## [[121]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[121]]$gene
    ## [1] "GCOL750-16"
    ## 
    ## [[121]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[122]]
    ## [[122]]$id
    ## [1] "GCOL8531-16"
    ## 
    ## [[122]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[122]]$gene
    ## [1] "GCOL8531-16"
    ## 
    ## [[122]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[123]]
    ## [[123]]$id
    ## [1] "GCOL9622-16"
    ## 
    ## [[123]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[123]]$gene
    ## [1] "GCOL9622-16"
    ## 
    ## [[123]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[124]]
    ## [[124]]$id
    ## [1] "GENHP512-11"
    ## 
    ## [[124]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[124]]$gene
    ## [1] "GENHP512-11"
    ## 
    ## [[124]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[125]]
    ## [[125]]$id
    ## [1] "KROK012-19"
    ## 
    ## [[125]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[125]]$gene
    ## [1] "KROK012-19"
    ## 
    ## [[125]]$sequence
    ## [1] "GATATTGGAACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTTTGATTTTTG"
    ## 
    ## 
    ## [[126]]
    ## [[126]]$id
    ## [1] "KROK017-19"
    ## 
    ## [[126]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[126]]$gene
    ## [1] "KROK017-19"
    ## 
    ## [[126]]$sequence
    ## [1] "AAGATATTGGAACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTTTGATTTTTTGT"
    ## 
    ## 
    ## [[127]]
    ## [[127]]$id
    ## [1] "TDAAT1157-20"
    ## 
    ## [[127]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[127]]$gene
    ## [1] "TDAAT1157-20"
    ## 
    ## [[127]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[128]]
    ## [[128]]$id
    ## [1] "TDAAT1195-20"
    ## 
    ## [[128]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[128]]$gene
    ## [1] "TDAAT1195-20"
    ## 
    ## [[128]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[129]]
    ## [[129]]$id
    ## [1] "GBCOE855-13"
    ## 
    ## [[129]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[129]]$gene
    ## [1] "GBCOE855-13"
    ## 
    ## [[129]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[130]]
    ## [[130]]$id
    ## [1] "GBCOU5027-14"
    ## 
    ## [[130]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[130]]$gene
    ## [1] "GBCOU5027-14"
    ## 
    ## [[130]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAA---------"
    ## 
    ## 
    ## [[131]]
    ## [[131]]$id
    ## [1] "GBCOU5575-14"
    ## 
    ## [[131]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[131]]$gene
    ## [1] "GBCOU5575-14"
    ## 
    ## [[131]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"

``` r
check2<- bold_seq(taxon = NULL, ids = NULL, bin = slicey$bin_uri, container = NULL, institutions = NULL, researchers = NULL, geo = NULL, marker = NULL, response = FALSE)
```

``` r
check2
```

    ## [[1]]
    ## [[1]]$id
    ## [1] "COLFE328-12"
    ## 
    ## [[1]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[1]]$gene
    ## [1] "COLFE328-12"
    ## 
    ## [[1]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[2]]
    ## [[2]]$id
    ## [1] "EUCAR1265-15"
    ## 
    ## [[2]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[2]]$gene
    ## [1] "EUCAR1265-15"
    ## 
    ## [[2]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGA"
    ## 
    ## 
    ## [[3]]
    ## [[3]]$id
    ## [1] "EUCAR1269-15"
    ## 
    ## [[3]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[3]]$gene
    ## [1] "EUCAR1269-15"
    ## 
    ## [[3]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[4]]
    ## [[4]]$id
    ## [1] "EUCAR1375-15"
    ## 
    ## [[4]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[4]]$gene
    ## [1] "EUCAR1375-15"
    ## 
    ## [[4]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[5]]
    ## [[5]]$id
    ## [1] "EUCAR1378-15"
    ## 
    ## [[5]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[5]]$gene
    ## [1] "EUCAR1378-15"
    ## 
    ## [[5]]$sequence
    ## [1] "GCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTTTG"
    ## 
    ## 
    ## [[6]]
    ## [[6]]$id
    ## [1] "EUCAR1401-15"
    ## 
    ## [[6]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[6]]$gene
    ## [1] "EUCAR1401-15"
    ## 
    ## [[6]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[7]]
    ## [[7]]$id
    ## [1] "EUCAR1402-15"
    ## 
    ## [[7]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[7]]$gene
    ## [1] "EUCAR1402-15"
    ## 
    ## [[7]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[8]]
    ## [[8]]$id
    ## [1] "EUCAR1599-16"
    ## 
    ## [[8]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[8]]$gene
    ## [1] "EUCAR1599-16"
    ## 
    ## [[8]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[9]]
    ## [[9]]$id
    ## [1] "EUCAR1758-17"
    ## 
    ## [[9]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[9]]$gene
    ## [1] "EUCAR1758-17"
    ## 
    ## [[9]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[10]]
    ## [[10]]$id
    ## [1] "EUCAR1759-17"
    ## 
    ## [[10]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[10]]$gene
    ## [1] "EUCAR1759-17"
    ## 
    ## [[10]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[11]]
    ## [[11]]$id
    ## [1] "EUCAR1760-17"
    ## 
    ## [[11]]$name
    ## [1] "Notiophilus quadripunctatus"
    ## 
    ## [[11]]$gene
    ## [1] "EUCAR1760-17"
    ## 
    ## [[11]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGAGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGGGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[12]]
    ## [[12]]$id
    ## [1] "EUCAR1771-17"
    ## 
    ## [[12]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[12]]$gene
    ## [1] "EUCAR1771-17"
    ## 
    ## [[12]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[13]]
    ## [[13]]$id
    ## [1] "FBCOA331-10"
    ## 
    ## [[13]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[13]]$gene
    ## [1] "FBCOA331-10"
    ## 
    ## [[13]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[14]]
    ## [[14]]$id
    ## [1] "FBCOA591-10"
    ## 
    ## [[14]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[14]]$gene
    ## [1] "FBCOA591-10"
    ## 
    ## [[14]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATCCGGGCTGAATTAGGTAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCGGTTGACTTGGCTATTTTTAGTTTGCATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[15]]
    ## [[15]]$id
    ## [1] "FBCOD003-11"
    ## 
    ## [[15]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[15]]$gene
    ## [1] "FBCOD003-11"
    ## 
    ## [[15]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[16]]
    ## [[16]]$id
    ## [1] "FBCOD036-11"
    ## 
    ## [[16]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[16]]$gene
    ## [1] "FBCOD036-11"
    ## 
    ## [[16]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[17]]
    ## [[17]]$id
    ## [1] "FBCOF1119-12"
    ## 
    ## [[17]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[17]]$gene
    ## [1] "FBCOF1119-12"
    ## 
    ## [[17]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[18]]
    ## [[18]]$id
    ## [1] "FBCOH261-12"
    ## 
    ## [[18]]$name
    ## [1] "Platynus scrobiculatus"
    ## 
    ## [[18]]$gene
    ## [1] "FBCOH261-12"
    ## 
    ## [[18]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCATGATCAGGGATAGTAGGAACTTCATTAAGAATATTAATTCGATTAGAGTTAGGTAGTCCTGGGTCATTGATTGGAGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTATTATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCCCCTGATATAGCATTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCCCCATCTTTAACATTGCTTTTAATGAGCAGAATAGTAGAAAGAGGTGCTGGAACTGGATGAACAGTTTACCCTCCCCTATCATCTGGAATTGCCCATGCTGGAGCTTCAGTTGATTTAGCTATTTTTAGATTACATCTAGCTGGAATTTCATCTATTTTAGGAGCTGTAAATTTTATTACTACTATTATTAATATACGATCAGTGGGAATAACTTTTGATCGAATACCTTTATTTGTTTGATCAGTTGGAATTACTGCTTTATTATTACTTTTATCTTTACCTGTTTTAGCAGGGGCTATTACAATATTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCTGCTGGAGGAGGAGACCCAATTTTATATCA----------"
    ## 
    ## 
    ## [[19]]
    ## [[19]]$id
    ## [1] "FBCOH643-12"
    ## 
    ## [[19]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[19]]$gene
    ## [1] "FBCOH643-12"
    ## 
    ## [[19]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[20]]
    ## [[20]]$id
    ## [1] "FBCOI721-12"
    ## 
    ## [[20]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[20]]$gene
    ## [1] "FBCOI721-12"
    ## 
    ## [[20]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCCTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[21]]
    ## [[21]]$id
    ## [1] "FBCOK374-13"
    ## 
    ## [[21]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[21]]$gene
    ## [1] "FBCOK374-13"
    ## 
    ## [[21]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTNTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGNTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCA----------"
    ## 
    ## 
    ## [[22]]
    ## [[22]]$id
    ## [1] "GBCL24393-15"
    ## 
    ## [[22]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[22]]$gene
    ## [1] "GBCL24393-15"
    ## 
    ## [[22]]$sequence
    ## [1] "CTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTGACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGGGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTGGGAATAACCTTTGATCGAATACCGTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTGCTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGA"
    ## 
    ## 
    ## [[23]]
    ## [[23]]$id
    ## [1] "GBCL24394-15"
    ## 
    ## [[23]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[23]]$gene
    ## [1] "GBCL24394-15"
    ## 
    ## [[23]]$sequence
    ## [1] "CTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTGTTACCCCCTTCTTTGACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGGGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTGGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTGGGAATAACCTTTGATCGAATACCGTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTGCTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGA"
    ## 
    ## 
    ## [[24]]
    ## [[24]]$id
    ## [1] "GBCL31241-19"
    ## 
    ## [[24]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[24]]$gene
    ## [1] "GBCL31241-19"
    ## 
    ## [[24]]$sequence
    ## [1] "GGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTTTGA"
    ## 
    ## 
    ## [[25]]
    ## [[25]]$id
    ## [1] "GBCL31242-19"
    ## 
    ## [[25]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[25]]$gene
    ## [1] "GBCL31242-19"
    ## 
    ## [[25]]$sequence
    ## [1] "GGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTTTGA"
    ## 
    ## 
    ## [[26]]
    ## [[26]]$id
    ## [1] "GBCOE854-13"
    ## 
    ## [[26]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[26]]$gene
    ## [1] "GBCOE854-13"
    ## 
    ## [[26]]$sequence
    ## [1] "-------------------------------GGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[27]]
    ## [[27]]$id
    ## [1] "GBCOE873-13"
    ## 
    ## [[27]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[27]]$gene
    ## [1] "GBCOE873-13"
    ## 
    ## [[27]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[28]]
    ## [[28]]$id
    ## [1] "GBCOE897-13"
    ## 
    ## [[28]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[28]]$gene
    ## [1] "GBCOE897-13"
    ## 
    ## [[28]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[29]]
    ## [[29]]$id
    ## [1] "GBCOG078-13"
    ## 
    ## [[29]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[29]]$gene
    ## [1] "GBCOG078-13"
    ## 
    ## [[29]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[30]]
    ## [[30]]$id
    ## [1] "GBCOG135-13"
    ## 
    ## [[30]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[30]]$gene
    ## [1] "GBCOG135-13"
    ## 
    ## [[30]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[31]]
    ## [[31]]$id
    ## [1] "GBCOL648-12"
    ## 
    ## [[31]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[31]]$gene
    ## [1] "GBCOL648-12"
    ## 
    ## [[31]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[32]]
    ## [[32]]$id
    ## [1] "GBCOL649-12"
    ## 
    ## [[32]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[32]]$gene
    ## [1] "GBCOL649-12"
    ## 
    ## [[32]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[33]]
    ## [[33]]$id
    ## [1] "GBCOU2763-13"
    ## 
    ## [[33]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[33]]$gene
    ## [1] "GBCOU2763-13"
    ## 
    ## [[33]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGCTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTTCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCGGGAGGAGGTGATCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[34]]
    ## [[34]]$id
    ## [1] "GBCOU5574-14"
    ## 
    ## [[34]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[34]]$gene
    ## [1] "GBCOU5574-14"
    ## 
    ## [[34]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[35]]
    ## [[35]]$id
    ## [1] "GBCOU6598-14"
    ## 
    ## [[35]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[35]]$gene
    ## [1] "GBCOU6598-14"
    ## 
    ## [[35]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[36]]
    ## [[36]]$id
    ## [1] "GBCOU7781-14"
    ## 
    ## [[36]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[36]]$gene
    ## [1] "GBCOU7781-14"
    ## 
    ## [[36]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGTTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAACTGGCTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATGCGATCAGAAGGAATAACTTTTGATCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCTGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGACCCCGCGGGAGGAGGTGACCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[37]]
    ## [[37]]$id
    ## [1] "GBCOU7786-14"
    ## 
    ## [[37]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[37]]$gene
    ## [1] "GBCOU7786-14"
    ## 
    ## [[37]]$sequence
    ## [1] "AACACTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAACTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATTATAATTGGAGGTTTTGGTAATTGATTGATTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTGAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTGGGAATTACTGCTTTGTTATTACTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAACACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[38]]
    ## [[38]]$id
    ## [1] "GBMIN41066-14"
    ## 
    ## [[38]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[38]]$gene
    ## [1] "GBMIN41066-14"
    ## 
    ## [[38]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTGGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[39]]
    ## [[39]]$id
    ## [1] "GBMIN41068-14"
    ## 
    ## [[39]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[39]]$gene
    ## [1] "GBMIN41068-14"
    ## 
    ## [[39]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAATTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[40]]
    ## [[40]]$id
    ## [1] "GBMIN41071-14"
    ## 
    ## [[40]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[40]]$gene
    ## [1] "GBMIN41071-14"
    ## 
    ## [[40]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[41]]
    ## [[41]]$id
    ## [1] "GBMIN41285-14"
    ## 
    ## [[41]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[41]]$gene
    ## [1] "GBMIN41285-14"
    ## 
    ## [[41]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGATTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTACCAACATTTA"
    ## 
    ## 
    ## [[42]]
    ## [[42]]$id
    ## [1] "GBMIX2254-15"
    ## 
    ## [[42]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[42]]$gene
    ## [1] "GBMIX2254-15"
    ## 
    ## [[42]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[43]]
    ## [[43]]$id
    ## [1] "GCOL1156-16"
    ## 
    ## [[43]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[43]]$gene
    ## [1] "GCOL1156-16"
    ## 
    ## [[43]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[44]]
    ## [[44]]$id
    ## [1] "GCOL1785-16"
    ## 
    ## [[44]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[44]]$gene
    ## [1] "GCOL1785-16"
    ## 
    ## [[44]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[45]]
    ## [[45]]$id
    ## [1] "GCOL2184-16"
    ## 
    ## [[45]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[45]]$gene
    ## [1] "GCOL2184-16"
    ## 
    ## [[45]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[46]]
    ## [[46]]$id
    ## [1] "GCOL3294-16"
    ## 
    ## [[46]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[46]]$gene
    ## [1] "GCOL3294-16"
    ## 
    ## [[46]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[47]]
    ## [[47]]$id
    ## [1] "GCOL354-16"
    ## 
    ## [[47]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[47]]$gene
    ## [1] "GCOL354-16"
    ## 
    ## [[47]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[48]]
    ## [[48]]$id
    ## [1] "GCOL4195-16"
    ## 
    ## [[48]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[48]]$gene
    ## [1] "GCOL4195-16"
    ## 
    ## [[48]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[49]]
    ## [[49]]$id
    ## [1] "GCOL4448-16"
    ## 
    ## [[49]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[49]]$gene
    ## [1] "GCOL4448-16"
    ## 
    ## [[49]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[50]]
    ## [[50]]$id
    ## [1] "GCOL4727-16"
    ## 
    ## [[50]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[50]]$gene
    ## [1] "GCOL4727-16"
    ## 
    ## [[50]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[51]]
    ## [[51]]$id
    ## [1] "GCOL5208-16"
    ## 
    ## [[51]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[51]]$gene
    ## [1] "GCOL5208-16"
    ## 
    ## [[51]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[52]]
    ## [[52]]$id
    ## [1] "GCOL654-16"
    ## 
    ## [[52]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[52]]$gene
    ## [1] "GCOL654-16"
    ## 
    ## [[52]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[53]]
    ## [[53]]$id
    ## [1] "GCOL9638-16"
    ## 
    ## [[53]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[53]]$gene
    ## [1] "GCOL9638-16"
    ## 
    ## [[53]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[54]]
    ## [[54]]$id
    ## [1] "KROK004-19"
    ## 
    ## [[54]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[54]]$gene
    ## [1] "KROK004-19"
    ## 
    ## [[54]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[55]]
    ## [[55]]$id
    ## [1] "KROK005-19"
    ## 
    ## [[55]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[55]]$gene
    ## [1] "KROK005-19"
    ## 
    ## [[55]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGATCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCCATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[56]]
    ## [[56]]$id
    ## [1] "KROK008-19"
    ## 
    ## [[56]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[56]]$gene
    ## [1] "KROK008-19"
    ## 
    ## [[56]]$sequence
    ## [1] "AAGATATTGGAACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCCATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTAGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATA"
    ## 
    ## 
    ## [[57]]
    ## [[57]]$id
    ## [1] "KROK010-19"
    ## 
    ## [[57]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[57]]$gene
    ## [1] "KROK010-19"
    ## 
    ## [[57]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATAT"
    ## 
    ## 
    ## [[58]]
    ## [[58]]$id
    ## [1] "KROK011-19"
    ## 
    ## [[58]]$name
    ## [1] "Carabus creutzeri"
    ## 
    ## [[58]]$gene
    ## [1] "KROK011-19"
    ## 
    ## [[58]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCTTGATCAGGAATAGTGGGAACTTCTTTAAGAATACTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTAACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGAGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTAGGAATAACCTTTGATCGAATACCTTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTACTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTCTAACAGACCGTAATTTAAATACTTCTTTTTTCGATCCAGCTGGGGGAGGTGACCCAATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[59]]
    ## [[59]]$id
    ## [1] "KROK015-19"
    ## 
    ## [[59]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[59]]$gene
    ## [1] "KROK015-19"
    ## 
    ## [[59]]$sequence
    ## [1] "AACATTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGTTTTGGTAATTGATTGGTTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTAGGAATTACTGCTTTGTTATTGCTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[60]]
    ## [[60]]$id
    ## [1] "KROK018-19"
    ## 
    ## [[60]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[60]]$gene
    ## [1] "KROK018-19"
    ## 
    ## [[60]]$sequence
    ## [1] "AACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[61]]
    ## [[61]]$id
    ## [1] "KROK019-19"
    ## 
    ## [[61]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[61]]$gene
    ## [1] "KROK019-19"
    ## 
    ## [[61]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATACTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCAGGAGGAGGTGACCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[62]]
    ## [[62]]$id
    ## [1] "KROK022-19"
    ## 
    ## [[62]]$name
    ## [1] "Platynus scrobiculatus"
    ## 
    ## [[62]]$gene
    ## [1] "KROK022-19"
    ## 
    ## [[62]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCATGATCAGGGATAGTAGGAACTTCATTAAGAATATTAATTCGATTAGAGTTAGGTAGTCCTGGGTCATTGATTGGAGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTATTATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCCCCTGATATAGCATTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCCCCATCTTTAACATTGCTTTTAATGAGCAGAATAGTAGAAAGAGGTGCTGGAACTGGATGAACAGTTTACCCTCCCCTATCATCTGGAATTGCCCATGCTGGAGCTTCAGTTGATTTAGCTATTTTTAGATTACATCTAGCTGGAATTTCATCTATTTTAGGAGCTGTAAATTTTATTACTACTATTATTAATATACGATCAGTGGGAATAACTTTTGATCGAATACCTTTATTTGTTTGATCAGTTGGAATTACTGCTTTATTATTACTTTTATCTTTACCTGTTTTAGCAGGGGCTATTACAATATTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGACCCCGCTGGAGGAGGAGACCCAATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[63]]
    ## [[63]]$id
    ## [1] "TDAAT1173-20"
    ## 
    ## [[63]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[63]]$gene
    ## [1] "TDAAT1173-20"
    ## 
    ## [[63]]$sequence
    ## [1] "AATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT-------------------------------------------------------------------------------"
    ## 
    ## 
    ## [[64]]
    ## [[64]]$id
    ## [1] "TDAOE288-21"
    ## 
    ## [[64]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[64]]$gene
    ## [1] "TDAOE288-21"
    ## 
    ## [[64]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[65]]
    ## [[65]]$id
    ## [1] "COLFF784-13"
    ## 
    ## [[65]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[65]]$gene
    ## [1] "COLFF784-13"
    ## 
    ## [[65]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[66]]
    ## [[66]]$id
    ## [1] "COLFH2111-16"
    ## 
    ## [[66]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[66]]$gene
    ## [1] "COLFH2111-16"
    ## 
    ## [[66]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATCGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[67]]
    ## [[67]]$id
    ## [1] "EUCAR1376-15"
    ## 
    ## [[67]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[67]]$gene
    ## [1] "EUCAR1376-15"
    ## 
    ## [[67]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGG"
    ## 
    ## 
    ## [[68]]
    ## [[68]]$id
    ## [1] "EUCAR1377-15"
    ## 
    ## [[68]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[68]]$gene
    ## [1] "EUCAR1377-15"
    ## 
    ## [[68]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTG"
    ## 
    ## 
    ## [[69]]
    ## [[69]]$id
    ## [1] "EUCAR1403-15"
    ## 
    ## [[69]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[69]]$gene
    ## [1] "EUCAR1403-15"
    ## 
    ## [[69]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[70]]
    ## [[70]]$id
    ## [1] "EUCAR1404-15"
    ## 
    ## [[70]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[70]]$gene
    ## [1] "EUCAR1404-15"
    ## 
    ## [[70]]$sequence
    ## [1] "ACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTA"
    ## 
    ## 
    ## [[71]]
    ## [[71]]$id
    ## [1] "EUCAR1772-17"
    ## 
    ## [[71]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[71]]$gene
    ## [1] "EUCAR1772-17"
    ## 
    ## [[71]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[72]]
    ## [[72]]$id
    ## [1] "FBCOB095-10"
    ## 
    ## [[72]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[72]]$gene
    ## [1] "FBCOB095-10"
    ## 
    ## [[72]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[73]]
    ## [[73]]$id
    ## [1] "FBCOD1052-11"
    ## 
    ## [[73]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[73]]$gene
    ## [1] "FBCOD1052-11"
    ## 
    ## [[73]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[74]]
    ## [[74]]$id
    ## [1] "FBCOD1053-11"
    ## 
    ## [[74]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[74]]$gene
    ## [1] "FBCOD1053-11"
    ## 
    ## [[74]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[75]]
    ## [[75]]$id
    ## [1] "FBCOD1096-11"
    ## 
    ## [[75]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[75]]$gene
    ## [1] "FBCOD1096-11"
    ## 
    ## [[75]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGNATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[76]]
    ## [[76]]$id
    ## [1] "FBCOF1118-12"
    ## 
    ## [[76]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[76]]$gene
    ## [1] "FBCOF1118-12"
    ## 
    ## [[76]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[77]]
    ## [[77]]$id
    ## [1] "FBCOO765-13"
    ## 
    ## [[77]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[77]]$gene
    ## [1] "FBCOO765-13"
    ## 
    ## [[77]]$sequence
    ## [1] "-------------------------------------------------------------------------------AATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCNGTTGACTTGGCTATTTTTAGTTTGCATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[78]]
    ## [[78]]$id
    ## [1] "GBCL24386-15"
    ## 
    ## [[78]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[78]]$gene
    ## [1] "GBCL24386-15"
    ## 
    ## [[78]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAACCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATGGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAAGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGAATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[79]]
    ## [[79]]$id
    ## [1] "GBCL24387-15"
    ## 
    ## [[79]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[79]]$gene
    ## [1] "GBCL24387-15"
    ## 
    ## [[79]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCCCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[80]]
    ## [[80]]$id
    ## [1] "GBCL24388-15"
    ## 
    ## [[80]]$name
    ## [1] "Carabus catenulatus"
    ## 
    ## [[80]]$gene
    ## [1] "GBCL24388-15"
    ## 
    ## [[80]]$sequence
    ## [1] "CTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGA"
    ## 
    ## 
    ## [[81]]
    ## [[81]]$id
    ## [1] "GBCOE103-13"
    ## 
    ## [[81]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[81]]$gene
    ## [1] "GBCOE103-13"
    ## 
    ## [[81]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[82]]
    ## [[82]]$id
    ## [1] "GBCOL593-12"
    ## 
    ## [[82]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[82]]$gene
    ## [1] "GBCOL593-12"
    ## 
    ## [[82]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[83]]
    ## [[83]]$id
    ## [1] "GBCOL658-12"
    ## 
    ## [[83]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[83]]$gene
    ## [1] "GBCOL658-12"
    ## 
    ## [[83]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGGGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[84]]
    ## [[84]]$id
    ## [1] "GBCOU1760-13"
    ## 
    ## [[84]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[84]]$gene
    ## [1] "GBCOU1760-13"
    ## 
    ## [[84]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[85]]
    ## [[85]]$id
    ## [1] "GBCOU2622-13"
    ## 
    ## [[85]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[85]]$gene
    ## [1] "GBCOU2622-13"
    ## 
    ## [[85]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTAACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTAGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAGCATCTGTTT"
    ## 
    ## 
    ## [[86]]
    ## [[86]]$id
    ## [1] "GBCOU2645-13"
    ## 
    ## [[86]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[86]]$gene
    ## [1] "GBCOU2645-13"
    ## 
    ## [[86]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[87]]
    ## [[87]]$id
    ## [1] "GBCOU3377-13"
    ## 
    ## [[87]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[87]]$gene
    ## [1] "GBCOU3377-13"
    ## 
    ## [[87]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[88]]
    ## [[88]]$id
    ## [1] "GBCOU5576-14"
    ## 
    ## [[88]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[88]]$gene
    ## [1] "GBCOU5576-14"
    ## 
    ## [[88]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAAATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTGGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATGCCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAG--------------------------------"
    ## 
    ## 
    ## [[89]]
    ## [[89]]$id
    ## [1] "GBCOU6597-14"
    ## 
    ## [[89]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[89]]$gene
    ## [1] "GBCOU6597-14"
    ## 
    ## [[89]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCA------------------------------------"
    ## 
    ## 
    ## [[90]]
    ## [[90]]$id
    ## [1] "GBCOU7780-14"
    ## 
    ## [[90]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[90]]$gene
    ## [1] "GBCOU7780-14"
    ## 
    ## [[90]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGCTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTTCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAGGGGGGCAGGTACAGGATGAACAGTTTACCCTCCGCTGTCTTCTGGAATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCTTCTATTCTAGGGGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGAAGGAATAACTTTTGACCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCATTATTATTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCCGCGGGAGGAGGTGATCCAATTCTTTACCAACACTTATTT"
    ## 
    ## 
    ## [[91]]
    ## [[91]]$id
    ## [1] "GBCOU7785-14"
    ## 
    ## [[91]]$name
    ## [1] "Molops striolatus"
    ## 
    ## [[91]]$gene
    ## [1] "GBCOU7785-14"
    ## 
    ## [[91]]$sequence
    ## [1] "AACACTATATTTCATTCTTGGGGCATGGTCAGGAATAGTAGGAACCTCCTTAAGAATATTAATTCGAACTGAATTAGGAAATCCGGGGTCCTTGATTGGAGATGACCAGATCTATAATGTAATTGTAACTGCACATGCTTTTGTTATAATTTTTTTTATAGTAATGCCTATCATAATTGGAGGTTTTGGTAATTGATTGATTCCTTTAATATTAGGAGCTCCTGATATAGCCTTTCCTCGGATAAATAATATGAGTTTTTGACTTCTTCCTCCATCTTTAACCCTTTTACTAGTGAGTAGCATAGTGGAAAAGGGAGTTGGTACAGGATGAACTGTATACCCTCCTCTCTCATCGACAATTGCTCATAGAGGAGCATCTGTAGATTTAGCTATTTTTAGCCTACATCTAGCAGGAATTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTGGGAATAACATTTGATCGTATACCTTTATTTGTATGATCAGTGGGAATTACTGCTTTGTTATTACTTTTATCCCTCCCAGTATTAGCAGGAGCTATTACAATGTTATTAACAGATCGAAATTTAAACACTTCTTTTTTTGACCCCGCAGGAGGAGGAGACCCTATTTTATACCAACATTTATTT"
    ## 
    ## 
    ## [[92]]
    ## [[92]]$id
    ## [1] "GBCOU8633-14"
    ## 
    ## [[92]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[92]]$gene
    ## [1] "GBCOU8633-14"
    ## 
    ## [[92]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[93]]
    ## [[93]]$id
    ## [1] "GBMIN22488-13"
    ## 
    ## [[93]]$name
    ## [1] "Carabus catenulatus catenulatus"
    ## 
    ## [[93]]$gene
    ## [1] "GBMIN22488-13"
    ## 
    ## [[93]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTGCCTGATCAGGAATAGTGGGAACTTCATTAAGAATGTTAATTCGAGCCGAATTAGGTAATCCCGGATCCTTAATTGGAGATGATCAAATTTATAACGTTATTGTTACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGGGGATTTGGAAACTGACTAGTCCCATTAATACTAGGAGCCCCAGATATAGCCTTTCCTCGAATAAATAATATAAGTTTTTGATTATTGCCTCCTTCTCTGACTCTTCTCCTAATAAGAAGAATAGTGGAAAAGGGGGCAGGTACAGGATGAACAGTTTACCCCCCACTGTCTTCTGGTATTGCCCATAGAGGGGCATCCGTAGATTTAGCAATTTTTAGACTACATTTGGCTGGGATCTCCTCTATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATGCGATCAGAAGGAATAACTTTTGATCGAATACCCCTATTTGTTTGATCCGTTGGTATTACTGCGTTATTGTTACTTTTATCTTTACCAGTATTAGCCGGAGCTATTACTATACTTTTAACAGACCGAAATCTTAACACGGCATTTTTTGATCCTGCGGGAGGAGGTGACCCAATTCTTTAC"
    ## 
    ## 
    ## [[94]]
    ## [[94]]$id
    ## [1] "GBMIN35988-13"
    ## 
    ## [[94]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[94]]$gene
    ## [1] "GBMIN35988-13"
    ## 
    ## [[94]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[95]]
    ## [[95]]$id
    ## [1] "GBMIN41067-14"
    ## 
    ## [[95]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[95]]$gene
    ## [1] "GBMIN41067-14"
    ## 
    ## [[95]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAATTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[96]]
    ## [[96]]$id
    ## [1] "GBMIN41069-14"
    ## 
    ## [[96]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[96]]$gene
    ## [1] "GBMIN41069-14"
    ## 
    ## [[96]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[97]]
    ## [[97]]$id
    ## [1] "GBMIN41070-14"
    ## 
    ## [[97]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[97]]$gene
    ## [1] "GBMIN41070-14"
    ## 
    ## [[97]]$sequence
    ## [1] "ACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTG"
    ## 
    ## 
    ## [[98]]
    ## [[98]]$id
    ## [1] "GBMIN41283-14"
    ## 
    ## [[98]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[98]]$gene
    ## [1] "GBMIN41283-14"
    ## 
    ## [[98]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTA"
    ## 
    ## 
    ## [[99]]
    ## [[99]]$id
    ## [1] "GBMIN41284-14"
    ## 
    ## [[99]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[99]]$gene
    ## [1] "GBMIN41284-14"
    ## 
    ## [[99]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTGATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGATTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTACCAACATTTA"
    ## 
    ## 
    ## [[100]]
    ## [[100]]$id
    ## [1] "GBMIN41286-14"
    ## 
    ## [[100]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[100]]$gene
    ## [1] "GBMIN41286-14"
    ## 
    ## [[100]]$sequence
    ## [1] "ACTTTATATTTCATTTTCGGGGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTA"
    ## 
    ## 
    ## [[101]]
    ## [[101]]$id
    ## [1] "GBMIX1115-14"
    ## 
    ## [[101]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[101]]$gene
    ## [1] "GBMIX1115-14"
    ## 
    ## [[101]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[102]]
    ## [[102]]$id
    ## [1] "GBMIX1140-14"
    ## 
    ## [[102]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[102]]$gene
    ## [1] "GBMIX1140-14"
    ## 
    ## [[102]]$sequence
    ## [1] "-----------------------------CAGGAATAGTGGGAACTTCTTTAAGAATACTAATTCGAGCTGAATTAGGTAACCCTGGATCCTTAATTGGAGATGATCAAATTTATAATGTTATTGTGACAGCTCATGCTTTTGTAATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGGGCACCTGATATAGCATTTCCTCGAATAAATAATATAAGATTTTGATTATTACCCCCTTCTTTAACTCTACTCCTAATAAGTTCAATAGTAGAAAGTGGAGCAGGTACTGGGTGAACAGTATACCCCCCTTTGTCATCTGGAATTGCCCATAGAGGTGCTTCTGTAGATTTAGCTATTTTTAGATTACATCTAGCTGGGATTTCTTCAATTCTAGGAGCAGTAAATTTTATTACAACAATTATTAATATACGATCAGTAGGAATAACCTTTGATCGAATACCTTTATTTGTTTGATCTGTAGGTATTACAGCTTTATTACTTTTACTTTCTCTCCCAGTATTAGCAGGAGCTATTACTATACTTTTAACAGACCGTAATTTAAATACTTCTTTTTTCGATCCAGCTGGGGGAGGTGACCCAATTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[103]]
    ## [[103]]$id
    ## [1] "GCOL1620-16"
    ## 
    ## [[103]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[103]]$gene
    ## [1] "GCOL1620-16"
    ## 
    ## [[103]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAATACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[104]]
    ## [[104]]$id
    ## [1] "GCOL1650-16"
    ## 
    ## [[104]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[104]]$gene
    ## [1] "GCOL1650-16"
    ## 
    ## [[104]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[105]]
    ## [[105]]$id
    ## [1] "GCOL1841-16"
    ## 
    ## [[105]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[105]]$gene
    ## [1] "GCOL1841-16"
    ## 
    ## [[105]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[106]]
    ## [[106]]$id
    ## [1] "GCOL1988-16"
    ## 
    ## [[106]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[106]]$gene
    ## [1] "GCOL1988-16"
    ## 
    ## [[106]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[107]]
    ## [[107]]$id
    ## [1] "GCOL2384-16"
    ## 
    ## [[107]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[107]]$gene
    ## [1] "GCOL2384-16"
    ## 
    ## [[107]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[108]]
    ## [[108]]$id
    ## [1] "GCOL2385-16"
    ## 
    ## [[108]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[108]]$gene
    ## [1] "GCOL2385-16"
    ## 
    ## [[108]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[109]]
    ## [[109]]$id
    ## [1] "GCOL260-16"
    ## 
    ## [[109]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[109]]$gene
    ## [1] "GCOL260-16"
    ## 
    ## [[109]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[110]]
    ## [[110]]$id
    ## [1] "GCOL3295-16"
    ## 
    ## [[110]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[110]]$gene
    ## [1] "GCOL3295-16"
    ## 
    ## [[110]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[111]]
    ## [[111]]$id
    ## [1] "GCOL4103-16"
    ## 
    ## [[111]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[111]]$gene
    ## [1] "GCOL4103-16"
    ## 
    ## [[111]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[112]]
    ## [[112]]$id
    ## [1] "GCOL4444-16"
    ## 
    ## [[112]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[112]]$gene
    ## [1] "GCOL4444-16"
    ## 
    ## [[112]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[113]]
    ## [[113]]$id
    ## [1] "GCOL4447-16"
    ## 
    ## [[113]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[113]]$gene
    ## [1] "GCOL4447-16"
    ## 
    ## [[113]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[114]]
    ## [[114]]$id
    ## [1] "GCOL4460-16"
    ## 
    ## [[114]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[114]]$gene
    ## [1] "GCOL4460-16"
    ## 
    ## [[114]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAATATAGTTGAAAACGGATCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGAATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[115]]
    ## [[115]]$id
    ## [1] "GCOL696-16"
    ## 
    ## [[115]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[115]]$gene
    ## [1] "GCOL696-16"
    ## 
    ## [[115]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[116]]
    ## [[116]]$id
    ## [1] "GCOL697-16"
    ## 
    ## [[116]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[116]]$gene
    ## [1] "GCOL697-16"
    ## 
    ## [[116]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[117]]
    ## [[117]]$id
    ## [1] "GCOL698-16"
    ## 
    ## [[117]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[117]]$gene
    ## [1] "GCOL698-16"
    ## 
    ## [[117]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[118]]
    ## [[118]]$id
    ## [1] "GCOL701-16"
    ## 
    ## [[118]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[118]]$gene
    ## [1] "GCOL701-16"
    ## 
    ## [[118]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[119]]
    ## [[119]]$id
    ## [1] "GCOL720-16"
    ## 
    ## [[119]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[119]]$gene
    ## [1] "GCOL720-16"
    ## 
    ## [[119]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCCATTCTAGGGGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[120]]
    ## [[120]]$id
    ## [1] "GCOL729-16"
    ## 
    ## [[120]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[120]]$gene
    ## [1] "GCOL729-16"
    ## 
    ## [[120]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGGCTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCCCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGCCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGGATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[121]]
    ## [[121]]$id
    ## [1] "GCOL750-16"
    ## 
    ## [[121]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[121]]$gene
    ## [1] "GCOL750-16"
    ## 
    ## [[121]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[122]]
    ## [[122]]$id
    ## [1] "GCOL8531-16"
    ## 
    ## [[122]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[122]]$gene
    ## [1] "GCOL8531-16"
    ## 
    ## [[122]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[123]]
    ## [[123]]$id
    ## [1] "GCOL9622-16"
    ## 
    ## [[123]]$name
    ## [1] "Notiophilus biguttatus"
    ## 
    ## [[123]]$gene
    ## [1] "GCOL9622-16"
    ## 
    ## [[123]]$sequence
    ## [1] "AACTTTATATTTTATCTTTGGGACTTGGTCAGGGATAGTTGGAACTTCTTTAAGAATACTAATTCGAGCAGAATTAGGAAATCCTGGATCTTTAATTGGAGATGACCAAATTTATAATGTAATTGTTACAGCTCATGCTTTTGTCATAATTTTTTTTATAGTTATACCTATTATAATTGGAGGATTTGGTAATTGACTTGTACCTCTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATGAGTTTCTGGTTACTTCCTCCCTCTTTAACTCTCCTCCTTACAAGAAGAATAGTGGAAAGAGGAGCAGGTACAGGTTGAACTGTGTACCCTCCCCTTTCTTCTGGAATTGCCCATAGAGGAGCTTCAGTTGATTTAGCAATTTTTAGTCTTCATTTAGCTGGAGTATCTTCTATTTTAGGAGCAGTAAATTTTATTACTACTATTATTAATATACGATCAGTTGGAATATCATTTGATCGAATACCCTTATTTGTGTGATCAGTTGGAATTACAGCTCTTTTATTACTTTTATCCTTACCTGTTTTAGCTGGAGCAATTACTATATTATTAACTGATCGAAACTTAAATACTTCTTTCTTTGACCCTGCTGGGGGAGGAGATCCTATTTTATATCAACACCTATTT"
    ## 
    ## 
    ## [[124]]
    ## [[124]]$id
    ## [1] "GENHP512-11"
    ## 
    ## [[124]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[124]]$gene
    ## [1] "GENHP512-11"
    ## 
    ## [[124]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[125]]
    ## [[125]]$id
    ## [1] "KROK012-19"
    ## 
    ## [[125]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[125]]$gene
    ## [1] "KROK012-19"
    ## 
    ## [[125]]$sequence
    ## [1] "GATATTGGAACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTTTGATTTTTG"
    ## 
    ## 
    ## [[126]]
    ## [[126]]$id
    ## [1] "KROK017-19"
    ## 
    ## [[126]]$name
    ## [1] "Molops piceus"
    ## 
    ## [[126]]$gene
    ## [1] "KROK017-19"
    ## 
    ## [[126]]$sequence
    ## [1] "AAGATATTGGAACATTATATTTTATTTTTGGAGCATGAGCAGGGATAGTAGGAACATCATTAAGAATATTGATTCGAGCTGAATTAGGAAGCCCAGGATCACTAATTGGAGATGATCAAATCTATAATGTAATTGTAACTGCACATGCATTTGTAATAATTTTTTTTATAGTAATACCTATTATAATTGGAGGATTTGGTAACTGATTAGTTCCTTTAATGTTAGGAGCCCCTGATATAGCTTTTCCTCGAATAAACAATATAAGTTTTTGACTTCTCCCTCCATCTTTAACCCTCTTATTAATAAGTAGTATAGTCGAAAAGGGGGCTGGCACAGGATGAACTGTGTACCCTCCTCTCTCATCAACAATTGCCCATAGAGGAGCATCAGTAGATTTAGCTATTTTTAGATTACATTTAGCAGGAGTTTCATCTATTTTAGGTGCTGTAAATTTTATTACTACAATTATTAATATACGATCTGTAGGAATAACATTTGATCGCATACCTTTATTTGTTTGATCAGTAGGAATTACTGCTTTACTATTACTACTATCTCTTCCAGTATTAGCTGGAGCTATTACAATATTACTAACAGATCGAAATTTAAACACTTCTTTTTTTGATCCCGCAGGAGGAGGTGACCCTATTTTATATCAACATTTATTTTGATTTTTTGT"
    ## 
    ## 
    ## [[127]]
    ## [[127]]$id
    ## [1] "TDAAT1157-20"
    ## 
    ## [[127]]$name
    ## [1] "Licinus hoffmannseggii"
    ## 
    ## [[127]]$gene
    ## [1] "TDAAT1157-20"
    ## 
    ## [[127]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGATTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGATCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"
    ## 
    ## 
    ## [[128]]
    ## [[128]]$id
    ## [1] "TDAAT1195-20"
    ## 
    ## [[128]]$name
    ## [1] "Pterostichus burmeisteri"
    ## 
    ## [[128]]$gene
    ## [1] "TDAAT1195-20"
    ## 
    ## [[128]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAACATTTATTT"
    ## 
    ## 
    ## [[129]]
    ## [[129]]$id
    ## [1] "GBCOE855-13"
    ## 
    ## [[129]]$name
    ## [1] "Abax ovalis"
    ## 
    ## [[129]]$gene
    ## [1] "GBCOE855-13"
    ## 
    ## [[129]]$sequence
    ## [1] "AACACTATATTTTATTTTTGGTACATGATCAGGAATAGTAGGAACATCTTTAAGAATATTAATTCGAGCTGAATTAGGAAATCCAGGATCATTAATTGGTGACGACCAAATTTATAATGTAATTGTTACTGCTCATGCATTTGTAATAATTTTTTTTATAGTAATGCCTATTATAATTGGGGGATTTGGAAACTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCGTTCCCTCGAATGAATAACATGAGATTTTGACTGTTACCCCCTTCTCTGACCCTTCTCCTTATAAGCAGCATAGTTGAAAGAGGAACTGGCACAGGATGGACAGTCTACCCACCACTTTCTTCTAATATTGCCCATAGAGGAGCTTCAGTTGACTTGGCTATTTTTAGTTTACATCTAGCTGGAATTTCTTCAATTCTAGGAGCTGTAAATTTTATCACTACAATTATCAATATACGATCAATAGGAATAACTTTTGATCGAATACCTCTATTTGTCTGATCAGTAGGAATCACTGCTTTATTATTATTGTTGTCACTACCTGTATTAGCTGGAGCTATCACAATACTTTTAACTGATCGAAATTTAAATACTTCATTTTTTGATCCAGCAGGAGGTGGAGATCCTATTTTATACCAACATCTGTTT"
    ## 
    ## 
    ## [[130]]
    ## [[130]]$id
    ## [1] "GBCOU5027-14"
    ## 
    ## [[130]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[130]]$gene
    ## [1] "GBCOU5027-14"
    ## 
    ## [[130]]$sequence
    ## [1] "AACTTTATATTTTATTTTTGGTATATGAGCAGGAATAGTAGGTACTTCATTAAGTATATTAATTCGAGCTGAATTAGGTAATCCTGGATCATTAATTGGTGACGATCAAATTTATAATGTTATTGTTACTGCCCATGCATTTGTTATAATTTTCTTTATAGTAATACCTATTATAATTGGAGGATTTGGAAATTGATTAGTTCCTTTAATATTAGGAGCTCCTGATATAGCTTTTCCTCGAATAAATAATATAAGTTTTTGATTACTTCCTCCTTCATTAACACTCCTTTTAATAAGAAGTATAGTTGAAAACGGTTCAGGAACAGGATGAACAGTTTATCCACCTTTATCATCAGGAATTGCACATGCAGGAGCTTCAGTTGATTTAGCTATTTTTAGTTTACATTTAGCTGGAATTTCCTCTATTTTAGGAGCTGTAAATTTTATTACTACAATTATTAATATACGATCAGTAGGGATAACATTTGATCGAATACCTTTATTTGTATGATCTGTTGGAATTACTGCTTTATTATTACTTCTTTCATTACCTGTATTAGCTGGTGCTATTACAATACTATTAACAGATCGAAATTTAAATACTTCTTTTTTTGATCCTGCAGGTGGTGGAGACCCTGTTTTATATCAA---------"
    ## 
    ## 
    ## [[131]]
    ## [[131]]$id
    ## [1] "GBCOU5575-14"
    ## 
    ## [[131]]$name
    ## [1] "Coleoptera"
    ## 
    ## [[131]]$gene
    ## [1] "GBCOU5575-14"
    ## 
    ## [[131]]$sequence
    ## [1] "AACTTTATATTTCATTTTCGGAGCCTGAGCAGGAATAGTAGGTACTTCTTTAAGTATATTAATTCGAGCTGAATTAGGAAATCCAGGATCACTTATTGGTGATGATCAGATTTATAATGTTATTGTTACAGCTCATGCATTTGTAATAATTTTTTTCATAGTAATACCTATTATAATTGGGGGGTTCGGAAACTGATTAGTTCCATTAATATTAGGAGCTCCTGATATAGCTTTCCCTCGAATAAATAATATAAGTTTTTGACTTCTTCCTCCTGCTTTAAGCCTACTTTTAATGAGAAGAGTAGTTGAAAGAGGAGCTGGCACCGGATGAACGGTGTACCCCCCCCTATCATCTAATATTGCCCATAGAGGTGCTTCCGTTGACTTAGCAATTTTCAGATTACACTTAGCGGGAGTATCTTCCATTTTAGGAGCTGTAAATTTTATTACCACTATTATTAATATACGATCAATAGGAATAACATTTGACCGAATACCATTATTTGTATGATCAGTAGGAATTACTGCTTTACTATTACTTTTATCATTACCAGTATTGGCTGGAGCTATTACAATACTTTTAACAGATCGAAATTTAAATACTTCATTTTTTGATCCTGCAGGAGGGGGAGACCCAATTCTTTATCAACATTTATTT"

``` r
search.BOLD()
```

    ## Warning: 'search.BOLD' is deprecated. Please use the 'bold' package.

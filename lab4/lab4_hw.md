---
title: "Lab 4 Homework"
author: "Grace Ochieng"
date: "2023:1:23`"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**


```r
homerange <- readr::read_csv("data/Tamburelloetal_HomerangeDatabase.csv")
```

```
## Rows: 569 Columns: 24
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  

Dimensions 

```r
dim(homerange)
```

```
## [1] 569  24
```

Column names

```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

Statstitical summary this also showes the class for each variable

```r
summary (homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  

Part one- Taxon
Variable of Taxon changed to factor

```r
class(homerange$taxon)
```

```
## [1] "character"
```

```r
homerange$taxon <-as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```

Levels of Taxon

```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```
 
Part Two- order
Variable of 'order' changed to factor

```r
homerange$order <-as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```
 Levels of order

```r
levels(homerange$order)
```

```
##  [1] "accipitriformes"       "afrosoricida"          "anguilliformes"       
##  [4] "anseriformes"          "apterygiformes"        "artiodactyla"         
##  [7] "caprimulgiformes"      "carnivora"             "charadriiformes"      
## [10] "columbidormes"         "columbiformes"         "coraciiformes"        
## [13] "cuculiformes"          "cypriniformes"         "dasyuromorpha"        
## [16] "dasyuromorpia"         "didelphimorphia"       "diprodontia"          
## [19] "diprotodontia"         "erinaceomorpha"        "esociformes"          
## [22] "falconiformes"         "gadiformes"            "galliformes"          
## [25] "gruiformes"            "lagomorpha"            "macroscelidea"        
## [28] "monotrematae"          "passeriformes"         "pelecaniformes"       
## [31] "peramelemorphia"       "perciformes"           "perissodactyla"       
## [34] "piciformes"            "pilosa"                "proboscidea"          
## [37] "psittaciformes"        "rheiformes"            "roden"                
## [40] "rodentia"              "salmoniformes"         "scorpaeniformes"      
## [43] "siluriformes"          "soricomorpha"          "squamata"             
## [46] "strigiformes"          "struthioniformes"      "syngnathiformes"      
## [49] "testudines"            "tetraodontiformes\xa0" "tinamiformes"
```
 
**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.** 

The taxa represented in the homerange data frame 

```r
levels(homerange$taxon)
```

```
## [1] "birds"         "lake fishes"   "lizards"       "mammals"      
## [5] "marine fishes" "river fishes"  "snakes"        "tortoises"    
## [9] "turtles"
```

Changing to the 'Taxa' data frame

```r
taxa <- select(homerange,taxon: species )
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  

Table for Common name 

```r
table (homerange$common.name)
```

```
## 
##                         aardwolf                 Abert's squirrel 
##                                1                                1 
##                   Abert's towhee                Aesculapian snake 
##                                1                                1 
##   African brush-tailed porcupine            African bush elephant 
##                                1                                1 
##              allied rock-wallaby                  American badger 
##                                1                                1 
##                   American bison                     american eel 
##                                1                                1 
##         American gray flycatcher                 American kestrel 
##                                1                                1 
##                  American marten                    American pika 
##                                1                                1 
##            American red squirrel                American redstart 
##                                1                                1 
##            American tree sparrow          American yellow warbler 
##                                1                                1 
##            Anegada ground iguana          Angel island chuckwalla 
##                                1                                1 
##              antilopine kangaroo                       arctic fox 
##                                1                                1 
##           arctic ground squirrel                      Arctic hare 
##                                1                                1 
##                     arctic shrew                           argali 
##                                1                                1 
##                   Armenian viper                   Asian elephant 
##                                1                                1 
##                  atlantic salmon        atlantic sharpnose puffer 
##                                1                                1 
##               australian gregory           Bahamian Andros iguana 
##                                1                                1 
##                    ballan wrasse             banded ground-cuckoo 
##                                1                                1 
##                   banded sculpin       banner-tailed kangaroo rat 
##                                1                                1 
##                    barbary sheep                         barn owl 
##                                1                                1 
##                 barred sand bass                       bay dikier 
##                                1                                1 
##                     beech marten                     Bell's vireo 
##                                1                                1 
##                     bermuda chub                   Berwick's wren 
##                                1                                1 
##               bicolor damselfish                    bighorn sheep 
##                                1                                1 
##                    black grouper                     black grouse 
##                                1                                1 
##                 black rhinoceros                   black rockfish 
##                                1                                1 
##                 black woodpecker           black-capped chickadee 
##                                1                                1 
##               black-capped vireo              black-footed ferret 
##                                1                                1 
##            black-striped wallaby          black-tailed jackrabbit 
##                                1                                1 
##     black-throated green warbler             Blackburnian warbler 
##                                1                                1 
##                  blackear wrasse                    blackeye goby 
##                                1                                1 
##                       blacksnake               blacktail redhorse 
##                                1                                1 
##          blacktailed rattlesnake                Blanding's turtle 
##                                1                                1 
##                      blue iguana                    blue rockfish 
##                                1                                1 
##                  bluebanded goby                         bluegill 
##                                1                                1 
##                  bluehead wrasse            bluespine unicornfish 
##                                1                                1 
##        bluestreak cleaner wrasse                           bobcat 
##                                1                                1 
##                  Bonelli's eagle                     booted eagle 
##                                1                                1 
##                       boreal owl            Botta's pocket gopher 
##                                1                                1 
##              Brazilian porcupine        bridled nail-tail wallaby 
##                                1                                1 
##              broad-toothed mouse                broadheaded snake 
##                                1                                1 
##                 brown antechinus                      brown trout 
##                                1                                1 
##                  brown wood rail                         bushbuck 
##                                1                                1 
##        bushmanland tent tortoise             bushy-tailed woodrat 
##                                1                                1 
##             butlers garter snake                          cabezon 
##                                1                                1 
##       California ground squirrel            california sheepshead 
##                                1                                1 
##                  California vole                      Canada lynx 
##                                1                                1 
##                   Canada warbler                    canary damsel 
##                                1                                1 
##                    canyon towhee               cape dune mole rat 
##                                1                                1 
##                       cape genet                        cape hare 
##                                1                                1 
##                    cape mole rat                   cape porcupine 
##                                1                                1 
##                          caracal                         caracara 
##                                1                                1 
##               Carolina chickadee                    Carolina wren 
##                                1                                1 
##                              cat              central stoneroller 
##                                1                                1 
##                  Chacoan peccary                          chamois 
##                                1                                1 
##                checkered snapper                          cheetah 
##                                1                                1 
##                       cherubfish           chestnut-sided warbler 
##                                1                                1 
##            chevron butterflyfish                   chicken turtle 
##                                1                                1 
##                chinese pit viper                 chipping sparrow 
##                                1                                1 
##                           chital                   cinereus shrew 
##                                1                                1 
##                     clown wrasse                        coachwhip 
##                                1                                1 
##                 cocoa damselfish                 collared peccary 
##                                1                                1 
##                Colorado chipmunk        Columbian ground squirrel 
##                                1                                1 
##                           comber          common brushtail possum 
##                                1                                1 
##                   common buzzard                 common chaffinch 
##                                1                                1 
##                common chuckwalla                    common cuckoo 
##                                1                                1 
##            common dwarf mongoose                     common eland 
##                                1                                1 
##                 common firecrest                     common genet 
##                                1                                1 
##                    common linnet                  common mole rat 
##                                1                                1 
##                     common raven                  common redstart 
##                                1                                1 
##           common snapping turtle                  common wallaroo 
##                                1                                1 
##                    common wombat               common wood pigeon 
##                                1                                1 
##              common yellowthroat                    Cooper's hawk 
##                                1                                1 
##                  copper rockfish           copperbelly watersnake 
##                                1                                1 
##                       copperhead                    coral grouper 
##                                1                                1 
##                       coral hind                      coral trout 
##                                1                                1 
##                        corncrake                           coruro 
##                                1                                1 
##                     cotton mouse                      cottonmouth 
##                                1                                1 
##                           cougar                    crowned shrew 
##                                1                                1 
##                           culpeo                           cunner 
##                                1                                1 
##                  cutthroat trout               Cuvier's spiny rat 
##                                1                                1 
##      Dalh's toad-headed tortoise              Damaraland mole rat 
##                                1                                1 
##                       damselfish                 Dartford warbler 
##                                1                                1 
##                    desert iguana                  desert tortoise 
##                                1                                1 
##                   desert warthog                   desert woodrat 
##                                1                                1 
##                    dusky grouper                     dusky grouse 
##                                1                                1 
##             dusky-footed woodrat          dwarf fat-tailed jerboa 
##                                1                                1 
##                   dwarf hawkfish            east African mole rat 
##                                1                                1 
##                  eastern bettong                 eastern bluebird 
##                                1                                1 
##               eastern cottontail            eastern gray squirrel 
##                                1                                1 
##            Eastern grey kangaroo             eastern indigo snake 
##                                1                                1 
##                 eastern kingbird                Eastern kingsnake 
##                                1                                1 
##       Eastern long-necked turtle               eastern meadowlark 
##                                1                                1 
##                     eastern mole               Eastern mud turtle 
##                                1                                1 
##   Eastern spiny softshell turtle eastern triangular butterflyfish 
##                                1                                1 
##               eastern wood pewee               eastern worm snake 
##                                1                                1 
##                Egyptian mongoose                Egyptian tortoise 
##                                1                                1 
##                 Egyptian vulture       elegant fat-tailed opossum 
##                                1                                1 
##                   Ethiopian wolf               Eurasian eagle-owl 
##                                1                                1 
##                    Eurasian lynx               Eurasian pygmy owl 
##                                1                                1 
##             Eurasian sparrowhawk   Eurasian three-toed woodpecker 
##                                1                                1 
##             Eurasian treecreeper                    Eurasian wren 
##                                1                                1 
##                 Eurasian wryneck                   European bison 
##                                1                                1 
##        European green woodpecker                    European hare 
##                                1                                1 
##                European hedgehog                 European kestrel 
##                                1                                1 
##                    European mink                    European mole 
##                                1                                1 
##                European nightjar                European nuthatch 
##                                1                                1 
##             European pine marten             European pond turtle 
##                                1                                1 
##                  European rabbit                  European roller 
##                                1                                1 
##                 european seabass                   European serin 
##                                1                                1 
##             European turtle dove               European whipsnake 
##                                1                                1 
##                      fallow deer                     fer-de-lance 
##                                1                                1 
##                           ferret                       field vole 
##                                1                                1 
##                           fisher                            fossa 
##                                1                                1 
##         four-toed elephant shrew                     fox squirrel 
##                                1                                1 
##       Franklin's ground squirrel                          gadwall 
##                                1                                1 
##            Galapagos land iguana                   Geoffroy's cat 
##                                1                                1 
##              giant garter snakes                giant golden mole 
##                                1                                1 
##               giant kangaroo rat                      giant panda 
##                                1                                1 
##                   giant trevally                       gila trout 
##                                1                                1 
##                gilthead seabream                          giraffe 
##                                1                                1 
##                             goat                        goldcrest 
##                                1                                1 
##                 golden bandicoot                     golden eagle 
##                                1                                1 
##     golden-rumped elephant shrew                     gopher snake 
##                                1                                1 
##                  gopher tortoise              Grant's golden mole 
##                                1                                1 
##                      grass snake              grasshopper sparrow 
##                                1                                1 
##                     gray snapper                          graysby 
##                                1                                1 
##                   greasy grouper                    great bittern 
##                                1                                1 
##                 great horned owl            great plains ratsnake 
##                                1                                1 
##             great spotted cuckoo                   greater glider 
##                                1                                1 
##                   greater grison                     greater kudu 
##                                1                                1 
##          greater prairie-chicken                     greater rhea 
##                                1                                1 
##               greater roadrunner       greater white-footed shrew 
##                                1                                1 
##                   grey partridge           grey-headed woodpecker 
##                                1                                1 
##                        groundhog            G\xfcnther's dik-dik 
##                                1                                1 
##             half-banded seaperch                       hartebeest 
##                                1                                1 
##                   hazel dormouse                     hazel grouse 
##                                1                                1 
##                      hen harrier             High Mountain Lizard 
##                                1                                1 
##                    hognose snake                           hoopoe 
##                                1                                1 
##                            horse                       house wren 
##                                1                                1 
##                  humphead wrasse                     Iberian lynx 
##                                1                                1 
##                           impala               impressed tortoise 
##                                1                                1 
##                        inca dove         Indian crested porcupine 
##                                1                                1 
##               Indian desert jird                      Indian hare 
##                                1                                1 
##                   indigo bunting                     island mouse 
##                                1                                1 
##                           jaguar                       jaguarundi 
##                                1                                1 
##          japanese black rockfish              japanese shrimpgoby 
##                                1                                1 
##                Japanese squirrel                           kakapo 
##                                1                                1 
##                        kelp bass                        king rail 
##                                1                                1 
##                         kinkajou               Kirtland's warbler 
##                                1                                1 
##                          kit fox                      land mullet 
##                                1                                1 
##                    lanner falcon               large indian civet 
##                                1                                1 
##            large-headed rice rat                  largemouth bass 
##                                1                                1 
##                    least bittern                   least chipmunk 
##                                1                                1 
##                 least flycatcher                     least weasel 
##                                1                                1 
##                          leopard                      leopard cat 
##                                1                                1 
##                 leopard tortoise               lesser grey shrike 
##                                1                                1 
##                      lesser rhea                lined surgeonfish 
##                                1                                1 
##                       little owl                loggerhead shrike 
##                                1                                1 
##                long-clawed shrew              long-eared hedgehog 
##                                1                                1 
##                   long-eared owl              long-footed potoroo 
##                                1                                1 
##            long-snouted seahorse                  long-tailed tit 
##                                1                                1 
##               long-tailed weasel                  longear sunfish 
##                                1                                1 
##                  longfinned goby                    longnose dace 
##                                1                                1 
##         Lumholtz's tree-kangaroo                 magnolia warbler 
##                                1                                1 
##               Malagasy giant rat                      maned sloth 
##                                1                                1 
##                     maori wrasse                           margay 
##                                1                                1 
##                Marmora's warbler                   marsh mongoose 
##                                1                                1 
##                     marsh rabbit                        marsh tit 
##                                1                                1 
##                      meadow vole     mediterranean rainbow wrasse 
##                                1                                1 
##           mediterranean tortoise                melodious warbler 
##                                1                                1 
##              melon butterflyfish           Merriam's kangaroo rat 
##                                1                                1 
##       middle spotted woodpeckers         midget faded rattlesnake 
##                                1                                1 
##           midland painted turtle                        milksnake 
##                                1                                1 
##               Mojave rattlesnake                Montagu's harrier 
##                                1                                1 
##                     montane vole                      moon wrasse 
##                                1                                1 
##                            moose                  mottled sculpin 
##                                1                                1 
##                  mountain beaver                 mountain gazelle 
##                                1                                1 
##                    mountain goat                    mountain hare 
##                                1                                1 
##                 mourning warbler                        mule deer 
##                                1                                1 
##                      muskellunge                          muskrat 
##                                1                                1 
##                   mutton snapper                   naked mole rat 
##                                1                                1 
##              namaqua dwarf adder                   nassau grouper 
##                                1                                1 
##         North American porcupine              northern brown kiwi 
##                                1                                1 
##         Northern flying squirrel                 Northern goshawk 
##                                1                                1 
##      northern hairy-nosed wombat             northern mockingbird 
##                                1                                1 
##           Northern parl squirrel   Northern three-striped opossum 
##                                1                                1 
##              Northern watersnake                northern wheatear 
##                                1                                1 
##                     Oak titmouse                  ocean whitefish 
##                                1                                1 
##                           ocelot                            okapi 
##                                1                                1 
##          orangespine unicornfish               Ord's kangaroo rat 
##                                1                                1 
##                ornate box turtle                   ornate tinamou 
##                                1                                1 
##                          ostrich                         ovenbird 
##                                1                                1 
##                    oystercatcher                   painted comber 
##                                1                                1 
##                      pampas deer                  Patagonian mara 
##                                1                                1 
##                     peacock hind                 peregrine falcon 
##                                1                                1 
##             Peruvian plantcutter                   Peter's dukier 
##                                1                                1 
##                       pine snake                  plains viscacha 
##                                1                                1 
##                     plateau pika                          pollack 
##                                1                                1 
##                   prairie falcon                     prairie vole 
##                                1                                1 
##                        pronghorn             prothonotary warbler 
##                                1                                1 
##                             pudu                      pumpkinseed 
##                                1                                1 
##                     pygmy rabbit               quillback rockfish 
##                                1                                1 
##                            racer                    rainbow trout 
##                                1                                1 
##                red bush squirrel                         red deer 
##                                1                                1 
##                      red grouper                         red hind 
##                                1                                1 
##                     red kangaroo                         red kite 
##                                1                                1 
##                         red moki                        red panda 
##                                1                                1 
##                     red squirrel                red-backed shrike 
##                                1                                1 
##          red-crowned ant tanager                   red-eyed vireo 
##                                1                                1 
##              red-footed tortoise             red-legged pademelon 
##                                1                                1 
##             red-necked pademelon               red-necked wallaby 
##                                1                                1 
##              red-shouldered hawk                  red-tailed hawk 
##                                1                                1 
##         red-throated ant tanager            red-throated caracara 
##                                1                                1 
##               redbacked ratsnake               redband parrotfish 
##                                1                                1 
##                  redbanded perch                redfin parrotfish 
##                                1                                1 
##                    redlip blenny              redspotted hawkfish 
##                                1                                1 
##               redtail parrotfish                 Reeves's muntjac 
##                                1                                1 
##                         reindeer                   ringneck snake 
##                                1                                1 
##             rivulated parrotfish                        rock bass 
##                                1                                1 
##                    rock squirrel                         roe deer 
##                                1                                1 
##                       Roman mole                    rosyside dace 
##                                1                                1 
##            rufous elephant shrew                     Ruppel's fox 
##                                1                                1 
##          Russian steppe tortoise                       rusty goby 
##                                1                                1 
##                      sage grouse                           saithe 
##                                1                                1 
##                           salema         salt marsh harvest mouse 
##                                1                                1 
##             schoolmaster snapper                          sculpin 
##                                1                                1 
##                           serval               sharp-shinned hawk 
##                                1                                1 
##           short-toed snake eagle           Siberian brown lemming 
##                                1                                1 
##                Siberian chipmunk                  Siberian weasel 
##                                1                                1 
##                       sidewinder                        sika deer 
##                                1                                1 
##                 silvery mole rat                    slender shrew 
##                                1                                1 
##                    slippery dick                       sloth bear 
##                                1                                1 
##                  smallmouth bass                     snow leopard 
##                                1                                1 
##                    snowshoe hare                        snowy owl 
##                                1                                1 
##                  snubnosed viper          South American gray fox 
##                                1                                1 
##             southern bog lemming         Southern brown bandicoot 
##                                1                                1 
##         Southern flying squirrel       southern grasshopper mouse 
##                                1                                1 
##          Southern plains woodrat       southwestern carpet python 
##                                1                                1 
##                  spanish hogfish                     Spanish ibex 
##                                1                                1 
##              Spanish pond turtle              spectacled dormouse 
##                                1                                1 
##    Speke's hinge-backed tortoise                spiny tail lizard 
##                                1                                1 
##               spotted flycatcher          spotted ground squirrel 
##                                1                                1 
##               spotted nutcracker            spur-thighed tortoise 
##                                1                                1 
##                  star-nosed mole                         steenbok 
##                                1                                1 
##             steephead parrotfish           Stephen's kangaroo rat 
##                                1                                1 
##                  stinkpot turtle                            stoat 
##                                1                                1 
##             stoplight parrotfish         streaked fantail warbler 
##                                1                                1 
##        stripe-necked musk turtle          striped ground squirrel 
##                                1                                1 
##               striped parrotfish                  Swainson's hawk 
##                                1                                1 
##                     swamp rabbit                    swamp wallaby 
##                                1                                1 
##                        swift fox          Tahititan butterflyfish 
##                                1                                1 
##                        tawny owl                            tayra 
##                                1                                1 
##           teardrop butterflyfish                  Tenerife lizard 
##                                1                                1 
##   thick-tailed three-toed jerboa   thirteen-lined ground squirrel 
##                                1                                1 
##               thumbprint emperor                            tiger 
##                                1                                1 
##                      tiger quoll                tiger rattlesnake 
##                                1                                1 
##                      tiger snake               timber rattlesnake 
##                                1                                1 
##                 Tome's spiny rat           tooth-billed bowerbird 
##                                1                                1 
##              travancore tortoise         twin-spotted rattlesnake 
##                                1                                1 
##              twinspot damselfish                   Uinta chipmunk 
##                                1                                1 
##                     wards damsel                 water chevrotain 
##                                1                                1 
##                       water vole        Western Bonelli's warbler 
##                                1                                1 
##             western capercaillie              western diamondback 
##                                1                                1 
##            Western grey kangaroo               western meadowlard 
##                                1                                1 
##                    Western quoll                 western ratsnake 
##                                1                                1 
##          western red-backed vole               western worm snake 
##                                1                                1 
##           western yellow wagtail                         whinchat 
##                                1                                1 
##                    white crappie                   white goatfish 
##                                1                                1 
##                 white rhinoceros                    white wagtail 
##                                1                                1 
##          white-backed woodpecker         White-bellied\xa0nesomys 
##                                1                                1 
##                 white-eyed vireo             white-footed dunnart 
##                                1                                1 
##             white-lipped peccary                white-tailed deer 
##                                1                                1 
##            white-tailed mongoose             whitesaddle goatfish 
##                                1                                1 
##              whitetail dascyllus                          wildcat 
##                                1                                1 
##                 willow ptarmigan                        wolverine 
##                                1                                1 
##                     wood lemming                       wood mouse 
##                                1                                1 
##                  woodchat shrike                    woodland vole 
##                                1                                1 
##                         woodlark                    worm pipefish 
##                                1                                1 
##                          wrentit             yellow bellied racer 
##                                1                                1 
##                  yellow bullhead                  yellow mongoose 
##                                1                                1 
##                     yellow perch            yellow-bellied marmot 
##                                1                                1 
##       yellow-blotched map turtle             yellow-breasted chat 
##                                1                                1 
##              yellow-necked mouse             yellow-pine chipmunk 
##                                1                                1 
##                   yellowfin hind                yellowhead wrasse 
##                                1                                1 
##               yellowtail snapper 
##                                1
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  


```r
table(homerange$trophic.guild)
```

```
## 
## carnivore herbivore 
##       342       227
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  

Code chunk only restricted for carnivores data frame

```r
carnivore.animals <-filter(homerange, trophic.guild == "carnivore")
```

Data frame for carivores 

```r
filter(homerange, trophic.guild == "carnivore")
```

```
## # A tibble: 342 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 lake … americ… acti… angu… angui… angu… rostra… teleme… 16       887    2.95 
##  2 river… blackt… acti… cypr… catos… moxo… poecil… mark-r… <NA>     562    2.75 
##  3 river… centra… acti… cypr… cypri… camp… anomal… mark-r… 20        34    1.53 
##  4 river… rosysi… acti… cypr… cypri… clin… fundul… mark-r… 26         4    0.602
##  5 river… longno… acti… cypr… cypri… rhin… catara… mark-r… 17         4    0.602
##  6 river… muskel… acti… esoc… esoci… esox  masqui… teleme… 5       3525    3.55 
##  7 marin… pollack acti… gadi… gadid… poll… pollac… teleme… 2        737.   2.87 
##  8 marin… saithe  acti… gadi… gadid… poll… virens  teleme… 2        449.   2.65 
##  9 marin… giant … acti… perc… caran… cara… ignobi… teleme… 4        726.   2.86 
## 10 lake … rock b… acti… perc… centr… ambl… rupest… mark-r… 16       196    2.29 
## # … with 332 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

Code chunk only restricted for herbivores data frame

```r
herbivore.animals <-filter(homerange, trophic.guild == "herbivore")
```

Data for herbivores

```r
filter(homerange, trophic.guild == "herbivore")
```

```
## # A tibble: 227 × 24
##    taxon  commo…¹ class order family genus species prima…² N     mean.…³ log10…⁴
##    <fct>  <chr>   <chr> <fct> <chr>  <chr> <chr>   <chr>   <chr>   <dbl>   <dbl>
##  1 marin… lined … acti… perc… acant… acan… lineat… direct… <NA>   109.     2.04 
##  2 marin… orange… acti… perc… acant… naso  litura… teleme… 8      772.     2.89 
##  3 marin… bluesp… acti… perc… acant… naso  unicor… teleme… 7      152.     2.18 
##  4 marin… redlip… acti… perc… blenn… ophi… atlant… direct… 20       6.2    0.792
##  5 marin… bermud… acti… perc… kypho… kyph… sectat… teleme… 11    1087.     3.04 
##  6 marin… cherub… acti… perc… pomac… cent… argi    direct… <NA>     2.5    0.398
##  7 marin… damsel… acti… perc… pomac… chro… chromis direct… <NA>    28.4    1.45 
##  8 marin… twinsp… acti… perc… pomac… chry… biocel… direct… 18       9.19   0.963
##  9 marin… wards … acti… perc… pomac… poma… wardi   direct… <NA>    10.5    1.02 
## 10 marin… austra… acti… perc… pomac… steg… apical… direct… <NA>    45.3    1.66 
## # … with 217 more rows, 13 more variables: alternative.mass.reference <chr>,
## #   mean.hra.m2 <dbl>, log10.hra <dbl>, hra.reference <chr>, realm <chr>,
## #   thermoregulation <chr>, locomotion <chr>, trophic.guild <chr>,
## #   dimension <dbl>, preymass <dbl>, log10.preymass <dbl>, PPMR <dbl>,
## #   prey.size.reference <chr>, and abbreviated variable names ¹​common.name,
## #   ²​primarymethod, ³​mean.mass.g, ⁴​log10.mass
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  
Herbivore

```r
mean(herbivore.animals$mean.hra.m2, na.rm=T)
```

```
## [1] 34137012
```

Carnivore

```r
mean(carnivore.animals$mean.hra.m2, na.rm=T)
```

```
## [1] 13039918
```
In comparison herbivores have a larger mean, 'mean.hra.m2'
 
**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?**  



```r
deer <-select (homerange, "log10.mass", "family", "genus", "mean.mass.g")
deer.cervidae <-filter (deer, family =="cervidae")
deer.cervidae
```

```
## # A tibble: 12 × 4
##    log10.mass family   genus      mean.mass.g
##         <dbl> <chr>    <chr>            <dbl>
##  1       5.49 cervidae alces          307227.
##  2       4.80 cervidae axis            62823.
##  3       4.38 cervidae capreolus       24050.
##  4       5.37 cervidae cervus         234758.
##  5       4.47 cervidae cervus          29450.
##  6       4.85 cervidae dama            71450.
##  7       4.13 cervidae muntiacus       13500.
##  8       4.73 cervidae odocoileus      53864.
##  9       4.94 cervidae odocoileus      87884.
## 10       4.54 cervidae ozotoceros      35000.
## 11       3.88 cervidae pudu             7500.
## 12       5.01 cervidae rangifer       102059.
```


```r
arrange (deer.cervidae, log10.mass)
```

```
## # A tibble: 12 × 4
##    log10.mass family   genus      mean.mass.g
##         <dbl> <chr>    <chr>            <dbl>
##  1       3.88 cervidae pudu             7500.
##  2       4.13 cervidae muntiacus       13500.
##  3       4.38 cervidae capreolus       24050.
##  4       4.47 cervidae cervus          29450.
##  5       4.54 cervidae ozotoceros      35000.
##  6       4.73 cervidae odocoileus      53864.
##  7       4.80 cervidae axis            62823.
##  8       4.85 cervidae dama            71450.
##  9       4.94 cervidae odocoileus      87884.
## 10       5.01 cervidae rangifer       102059.
## 11       5.37 cervidae cervus         234758.
## 12       5.49 cervidae alces          307227.
```
The largest deer is the Alcels and its common name is the moose

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**   

Now we create a new data set for the viperidae family which are the snakes  

```r
snake <-select (homerange, "log10.mass", "family", "genus", "mean.hra.m2")
```


```r
snake.x <-filter (deer, family =="viperidae")
snake.x
```

```
## # A tibble: 15 × 4
##    log10.mass family    genus       mean.mass.g
##         <dbl> <chr>     <chr>             <dbl>
##  1       2.36 viperidae agkistrodon       231. 
##  2       2.27 viperidae agkistrodon       188  
##  3       1.23 viperidae bitis              17.0
##  4       2.92 viperidae bothrops          826. 
##  5       2.51 viperidae crotalus          320. 
##  6       2.03 viperidae crotalus          107. 
##  7       3.01 viperidae crotalus         1020  
##  8       2.62 viperidae crotalus          414  
##  9       2.14 viperidae crotalus          139. 
## 10       1.83 viperidae crotalus           67.2
## 11       2.45 viperidae crotalus          280. 
## 12       2.37 viperidae crotalus          235. 
## 13       2.29 viperidae gloydius          197. 
## 14       2.21 viperidae montivipera       162. 
## 15       1.99 viperidae vipera             97.4
```


```r
arrange (snake.x, log10.mass)
```

```
## # A tibble: 15 × 4
##    log10.mass family    genus       mean.mass.g
##         <dbl> <chr>     <chr>             <dbl>
##  1       1.23 viperidae bitis              17.0
##  2       1.83 viperidae crotalus           67.2
##  3       1.99 viperidae vipera             97.4
##  4       2.03 viperidae crotalus          107. 
##  5       2.14 viperidae crotalus          139. 
##  6       2.21 viperidae montivipera       162. 
##  7       2.27 viperidae agkistrodon       188  
##  8       2.29 viperidae gloydius          197. 
##  9       2.36 viperidae agkistrodon       231. 
## 10       2.37 viperidae crotalus          235. 
## 11       2.45 viperidae crotalus          280. 
## 12       2.51 viperidae crotalus          320. 
## 13       2.62 viperidae crotalus          414  
## 14       2.92 viperidae bothrops          826. 
## 15       3.01 viperidae crotalus         1020
```

The smallest snake is the bitis are commonly known as African adders. It is venomous and commonly found in west and central regions of the African continent.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   

+++
date = '2026-04-15T14:54:03+01:00'
draft = true
title = 'Explorations with record linkage'
ShowToc = true
tags = ["census", "record-linkage"]
author = "Josh"
+++

## Record linkage

What is this post for? Who is this post for?

Linking records with norminal record linkage is 

I've just come across an impressive [working paper](https://doi.org/10.17863/CAM.120530) released by Campop (at Cambridge University) back in August 2025 detailing the first attempt to link every person between the 1851 and 1921 England and Wales (???) censuses. There have been several attempts (mine included) to link subsets of indivduals between censuses using I-CeM data. But this is the first to link all xxx million people. 👏 to the paper's authors G. Proffit, A. Litvine, E. Diduch, R. Linacre & E. Chung - I'm looking forward to reading the published paper when it's out!

Very generously, they've released a [10% sample](https://doi.org/10.5281/zenodo.17184801) of their record linkage dataset ahead of full publication. In this post, I'm using this sample to explore their links between the 1851 and 1861 censuses and comparing them with my own linked subset made up of weavers for the same years.

This is what their linked sample looks like:

unique_id_l|unique_id_r|
:--:|:--:|
1851/13855314|1861/15945942|
1851/17205716|1861/9964164|
1851/6503654|1861/7043768|

The numbers to the right of the slashes are the `recid` values (unique person identifiers) found in I-CeM. This table is telling us that `recid` 13855314 in 1851 and `recid` 15945942 in 1861 are the same person. (add who this actually is) You can join these id values to a full copy of I-CeM to add all the information in the census for this person (name, address, occupation, age, gender etc). N.B. The names and addresses in I-CeM are a separate dataset that you need a [special licence](http://doi.org/10.5255/UKDA-SN-7856-2) to access.

There are 651,524 people in the 10% linked 1851-1861 sample. I have a sample of xxxx weavers linked between the same censuses. My analysis below is based on the 10,000 weavers found in both samples.

Encouragingly, we linked the same people in 87.4% (8,736 weavers) of cases. Just because we've come to the same result doesn't necessarily mean these are all correct (aka [true positives](https://en.wikipedia.org/wiki/Sensitivity_and_specificity)). Probably a small proportion will be wrong but it would take me far too long to manually checking each one! It's encouraging that we've come to the same result in almost 90% of cases since we've independently run different types of linkage algorithm (mine deterministic, theirs probabalistic - more on this later) and come back with the same result. I think it's safe to say that we won't be able to improve on these links without can be pretty sure most of these are correct based on the information recorded in I-CeM since.



Now for the interesting bit, the 22.6% where we disagree...

I've manually looked up the original census returns on findmypast for the 1,264 weavers.

Here's what I found:

Status|PLD25|My Sample|
--|--|--|
Correct||
Wrong||
Can't decide|






> For any use of the data or our methodology, please quote: Proffit, G., Litvine, A., Diduch, E., Linacre, R., & Chung, E. (2025). A First Full-Count Linking of English and Welsh Censuses, 1851-1921, data (https://doi.org/10.5281/zenodo.15727456) and working paper (https://doi.org/10.17863/CAM.120530)
### Immutable vs mutable characteristics




They've used [Splink](https://github.com/moj-analytical-services/splink) a python package for large-scale probabalistic record linkage produced by the UK's Ministry of Justice used widely in government, industry, and academia.



For anyone who doesn't know, digitised historic British census data is available via the [UK Data Service](https://icem.ukdataservice.ac.uk/). 
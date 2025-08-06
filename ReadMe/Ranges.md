## Ranges Module

These module contains to main classes, `Ranges` moduel along with its counterparts `RangesList` and `RangesDict` are for storing arbitrary ranges. These can be any integer based ranges (that's the current limitation). Once you have a few ranges you can calculate the distance between them, you can merge them, calculate overlaps between 2 ranges. 

All these operations are also supported in `GenomicRanges` instances as well. It also requires strand and chromosome information for more biologically relevant calculations. These modules can be used on their own for perfoming pythonic operations similar to R's `GenomicFeatures` package. They are also being heavily used by the `genome.genome.Genome` class for querying, and some of the endpoints in the `apis.ensembl.Ensembl` instance. Please see the specific readme under the ranges module for usage instructions. 

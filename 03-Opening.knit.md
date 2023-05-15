#  Opening UKDS datasets in R
## Essential information
In principle, any  dataset whether in CSV, SPSS, SAS, or Stata format can be opened by R. There are a number of issues to consider however:

- The `foreign` package has been traditionally used  to import SPSS and Stata datasets into R:

  - `read.spss()` and `write.spss()` respectively open and write .sav files. Given that both were developed from  older versions of SPSS, it is therefore advised  to check that their outcome is as expected. In addition
    - `read.spss()` does not store the data in a R data frame by default and will require the option         `to.data.frame=T` to be specified.
    - `read.spss()` may sometimes struggle with some numeric format and wrongly attempt to convert them as factor, which will result in error messages. It is therefore advised to limit the maximum number of levels that  will be considered when converting factors  by using  the option   `max.value.labels=`

  - `read.dta()` and `write.dta()` respectively open and write Stata files up to version 12. An option to watch for is `convert.factor=T/F` which either will import  Stata categorical variable as their underlying numeric value or instead will convert them into factors, 
  using value labels as levels, which may be an issue for categorical variables with    a large number of levels. Users have to bear in mind that the labels will by default sorted alphabetically, . 

- The `readstata13` package opens  Stata datasets from version 13 onwards with the `read.dta13()` function and offers a more comprehensive set of options. `convert.factor=T/F` has the same effect as in  `read.dta()` from `foreign`.

- Data frames created with either `read.dta()` or `read.dta13()` have extra information stored as attributes, which maybe useful to retrieve. For instance:

```
> mydata<-read.dta("Some_Stata_dataset.dta")
> attributes(mydata)$var.labels   ### Retrieves the original Stata variable labels
```

- Finally the `haven` package opens SPSS, Stata and SAS files with respectively `read_spss()`, `read_dta()` and `read_sas()`. By contrast with the other two packages, it relies on ad hoc data formats and data structures for converting labelled categorical variables and attempts to mimic Stata's value and variable labels. More information is available [here](https://haven.tidyverse.org/reference/read_dta.html).

In order not to overcomplicate their initial exploration of R we recommend new users to use  `read.spss()` or `read.dta13()` when importing datasets from either SPSS or Stata, rather than the more elaborate functions available in `haven`.



## The 2017 British Social Attitudes Survey
For the rest of this guide, we will use the `British Social Attitudes Survey, 2017, Environment and Politics: Open Access Teaching Dataset`, which can be downloaded from the [UK Data Service website](https://beta.ukdataservice.ac.uk/datacatalogue/studies/study?id=8849). We will use  the   SPSS version of the dataset, which will be assumed to be  saved in a `UKDS` folder created inside `Documents` folder. `C:\\Users\\Your_User_Name_Here\\Documents` We will  set this as default working directory. This way, we won’t have to specify the full path of files that we will be opening or saving.  


We can finally open the file:
























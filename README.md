# review_localcovid19now

Review of localcovid19now

 * JOSS Issue: https://github.com/openjournals/joss-reviews/issues/4791
 * Repo: https://github.com/sjbeckett/localcovid19now
 * Paper: https://github.com/sjbeckett/localcovid19now/blob/main/paper/paper.md
 * Preprint as PDF: https://osf.io/fg6vw/

## Paper

First and foremost, I think the authors did an excellent job in collecting all
information about COVID prevalance! I think the package is useful and relevant.

However, when only running the examples both `README.md`
and the code examples, there are plenty of needless warnings.
Similar to having spelling errors in an academic manuscript,
this comes accross as needlessly sloppy.
Also, not using a uniform coding standard is another such thing
to make the package come accross as needlessly 
sloppy (for example, `calc_risk`, `addNewGeoms` and `LoadAlgeria` each
follow a different naming convention).
Additionally, most (all?) examples are put into `dontrun` tags,
which is fine for fuction that take a long time, but this happens
for short functions as well. This gives the incorrect impression
that the authors do not want to have examples that are actually 
ran, and hence, checked (the `calc_risk` function is a good example)!
I encourage the authors to fix these things,
so that `localcovid19now` makes an even better impression,
as I feel they did important work that should not be underappreciated.

### [Review checklist](https://raw.githubusercontent.com/openjournals/joss/main/docs/review_checklist.md)

### Conflict of interest

 * [x] I confirm that I have read the 
   [JOSS conflict of interest policy](reviewer_guidelines.html#joss-conflict-of-interest-policy) 
   and that: I have no COIs with reviewing this work or 
   that any perceived COIs have been waived by JOSS for the purpose of this review.

### Code of Conduct

 * I confirm that I read and will adhere to the [JOSS code of conduct](https://joss.theoj.org/about#code_of_conduct).

### General checks

- [x] **Repository:** Is the source code for this software available at the <a target="_blank" href="https://github.com/DistrictDataLabs/yellowbrick">repository url</a>?

Yes

- **License:** Does the repository contain a plain-text LICENSE file with the contents of an [OSI approved](https://opensource.org/licenses/alphabetical) software license?

Yes, an MIT license

- [x] **Contribution and authorship:** Has the submitting author made major contributions to the software? Does the full list of paper authors seem appropriate and complete?

Yes, the submitting author made major contributions to the software.

**Unsure** if the full list of paper authors is appropriate and complete:
Below I made a table from the author list and the GitHub Contributor
list at [https://github.com/sjbeckett/localcovid19now/graphs/contributors](https://github.com/sjbeckett/localcovid19now/graphs/contributors).
From that I conclude:
 * I am sure the submitting author is a major contributor.
   It seems both Beckett and Brandel-Tanis are the two prime contributors.
 * I am unsure if 'All authors have significantly contributed to the research'.
    * I do not understand that Johnson is not an author and Guyen is,
      as Johnson made more commits (6 versus 2), added more lines (12330 versus 96)
      and deleted more lines (975 versus 2), but as she is mentioned in the
      Acknowledgements, I assume she chose to do something else.
    * I would enjoy to see any proof or a statement of the contributions of 
      Rishishwar, Andris and Weitz. I find them under the 'aut' role in
      DESCRIPTION, but I see no commits by any of them. This makes
      me assume they have been involved more into funding and supervision.
      I would enjoy to find
      a 'Contribution' section describing the role of the authors
      with a possible update of the roles in DESCRIPTION

Name         |Author |Contributor
-------------|-------|-----------
Beckett      |Yes    |Yes
Brandel-Tanis|Yes    |Yes
Chande       |Yes    |Yes
Johnson      |No [1] |Yes
Guyen        |Yes    |Yes
Rishishwar   |Yes    |No
Andris       |Yes    |No
Weitz        |Yes    |No

 * [1] Johnson is mentioned in the Acknowledgements

### Functionality

- **Installation:** Does installation proceed as outlined in the documentation?

Yes

- **Functionality:** Have the functional claims of the software been confirmed?

Loading the Phillipines dataset on its own, after authentication, fails:

```
> googledrive::drive_auth(email = TRUE)
> Philippines <- LoadPhilippines()
Error in `gargle::response_process()`:
! Client error: (403) Forbidden
Insufficient Permission: Request had insufficient authentication scopes.
• domain: global
• reason: insufficientPermissions
• message: Insufficient Permission: Request had insufficient authentication scopes.
Run `rlang::last_error()` to see where the error occurred.
```

However, the Phillipes can be loaded by using `r LoadCountries`:

```
> GLOBALMAP <- LoadCountries()

 LoadPhilippines 

 LoadAlgeria 

 LoadAustralia 
```

- **Performance:** If there are any performance claims of the software, have they been confirmed? (If there are no claims, please check off this item.)

NA

### Documentation

- **A statement of need:** Do the authors clearly state what problems the software is designed to solve and who the target audience is?

The authors clearly state what the package does.

The authors do not state the intended audience.

- **Installation instructions:** Is there a clearly-stated list of dependencies? Ideally these should be handled with an automated package management solution.

No and this is not needed: the installation installs all dependencies.

- **Example usage:** Do the authors include examples of how to use the software (ideally to solve real-world analysis problems).

When running the code in `README.md`, one gets as needless warning:

```
> Malaysia <- LoadMalaysia()
Rows: 16096 Columns: 25                                                                 
── Column specification ──────────────────────────────────────────────────────────────────
Delimiter: ","
chr   (1): state
dbl  (23): cases_new, cases_import, cases_recovered, cases_active, cases_cluster, case...
date  (1): date

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

If `r googledrive::drive_auth(email = TRUE)` is not run, then, indeed, `r Philippines <- LoadPhilippines()` fails.
However, also `r GLOBALMAP <- LoadCountries()` fails if `r googledrive::drive_auth(email = TRUE)` is not run.
I would enjoy to see this documented as such:

```r
if (has_credentials()) {
  Philippines <- LoadPhilippines()
  GLOBALMAP <- LoadCountries()
} else {
  message(
    "You need to have Google Drive credientials ",
    "to use 'Philippines' and 'GLOBALMAP'. ",
    "To authenticate, use:",
    "",
    "'googledrive::drive_auth(email = TRUE)'"
  )
}
```

Running `PerCapitaMap_leaflet` on `US` gives a needless warning:

```
> PerCapitaMap_leaflet(US,100000)
Warning message:
In pal(percapcases) :
  Some values were outside the color scale and will be treated as NA
```

Running `PerCapitaMap_tmap` on `US` gives a needless warning:

```
> PerCapitaMap_tmap(US,100000)
Variable(s) "percapcases" contains positive and negative values, so midpoint is set to 0. Set midpoint = NA to show the full spectrum of the color palette.
Warning message:
Values have found that are less than the lowest break 
```

Running this line fails:

```
MAP = EventMap_tmap(US,100,US$AB,projection="ESPG:5070")
Error in CPL_transform(x, crs, aoi, pipeline, reverse, desired_accuracy, : 
crs not found: is it missing?
```

Running `create_c19r_data` gives needless output:

```
> create_c19r_data(df_in = US, asc_bias_list = cbind(AB4 = US$AB))
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
Joining, by = "geoid"
```

Additionally, the `README.md` has a needlessly clumsy construct:

```r
GLOBALMAP <- LoadCountries()
GLOBALMAP <- tidy_Data(GLOBALMAP) 
```

I see no point to bother a user to call `tidy_Data`. Instead, I'd encourage
either that the `LoadCountries` function calls `tidy_Data` in its final setup,
or that other functions such as `PerCapitaMap_leaflet` 
detect if the data data needs to be tidied and do so if needed.

#### Regular functions

`LoadNetherlands` gives needless output:

```
> Netherlands <- LoadNetherlands()
Reading layer `OGRGeoJSON' from data source 
  `https://geodata.nationaalgeoregister.nl/cbsgebiedsindelingen/wfs?request=GetFeature&service=WFS&version=2.0.0&typeName=cbs_gemeente_2022_gegeneraliseerd&outputFormat=json' 
  using driver `GeoJSON'
Simple feature collection with 345 features and 5 fields
Geometry type: MULTIPOLYGON
Dimension:     XY
Bounding box:  xmin: 13565.4 ymin: 306846.2 xmax: 278026.1 ymax: 619352.4
Projected CRS: Amersfoort / RD New
Rows: 143964 Columns: 12                                                                
── Column specification ──────────────────────────────────────────────────────────────────
Delimiter: ";"
chr  (7): Municipality_code, Municipality_name, Province, Security_region_code, Securi...
dbl  (3): Version, Total_reported, Deceased
dttm (1): Date_of_report
date (1): Date_of_publication

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

`LoadSweden` gives needless output:

```
> Sweden <- LoadSweden()
trying URL 'https://fohm.maps.arcgis.com/sharing/rest/content/items/b5e7488e117749c19881cce45db13f7e/data'
Content type 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet' length 2865276 bytes (2.7 MB)
==================================================
downloaded 2.7 MB
```

The example `moveFiles` creates and moves a file in the user's filesystem,
without deleting it. This would go against CRAN guidelines, as it comes
across as needlessly ignorant of the user (creating useless new files, that is).
I encourage the authors to deleted the moved file.

Note that `moveFiles` has an unclear name (`moveProcessedFiles` already seems better) 
and does overwrite files if these are at the target location. I encourage the
authors to give an error if there is a file at the target folder that is to
be overwritten.

Additionally, what does a function like `moveFiles` do in a file called `addNewGeom`?
I encourage the authors to either put it into a files called `MoveFiles.R`
or `FileUtils.R`.

`addNewGeoms` has an example that is `dontrun` for some reason. Running it
takes no time at all and it does not seem to do anything. I would enjoy
to see an example of `addNewGeoms` that actually does something.

`resetNewGeoms` does something that seems to not take time, yet it is
in `dontrun`. I am unsure what it does, but whatever it does, it can
just be run. I encourage the authors to remove the `dontrun`.

The `calc_risk` function has an example function with needless `dontrun`
and -probably due to that- a typo in the call to the function:

```r
#' @examples
#' \dontrun{
#' risk <- calcrisk(.001, 50)
#' }
#'
```

I suggest to remove the `dontrun` and call the function with the correct name.

The example from `create_c19r_data` (except for the needless warnings)
does not convey what it does by its return type. As it creates a CSV file,
I would encourage the authors to either return the CSV filename or the
content of the CSV table.

The example of `estRisk` is needlessly put into `dontrun`. 

The examples of `EventMap_leaflet` and `EventMap_tmap` 
give an error that does not help
the user to find the problem:

```r
> Austria <- LoadAustria()
Error in open.connection(3L, "rb") : 
error:0A00018A:SSL routines::dh key too small
```

Neither `PerCapitaMap_leaflet` nor `PerCapitaMap_tmap` 
have an example. Please add one :-)

The `remSurplus` example seems to run in less than 1 second.
I suggest to remove the `dontrun` tag due to that.

I could not check `tidy_Data` example, as the first line gave en error (see
below). I encourage the authors to use an easier country to demonstrate
the `tidy_Data` function.

```r
> Philippines <- LoadPhilippines()
Auto-refreshing stale OAuth token.
Error in `gargle::response_process()`:
! Client error: (403) Forbidden
Insufficient Permission: Request had insufficient authentication scopes.
• domain: global
• reason: insufficientPermissions
• message: Insufficient Permission: Request had insufficient authentication scopes.
Run `rlang::last_error()` to see where the error occurred.
```


- **Functionality documentation:** Is the core functionality of the software documented to a satisfactory level (e.g., API method documentation)?

Yes.

- **Automated tests:** Are there automated tests or manual steps described so that the functionality of the software can be verified?

There are automated tests that test the package to some extent.

For example, the package is tested to be built.
Note that there are many notes/warnings that are ignored
in the error logs, e.g. the latest error log at https://github.com/sjbeckett/localcovid19now/actions/runs/3143906398/jobs/5109223012#step:5:304 (needs a GitHub login)
has 4 notes. This comes across as needlessly ignorant and I encourage 
the authors to fix all these.

The main functionality is, however, not tested.

It is understandable that the main functionality is not
tested in the code examples in the documentation:
these take too long (CRAN uses 5 secs as the definition of 'too long').

However, I would expect another GitHub Actions script that

 * Loads all countries that do not need a Google Authentication
 * Creates a PNG file with a world map of COVID densities
   * using both Leaflet and TMap

I do not expect tests about actually using Leaflet or TMap's user interfaces,
nor using the data behind the Google Authentication.

But creating an image for easily accessible countries seems the core 
functionality to me. Put that in a simple R script and add it to the tests.

- **Community guidelines:** Are there clear guidelines for third parties wishing to 1) Contribute to the software 2) Report issues or problems with the software 3) Seek support

Yes.

### Software paper

- **Summary:** Has a clear description of the high-level functionality and purpose of the software for a diverse, non-specialist audience been provided?

Yes, I think a diverse audience can understand what the package does.

- **A statement of need:** Does the paper have a section titled 'Statement of need' that clearly states what problems the software is designed to solve, who the target audience is, and its relation to other work?

 * [x] what problems the software is designed to solve, 

Yes

 * [x] who the target audience is, and 

**No**, not explicitly. Just add it :-)

 * [x] its relation to other work?

Yes.

- **State of the field:** Do the authors describe how this software compares to other commonly-used packages?

Yes.

- **Quality of writing:** Is the paper well written (i.e., it does not require editing for structure, language, or writing quality)?

Yes, I would agree to accept it as-is. Good job!

As a minor note, I would enjoy to see pictures in the paper. 
`localcovid19now` is about putting the spread of COVID-19 into pretty maps.
I would strongly expect at least one such picture!

- **References:** Is the list of references complete, and is everything cited appropriately that should be cited (e.g., papers, datasets, software)? Do references in the text use the proper [citation syntax]( https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html#citation_syntax)?

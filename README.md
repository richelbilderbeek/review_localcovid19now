# review_localcovid19now

Review of localcovid19now

 * JOSS Issue: https://github.com/openjournals/joss-reviews/issues/4791
 * Repo: https://github.com/sjbeckett/localcovid19now
 * Paper: https://github.com/sjbeckett/localcovid19now/blob/main/paper/paper.md
 * Preprint as PDF: https://osf.io/fg6vw/

## Paper

 * [ ] I really miss a picture

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



- **Performance:** If there are any performance claims of the software, have they been confirmed? (If there are no claims, please check off this item.)

### Documentation

- **A statement of need:** Do the authors clearly state what problems the software is designed to solve and who the target audience is?

The authors clearly state what the package does.

The authors do not state the intended audience.

- **Installation instructions:** Is there a clearly-stated list of dependencies? Ideally these should be handled with an automated package management solution.

No and this is not needed: the installation installs all dependencies.

- **Example usage:** Do the authors include examples of how to use the software (ideally to solve real-world analysis problems).

When running the code in README.md, one gets as needless warning:

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


- **Functionality documentation:** Is the core functionality of the software documented to a satisfactory level (e.g., API method documentation)?

Running the examples creates files within the package, e.g. `tools/processed/testFile.R`

- **Automated tests:** Are there automated tests or manual steps described so that the functionality of the software can be verified?

- **Community guidelines:** Are there clear guidelines for third parties wishing to 1) Contribute to the software 2) Report issues or problems with the software 3) Seek support

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

- **Quality of writing:** Is the paper well written (i.e., it does not require editing for structure, language, or writing quality)?



- **References:** Is the list of references complete, and is everything cited appropriately that should be cited (e.g., papers, datasets, software)? Do references in the text use the proper [citation syntax]( https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html#citation_syntax)?

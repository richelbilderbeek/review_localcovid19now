# review_localcovid19now

Review of localcovid19now

 * JOSS Issue: https://github.com/openjournals/joss-reviews/issues/4791
 * Repo: https://github.com/sjbeckett/localcovid19now
 * Paper: https://github.com/sjbeckett/localcovid19now/blob/main/paper/paper.md
 * Preprint as PDF: https://osf.io/fg6vw/

## Paper

 * [ ] I really miss a picture

### [Review checklist](https://raw.githubusercontent.com/openjournals/joss/main/docs/review_checklist.md)
================

### Conflict of interest

 * [x] I confirm that I have read the 
   [JOSS conflict of interest policy](reviewer_guidelines.html#joss-conflict-of-interest-policy) 
   and that: I have no COIs with reviewing this work or 
   that any perceived COIs have been waived by JOSS for the purpose of this review.

### Code of Conduct

 * I confirm that I read and will adhere to the [JOSS code of conduct](https://joss.theoj.org/about#code_of_conduct).


 * Contribution.
   Below I made a table from the author list and the GitHub Contributor
   list at https://github.com/sjbeckett/localcovid19now/graphs/contributors .
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


### General checks

- [x] **Repository:** Is the source code for this software available at the <a target="_blank" href="https://github.com/DistrictDataLabs/yellowbrick">repository url</a>?

Yes

- **License:** Does the repository contain a plain-text LICENSE file with the contents of an [OSI approved](https://opensource.org/licenses/alphabetical) software license?
- **Contribution and authorship:** Has the submitting author made major contributions to the software? Does the full list of paper authors seem appropriate and complete?

### Functionality

- **Installation:** Does installation proceed as outlined in the documentation?
- **Functionality:** Have the functional claims of the software been confirmed?
- **Performance:** If there are any performance claims of the software, have they been confirmed? (If there are no claims, please check off this item.)

### Documentation

- **A statement of need:** Do the authors clearly state what problems the software is designed to solve and who the target audience is?
- **Installation instructions:** Is there a clearly-stated list of dependencies? Ideally these should be handled with an automated package management solution.
- **Example usage:** Do the authors include examples of how to use the software (ideally to solve real-world analysis problems).
- **Functionality documentation:** Is the core functionality of the software documented to a satisfactory level (e.g., API method documentation)?
- **Automated tests:** Are there automated tests or manual steps described so that the functionality of the software can be verified?
- **Community guidelines:** Are there clear guidelines for third parties wishing to 1) Contribute to the software 2) Report issues or problems with the software 3) Seek support

### Software paper

- **Summary:** Has a clear description of the high-level functionality and purpose of the software for a diverse, non-specialist audience been provided?
- **A statement of need:** Does the paper have a section titled 'Statement of need' that clearly states what problems the software is designed to solve, who the target audience is, and its relation to other work?
- **State of the field:** Do the authors describe how this software compares to other commonly-used packages?
- **Quality of writing:** Is the paper well written (i.e., it does not require editing for structure, language, or writing quality)?
- **References:** Is the list of references complete, and is everything cited appropriately that should be cited (e.g., papers, datasets, software)? Do references in the text use the proper [citation syntax]( https://rmarkdown.rstudio.com/authoring_bibliographies_and_citations.html#citation_syntax)?

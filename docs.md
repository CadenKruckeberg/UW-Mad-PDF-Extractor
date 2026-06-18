# Output Issues Acknowledgement

Parsing the DIR Reports seldom presents issues. Parsing the Grades Reports is not the same:

### Impurities in the PDFs

* `1032-grades.pdf` has major errors in the Section column throughout the entire PDF

* `1164-grades.pdf` has odd "#Error" values on pages 419, 423, and 425. None of these issues are in the extracted results, though.

* `1224-dir.pdf` splits an instructor's name over pages 527 and 528

* `1232-grades.pdf` has odd "#Type!" error-looking values on pages 395, 436, and 440. None of these issues are in the extracted results, though.

* Several grades reports have unlabelled rows above the Freshman row in the summary section. None of these issues are in the extracted results, though.

### pdfplumber limitation

* pdfplumber automatically converts two consecutive spaces into just one space, inaccurately (but maybe fortunately) extracting some instructor names in DIR reports

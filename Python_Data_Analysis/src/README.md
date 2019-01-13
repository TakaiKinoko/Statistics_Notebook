## survey.py -- structure

* Record class 
    * subclasses:
        * Respondent -- empty (no init)
        * Pregnant -- empty (no init)
    * use: 
        ```
        Table.MakeRecord(text)      # convert a line of text into a record object
        ```

* Table class
    * subclasses:
        * Respondents 
        * Pregnancies

* **recodes** v.s. **raw data**
    * most of the variables returned from **GetFields** are recodes, which means that they are not part of the raw data collected by the survey, but they are calculated using the raw data.
        * e.g. *prglength* for live births is equal to the raw variable wksgest (weeks of gestation) if it is available; otherwise it is estimated using mosgest * 4.33
    * Recodes are often based on logic that checks the consistency and accuracy of the data. In general it is **a good idea to use recodes** unless there is a compelling reason to process the raw data yourself.
        * Pregnancies has a method called Recode that does some additional checking and recoding
        

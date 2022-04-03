# Note

This is a research question as part of the MSR course 2021/22 at UniKo, CS department, SoftLang Team

# Names of team/students

- Team: Golf
- Members:  
   Rahul Narayandas Chhabadiya (rchhabadiya@uni-koblenz.de)  
   Uthara Ramanandan Kottaypilaprathodi (ukottaypilap@uni-koblenz.de )

# Baseline study:

- ### Research Question based on the exisiting project:

   Can we predict (non-) implication probabilistically by using just POM dependencies?

- ### Existing method:

   - This method is used on respositories
   - To find dependencies that are likely candidates for mixed API usage  
   - The dependency/pair occurence proportion is computed for   both dependencies by
      
      P(A, B) =  # occurrences of dependency A and B / # occurrences of dependency A

   
- ### Approach:
  - We propose to apply a causality function.
  - In this approach, pom files are being used not the repositories.
  - P(e|i) = probability of an API e given API i in a pom file.
   
      -Equation: 
         Δ*Pe given i = P(e|i) - P(e)/ P(¬i^¬e)
  
      - where ΔPei=P(e|i)-P(e)>0
   

        

# Findings of research question

- ### Process delta:
   - The original work was done on repositories while in this research question only pom files have been used which is already part of main research question.
   - Dependencies usage count is stored in the csv file "repositories_with_dependencies.csv" and it contains data for the table 'Table 4.4: The top dependencies (Dependency) with the number of repositories that declare them (Count)' of the original thesis.
   - Dependency pair usage is stored in the csv file "dependencies_pairs_counted.csv" and it contains data for table 'Table 4.5: The dependency pairs' of the original thesis.
  
- ### Output delta:
  - In the original work >3k repositories have been used while in our case POM files have been used. So although the results are not identical they are proportional and confirm the findings from the original work.
  - We are trying to get result of data table 4.5 from the thesis from using only pom file where Delta of P is greater than 0.6 for both dependencies.
  - In our output the results are different because we only used POM files instead of using repositories.
  - Dependency pair usages were counted for both side of dependencies accordingly. In the first CSV file Delta P is counted as P of e given i, in the second CSV file Delta P is counted as P of i given e.
  - Dependencies we found in the result are not in the main result.


# Implementation of replication:


- ### Hardware requirements:
    - OS: Windows, Linux or MacOS
    - Memory: 4 GB RAM recommended

- ### Software requirements
  - Python (we used python v3.7.0)
  - python packages - numpy, findspark


- ## Data:
- ### Input data:
    - Java project repo with Maven from Github
      - POM files  
      - POM file in XML format and named pom.xml  (stored in pomfiles directory)

- ### Output data:
   - The output is stored in two different CSV files data_prediction1.csv & data_prediction2.csv.  
   - data_prediction1.csv -> Statistics about dependency pairs used in the repositories where Delta P e given i. 
   - data_prediction2.csv -> Statistics about dependency pairs used in the repositories where Delta P i given e.

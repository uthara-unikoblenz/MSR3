# Note

This repository contains the enhancement conducted as part of the MSR course 2021/22 at UniKo, CS department, SoftLang Team to the code underlying the master thesis "Applying API Categories to the Abstractions Using APIs" (2021) written by Katharina Gorjatschev

# Names of team/students

- Team: Golf
- Members:  
   Rahul Narayandas Chhabadiya (rchhabadiya@uni-koblenz.de)  
   Uthara Ramanandan Kottaypilaprathodi (ukottaypilap@uni-koblenz.de )

# Baseline study:

- ### Aspect of the enhancement project:

   Research Question: Can we predict (non-) implication probabilistically by using just POM dependencies?
   
      -Is there a way to derive POM(A => B)
      -How can the effect of popular APIs (eg: JUnit) be mitigated 
 
# Findings of the enhancement

- ### Process delta:
   - Only analyses POM files to derive possible mixed API usage. Does not parse repositories.   
   - Applies two methods to arrive at possible mixed API usage   
      1. **Applying causality function**: a probability based approach to derive “imply’ relationships among APIs by only analysing POM files 
       
          P(e|i) = probability of an API e given API i in a pom file. 
         
         ![img](https://latex.codecogs.com/svg.latex?%5CDelta%20P%5Ee_i%3D%5Cfrac%7BP%28e%7Ci%29-P%28e%7C%5Crightharpoondown%20i%29%7D%7B1-P%28e%7C%5Crightharpoondown%20i%29%7D)     
         
         where ![img](https://latex.codecogs.com/svg.latex?P%28e%7Ci%29-P%28e%7C%5Crightharpoondown%20i%29%3E%200)         
      2. **Applying causality function along with occurrence proportion**
      
          The dependency/pair occurence proportion is computed for both dependencies by
          
          P(A, B) =  ![img](https://latex.codecogs.com/svg.latex?%5Cfrac%7Boccurrences%5Chspace%7B.3em%7Dof%5Chspace%7B.3em%7D%20dependency%5Chspace%7B.3em%7D%20A%5Chspace%7B.3em%7D%20and%5Chspace%7B.3em%7D%20B%7D%7Boccurrences%5Chspace%7B.3em%7D%20of%5Chspace%7B.3em%7D%20dependency%5Chspace%7B.3em%7D%20A%7D)
      3. **Involved files**
      
          dependencies_counter.py
    

      
  
- ### Output delta:
  - Comparing the results of this enhancement with Delta_P > 0.6  with the results from the original thesis namely table 4.7 and 4.14 we find
  - Most of the API pairs ranked high with occurrence proportion also rank high with Delta_P
  - Various API pairs ranked high in Delta_P does not show any actual mixed usage
  - API’s chosen for final analysis in [Gorjateschev] after applying manual verification naturally doesn’t score high in Delta_P values as only POM files were used



# Implementation of replication:


- ### Hardware requirements:
    - OS: Windows, Linux or MacOS
    - Memory: 4 GB RAM recommended

- ### Software requirements
  - Python (we used python v3.7.0)
  - python packages - numpy, findspark


- ### Data:

  - #### Input data:  
          POM file in XML format and named pom.xml collected from 
          Java projects with Maven 
          Only considering Repositories that have
          At least 100 stars,
          At least 100 commits
          At least two contributors
          At least one source directory src/main/java

   - #### Output data:
            Two csv files generated as a result of applying the causality function 
            data_prediction.csv (without the use of occurrence proportion)
            data_prediction_without_proportion_filtering (with the use of occurrence proportion)

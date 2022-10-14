# Readings in Differential Privacy

A list of papers and materialies for understanding differential privacy (DP) and its applications to real-world systems. 

## Introduction to Differential Privacy

- [Protecting Privacy with MATH (Collab with the US Census Bereau)](https://www.youtube.com/watch?v=pT19VwBAqKA) A very illustrative 12-minute video that shows how the database reconstruction attack (DRA) works and how differential privacy can be used for preventing such attacks.
- [Differential Privacy: A Primer for a Non-Technical Audience](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3338027) (2019) A good introduction for understanding the overall concepts and motivation behind the differential privacy. 
- [Programming Differential Privacy](https://programming-dp.com/index.html) A short-online textbook good for learning the core concepts and theory around differential privacy. This book is from one of the authors of the CHORUS DP SQL engine work.
- [A friendly, non-technical introduction to differential privacy](https://desfontain.es/privacy/friendly-intro-to-differential-privacy.html) (2021) A series of blog posts that illustrate the theory and practice of differential privacy in a succinct manner.
- [Differential Privacy: The Pursuite of Protections by Default](https://dl.acm.org/doi/abs/10.1145/3434228). (2021) (_A free online version of the article is also available at [acmqueue](https://queue.acm.org/detail.cfm?id=3439229)_). The authors of Google's DP SQL engine shared their learnings when applying differential privacy to the real world applications. Especially, they pointed out that bounding user-contributions, which is essential for computing sensitivity to adjust the amount of noise, was missing in the past studies.

### Lecures and Tutorials

- Differential Privacy in the Wild. [Part 1](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-1.pdf), [Part 2](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-2.pdf) (SIGMOD 2017 Tutorial)
- [Lecture Notes: Applied Privacy for Data Science](https://opendp.github.io/cs208/spring2022/) (Harvard University, 2020) 

## Keywords 

Here is a list of keywords specific to literatures in the differential privacy area. You need to be familiar with these keywords, because they are often used without any explanations:

- _Mechanism_
  - A mechanism refers to a computation process (e.g., query processing) in the context of differential privacy. Differential privacy is a property of the data processing process (mechanism), which usually applyies noise to the result, as opposed to the property of the data itself (e.g., [k-anonymity](https://programming-dp.com/notebooks/ch2.html) is a property of the data).
- _Neighbour Databases_
  - A set of all possible databases where only the records from a single individual person (privacy unit) differ. Differential privacy protectes the privacy of indivdiaul userr by producing almost the same query results regardless the presence or absence of individual users in the database. Considering all neighbour databases is the core concept of differential privacy.
- _Sensitivity_
  - A sensitivity is the amount of the output value difference of a function when records from a single person change. For example, the senstivity of `COUNT(*)` SQL query is 1 because presence or absence of a single record can change the value of `COUNT(*)` at most 1. This sensitivy is used for scaling the amount of Laplace/Gaussian noise.
- _User Contribution_
  - The number of records a single user provides. For example, if a single user has multiple records, say at most N, in the database, the sensitivy of `COUNT(*)` becomes N. 
- _Local Differential Privacy_
  - A method applying noise to the source data.
- _Global Differential Privacy_
  - A method applying noise to the query results.


## Differentially Private SQL Engines (Global Differential Privacy)

- [Differentially Private SQL with Bounded User Contribution](https://arxiv.org/abs/1909.01917) (2019). A comprehensive design and overview of Google's DP SQL engine. The privacy policy enforcment described in this paper is apparently applied to their [Google Ads Data Hub (ADH)](https://developers.google.com/ads-data-hub/guides/privacy-checks) service as well.
  - To restrict the number of maximum user-contributions to different partitions, it applies a randomized [reservoir sampling](https://dl.acm.org/doi/10.1145/3147.3165) (1985) method while scanning records from tables.  
  - The idea of thresholding groups represented by small number of people was originally proposed in [Releasing search queries and clicks privately
](https://dx.doi.org/10.1145/1526709.1526733) (2009)
- [CHORUS: a Programming Framework for Building Scalable Differential Privacy Mechanisms](https://ieeexplore.ieee.org/document/9230409) (Euro S&P 2020). An [open-source implementation of DP SQL engine written in Scala](https://github.com/uvm-plaid/chorus). This is a DBMS-independent approach for building DP SQL engines, which rewrites SQL queries and applies noise to the results as a post process.
- [LinkedIn's Audience Engagements API: A Privacy Preserving Data Analytics System at Scale](https://arxiv.org/abs/2002.05839) (2020) Following the same direction with CHORUS, LinkedIn implemented a DP SQL engine over their real-time SQL engine Pinot without changing the DBMS itself. It also has a privacy budget management sub-system. 
- [PrivateSQL: A Differentially Private SQL Query Engine](https://dl.acm.org/doi/10.14778/3342263.3342274) (2019) An early prototype to apply diffrential privacy to SQL processing. Although only `COUNT(*)` queries are supported, this work formalized join processing between multiple privacy tables (primary/secondary privacy relations) and developed a method to split privacy budget within pre-defined workloads.
- [Calibrating Noise to Sensitivity in Private Data Analysis](https://journalprivacyconfidentiality.org/index.php/jpc/article/view/405) (2017) A proof for a mechanism adding Laplace noise scaled with (sensitivity)/ε satisfies ε-differential privacy.
- [R2T: Instance-optimal Truncation for Differentially Private Query Evaluation with Foreign Keys](https://dl.acm.org/doi/10.1145/3514221.3517844) (SIGMOD 2022 Best Paper) Extending the application of differential privacy to more complex joins by considerfing join-graph structure patterns. Note: group-by queries are not covered in this work.  

## Local Differential Privacy

- [Local vs. central differential privacy](https://desfontain.es/privacy/local-global-differential-privacy.html) (2019) Explaining the differences between Local differential privacy (applying noise to the data) and Global differential privacy (applying noise to the query result). Middle-ground approaches betweem Local and Global DP have also been studied. 
- [RAPPOR: Randomized Aggregatable Privacy-Preserving Ordinal Response](https://arxiv.org/abs/1407.6981) (2014)
- [Prochlo: Strong Privacy for Analytics in the Crowd](https://arxiv.org/abs/1710.00901) (2017)
- [The Privacy Blanket of the Shuffle Model](https://arxiv.org/abs/1903.02837) (2019) 


## Differential Privacy in Practice

- [A list of real-world uses of differential privacy](https://desfontain.es/privacy/real-world-differential-privacy.html) (2021). How the big tech companies, including Apple, Google, Facebook (Meta), LinkedIn, Microsoft, etc., applies differential privacy. 
- [Understanding Database Reconstruction Attacks on Public Data: These attacks on statistical databases are no longer a theoretical danger](https://dl.acm.org/doi/10.1145/3291276.3295691) (2018) The 2010 US Census used the notion of k-anonymity and nullified part of table cells for hiding too specific data. However, [researchers simulated a database reconstruction attack (DRA) against the 2010 US Census data](https://www.census.gov/data/academy/webinars/2021/disclosure-avoidance-series/simulated-reconstruction-abetted-re-identification-attack-on-the-2010-census.html) could successfully recover 46% of the original individual records, including the sex, age, race, ethnicity, and fine-grained geographic locations. If allowing errors within one year, it could reconstruct 71% of US population data (219 million records!).
- [Understanding the 2020 Census Disclosure Avoidance System](https://www2.census.gov/about/training-workshops/2021/2021-07-01-das-presentation.pdf) From the learning of the 2010 US Census, the 2020 version of US Census data has applied differential privacy technology to anonymize the published statistics with noise. 
  - [Issues Encountered Deploying Differential Privacy](https://arxiv.org/abs/1809.02201) (2018) Describes lessons learned while introducing differential privacy to the 2020 US Census. There were many challenges unanticipated by differential privacy’s creators. For example, chosing a value of ε, explaining differntial privacy in academic languages was not acceptable to many of the data users, etc.
- [Google COVID-19 Community Mobility Reports: Anonymization Process Description (version 1.1)](https://arxiv.org/abs/2004.04145) (2020) Differential privacy techniques are used for anonymyzing and analyzing contact tracing data. 
  - A more background can be found in [Delivering a Rapid Digital Response to the COVID-19 Pandemic](https://cacm.acm.org/magazines/2022/1/257447-delivering-a-rapid-digital-response-to-the-covid-19-pandemic/abstract) (CACM 2022)


## Differential Privacy in Machine Learning

- [Differentially Private Machine Learning: Theory, Algorithms, and Applications](https://www.ece.rutgers.edu/~asarwate/nips2017/) (NIPS 2017 Tutorial)

## Security 

- [Side-Channel Attacks on Query-Based Data Anonymization](https://dl.acm.org/doi/10.1145/3460120.3484751) (2021) Even if the system satisfies differential privacy, there still is a way to find personal information without reading any query results. Side-channel attacks intentinally inject query errors (division by zero, overflow, etc.) or delays of query executions that happen when a specific condition matches. This paper shows such examples and provides ideas to avoid these side-channel attacks.
- [On significance of the least significant bits for differential privacy](https://dl.acm.org/doi/10.1145/2382196.2382264) (2012) Sampling from Laplace distribution suffers from insufficient resolution of floating-poing computations and damages DP gurantees. A practical approach for this problem is rounding the result after adding noise, but it sacrifices the utility of the result. Google's open-source DP library provides an alternative [secure noise generation](https://github.com/google/differential-privacy/blob/main/common_docs/Secure_Noise_Generation.pdf) method to lower the error. This approach can be applied to both the Laplace and Gaussian noise.

## Open-Source Libraries

- [Google Differential Privacy](https://github.com/google/differential-privacy) C++/Go/Java implementations of differential-privacy algorithms. It include code for adding Laplace/Gaussian noise, computing bounded aggregation, approximate bounding, etc.
- [OpenDP](https://github.com/opendp/opendp) A python library collection for differential privacy. 

## Companies Adopting Differential Privacy

- [Apple: Differential Privacy Overview](https://www.apple.com/privacy/docs/Differential_Privacy_Overview.pdf)
  - [Learning with Privacy at Scale](https://machinelearning.apple.com/research/learning-with-privacy-at-scale) (2017)
- [Google: How we're helping developers with differential privacy](https://developers.googleblog.com/2021/01/how-were-helping-developers-with-differential-privacy.html)
- [Micorosoft: AI Lab projects related to differential privacy](https://www.microsoft.com/en-us/ai/ai-lab-differential-privacy)
- [Tumult Labs](https://www.tmlt.io/)
- [Amazon: Differential Privacy](https://www.amazon.science/tag/differential-privacy)

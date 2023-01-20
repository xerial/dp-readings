# Readings in Differential Privacy

[Differential privacy (DP)](https://en.wikipedia.org/wiki/Differential_privacy) was invented in 2006 by C. Dwork, et al. Since then, a lot of scientific papers have been published in this area. Unfortunately, however, too many publications makes difficult for new-comers to understand its scientific terms (e.g., sensitivity, neighbour databases, etc.), implicit assumptions (how many user contributions in the database?), actual pros and cons when applying DP to the real-world systems. 

This page provides a curated list of papers and resources essential to understanding the concept of differential privacy, its history, and applications. If you think some important paper is missing in the list, please submit a pull request. 

## Introduction to Differential Privacy

- [Protecting Privacy with MATH (Collab with the US Census Bereau)](https://www.youtube.com/watch?v=pT19VwBAqKA) A very illustrative 12-minute video that shows how the database reconstruction attack (DRA) works and how differential privacy can prevent them.
- [A friendly, non-technical introduction to differential privacy](https://desfontain.es/privacy/friendly-intro-to-differential-privacy.html) (2021) A series of blog posts that illustrate the theory and practice of differential privacy.
- [Programming Differential Privacy](https://programming-dp.com/index.html) A short-online textbook, good for learning the core concepts and theories around differential privacy. This book is from one of the authors of the CHORUS DP SQL engine work.
- [Differential Privacy: A Primer for a Non-Technical Audience](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3338027) (2019) A good introduction for understanding the overall concepts and motivations behind the differential privacy without using too much mathmatics.
- [Differential Privacy: The Pursuite of Protections by Default](https://dl.acm.org/doi/abs/10.1145/3434228). (2021) (_A free online version of the article is also available at [acmqueue](https://queue.acm.org/detail.cfm?id=3439229)_). The authors of Google's DP SQL engine shared their learnings when applying differential privacy to the real world applications. Especially, they pointed out that bounding user-contributions, which is essential for properly computing sensitivity, was missing in the past studies.

### Lectures and Tutorials

- Differential Privacy in the Wild. [Part 1](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-1.pdf), [Part 2](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-2.pdf) (SIGMOD 2017 Tutorial)
- [Lecture Notes: Applied Privacy for Data Science](https://opendp.github.io/cs208/spring2022/) (Harvard University, 2020) 

### Keywords 

Here is a list of keywords specific to literatures in the differential privacy area. You need to be familiar with these keywords, because they are often used without any explanations:

- _Mechanism_
  - A mechanism refers to a computation process (e.g., query processing) in the context of differential privacy. Differential privacy is a property of the data processing process (mechanism), which usually applies noise to the result, as opposed to the property of the data itself (e.g., [k-anonymity](https://programming-dp.com/notebooks/ch2.html) is a property of the data).
- _Neighbour Databases_
  - A set of all possible databases where only the records from a single individual person (privacy unit) differ. Differential privacy protectes the privacy of indivdiaul userr by producing almost the same query results regardless the presence or absence of individual users in the database. Considering all neighbour databases is the core concept of differential privacy.
- _Sensitivity_
  - A sensitivity is the amount of the output value difference of a function when records from a single person change. For example, when a table contains at most one record per user, the senstivity of `COUNT(*)` SQL query becomes 1 because presence or absence of a single user record can change the value of `COUNT(*)` at most 1. This sensitivy is used for scaling the amount of Laplace/Gaussian noise.
- _User Contribution_
  - The number of records a single user provides. For example, if a single user has multiple records in the database, say at most N, the sensitivy of `COUNT(*)` becomes N. 
- _Local Differential Privacy_
  - A method applying noise to the source data.
- _Global (or Central) Differential Privacy_
  - A method applying noise to the query results. This is also called central differential privacy.

![image](https://user-images.githubusercontent.com/57538/213010982-3426bb08-f0cd-4739-9051-74537ad9c662.png)
(An image from [A SURVEY OF DIFFERENTIAL PRIVACY FRAMEWORKS
](https://blog.openmined.org/a-survey-of-differential-privacy-frameworks/))

## Academic Conferences

Papers on differential privacy often presented in these conferences. 

- [Privacy Enhancing Technologies Symposium (PETS)](https://petsymposium.org/)
  - [Presentation videos on YouTube](https://www.youtube.com/c/PrivacyEnhancingTechnologiesSymposium/videos)
- [TPDP - Theory and Practice of Differential Privacy](https://tpdp.journalprivacyconfidentiality.org/)
- [PEPR - USENIX Conference on Privacy Engineering Practice and Respect](https://www.usenix.org/conferences/byname/1046)
- Database Conferences
  - [SIGMOD](https://sigmod.org/)
  - [VLDB](https://www.vldb.org/)

## Differentially Private SQL Engines (Global Differential Privacy)

- [Differentially Private SQL with Bounded User Contribution](https://arxiv.org/abs/1909.01917) (2019). A comprehensive design and overview of Google's DP SQL engine, which takes into account the user-level differential privacy when a user have multiple log records in the database. The privacy policy enforcment scheme described in this paper is partially applied to their [Google Ads Data Hub (ADH)](https://developers.google.com/ads-data-hub/guides/privacy-checks) service too.
  - For restricting the number of maximum user-contributions to different partitions, it applies a randomized [reservoir sampling](https://dl.acm.org/doi/10.1145/3147.3165) (1985) method while scanning records from tables.  
  - The idea of aggrgation thresholding was originally proposed in [Releasing search queries and clicks privately
](https://dx.doi.org/10.1145/1526709.1526733) (2009)
- [Differential Privacy for Databases](https://dpfordb.github.io/dpfordb.pdf) (2021) An overview of differential privacy techniques for answering database queries. This book was written by the authors of CHORUS work. 
- [CHORUS: a Programming Framework for Building Scalable Differential Privacy Mechanisms](https://ieeexplore.ieee.org/document/9230409) (Euro S&P 2020). An [open-source implementation of DP SQL engine written in Scala](https://github.com/uvm-plaid/chorus). A DBMS-independent approach for building DP SQL engines, which rewrites SQL queries and applies noise to the query results as a post process.
- [PrivateSQL: A Differentially Private SQL Query Engine](https://dl.acm.org/doi/10.14778/3342263.3342274) (2019) An early prototype of a diffrentially private SQL engine, which utilizes differential-private views (called private synopsys) extracted from a pre-defined workload. In this papar, only `COUNT(*)` queries is supported, but extending this approache to other types of SQL operators should be possible.
- [Calibrating Noise to Sensitivity in Private Data Analysis](https://journalprivacyconfidentiality.org/index.php/jpc/article/view/405) (2017) A proof for a mechanism that adds Laplace noise scaled with (sensitivity)/ε satisfies ε-differential privacy.
- [R2T: Instance-optimal Truncation for Differentially Private Query Evaluation with Foreign Keys](https://dl.acm.org/doi/10.1145/3514221.3517844) (SIGMOD 2022 Best Paper) Extending the application of differential privacy to more complex joins by considerfing join-graph structure patterns. Note: group-by aggregations are not covered in this work.  

## Privacy Budget Management

- [LinkedIn's Audience Engagements API: A Privacy Preserving Data Analytics System at Scale](https://arxiv.org/abs/2002.05839) (2020) LinkedIn implemented a DP SQL engine and privacy budget management system over their real-time SQL engine Pinot without changing the internals of the DBMS. This paper discusses on what situations using higher privacy budget is acceptable.
- [Visualizing Privacy-Utility Trade-Offs in Differentially Private Data Releases](https://arxiv.org/abs/2201.05964) (2022) Visualizing privacy and utility tradeoffs. The authors also published a [blog post](https://medium.com/multiple-views-visualization-research-explained/visualizing-the-accuracy-privacy-trade-off-to-improve-budget-decisions-with-differential-privacy-66fc3efb34a) about this work. ![image](https://user-images.githubusercontent.com/57538/199791892-a29f65d6-245e-4618-803d-172c8f2acdb0.png)
- [Negotiating Privacy/Utility Trade-Offs under Differential Privacy](https://www.usenix.org/conference/pepr22/presentation/miklau) (2022) It explains the complexity of making choices about privacy/utility trade-offs in details.


## Local Differential Privacy

- [Local vs. central differential privacy](https://desfontain.es/privacy/local-global-differential-privacy.html) (2019) Explaining the differences between Local differential privacy (applying noise to the data) and Global differential privacy (applying noise to the query result). Middle-ground approaches betweem Local and Global DP have also been studied. 
- [RAPPOR: Randomized Aggregatable Privacy-Preserving Ordinal Response](https://arxiv.org/abs/1407.6981) (2014)
- [Prochlo: Strong Privacy for Analytics in the Crowd](https://arxiv.org/abs/1710.00901) (2017)
- [Collecting Telemetry Data Privately](https://www.microsoft.com/en-us/research/publication/collecting-telemetry-data-privately/) (NIPS 2017) Microsoft used local differential privacy for collecting telemetry data in Windows.
- [The Privacy Blanket of the Shuffle Model](https://arxiv.org/abs/1903.02837) (2019) 

## Synthetic Data Generation

- [PrivBayes: Private Data Release via Bayesian Networks](https://dl.acm.org/doi/10.1145/3134428) (2017) A method for privacy-preserving data publishing that satisfies a DP guarantee.
- [Benchmarking Differentially Private Synthetic Data Generation Algorithms](https://arxiv.org/abs/2112.09238) (2022) Evaluating the utility of synthetic data generators. 
- [Winning the NIST Contest: A scalable and general approach to differentially private synthetic data](https://arxiv.org/abs/2108.04978) (2021) The marginal-based synthetic data generator, which marked the best score in the above benchmark paper. 
- [Differentially Private Marginals](https://github.com/microsoft/synthetic-data-showcase/blob/main/docs/dp/dp_marginals.pdf) (2022) A differentially private algoritm to output approximate k-way marginals of tabular data. This method is used for [Synthetic Data Showcase](https://github.com/microsoft/synthetic-data-showcase) project.

## Differential Privacy in Practice

- [A list of real-world uses of differential privacy](https://desfontain.es/privacy/real-world-differential-privacy.html) (2021). How the big tech companies, including Apple, Google, Facebook (Meta), LinkedIn, Microsoft, etc., applies differential privacy. 
- [Understanding Database Reconstruction Attacks on Public Data: These attacks on statistical databases are no longer a theoretical danger](https://dl.acm.org/doi/10.1145/3291276.3295691) (2018) The 2010 US Census used the notion of k-anonymity and nullified part of table cells for hiding too specific data. However, [researchers simulated a database reconstruction attack (DRA) against the 2010 US Census data](https://www.census.gov/data/academy/webinars/2021/disclosure-avoidance-series/simulated-reconstruction-abetted-re-identification-attack-on-the-2010-census.html) could successfully recover 46% of the original individual records, including the sex, age, race, ethnicity, and fine-grained geographic locations. If allowing errors within one year, it could reconstruct 71% of US population data (219 million presonal records!).
- [Understanding the 2020 Census Disclosure Avoidance System](https://www2.census.gov/about/training-workshops/2021/2021-07-01-das-presentation.pdf) From the learning of the 2010 US Census, the 2020 version of US Census data has applied differential privacy technology to anonymize the published statistics with noise. In the 2020 US Census, zero-concentrated CDP (zCDP) is used for applying Gaussian noise.
  - [Issues Encountered Deploying Differential Privacy](https://arxiv.org/abs/1809.02201) (2018) Describes lessons learned while introducing differential privacy to the 2020 US Census. There were many challenges unanticipated by differential privacy’s creators. For example, chosing a value of ε can be a political problem. And also, explaining differntial privacy in academic languages was not acceptable to many of the data users, etc.
- [Google COVID-19 Community Mobility Reports: Anonymization Process Description (version 1.1)](https://arxiv.org/abs/2004.04145) (2020) Differential privacy techniques are used for anonymyzing and analyzing contact tracing data. 
  - A more background can be found in [Delivering a Rapid Digital Response to the COVID-19 Pandemic](https://cacm.acm.org/magazines/2022/1/257447-delivering-a-rapid-digital-response-to-the-covid-19-pandemic/abstract) (CACM 2022)


## Differential Privacy in Machine Learning

- [Differentially Private Machine Learning: Theory, Algorithms, and Applications](https://www.ece.rutgers.edu/~asarwate/nips2017/) (NIPS 2017 Tutorial)

## Security 

- [Side-Channel Attacks on Query-Based Data Anonymization](https://dl.acm.org/doi/10.1145/3460120.3484751) (2021) Even if the system satisfies differential privacy, there still is a way to find personal information without reading any query results. Side-channel attacks intentinally inject query errors (division by zero, overflow, etc.) or delays of query executions that happen when a specific condition matches. This paper shows such examples and provides ideas to avoid these side-channel attacks.
- [On significance of the least significant bits for differential privacy](https://dl.acm.org/doi/10.1145/2382196.2382264) (2012) Sampling from Laplace distribution suffers from insufficient resolution of floating-poing computations and damages DP gurantees. A practical approach for this problem is rounding the result after adding noise, but it sacrifices the utility of the result. Google's open-source DP library provides an alternative [secure noise generation](https://github.com/google/differential-privacy/blob/main/common_docs/Secure_Noise_Generation.pdf) method to lower the error. This approach can be applied to both the Laplace and Gaussian noise.
- [Precision-based attacks and interval refining: how to break, then fix, differential privacy on finite computers](https://arxiv.org/abs/2207.13793) (2022) A new type of attack utilizing the finite precision of floating-point values is found. 
  - [Tiny bits matter: precision-based attacks on differential privacy](https://www.tmlt.io/research/tiny-bits-matter-precision-based-attacks-on-differential-privacy) 

## Open-Source Libraries

- [Google Differential Privacy](https://github.com/google/differential-privacy) C++/Go/Java implementations of differential-privacy algorithms. It include code for adding Laplace/Gaussian noise, computing bounded aggregation, approximate bounding, etc.
- [OpenMined/PipelineDP](https://github.com/OpenMined/PipelineDP) A Python framework for applying differential private aggregations in Apache Spark, Apache Beam, etc.
- [OpenDP](https://github.com/opendp/opendp) A python library collection for differential privacy. 
- [Tumult Core](https://gitlab.com/tumult-labs/core) A collection of composable components for implementing algorithms to perform differentially private computations. This library is used for building DP-data processing engine on top of PySpark [timult-analytics](https://gitlab.com/tumult-labs/analytics).
- [Zeta SQL - anonymization_rewriter.cc](https://github.com/google/zetasql/blob/master/zetasql/analyzer/anonymization_rewriter.cc) An implementation of query rewriter for transforming aggregation queries into anonymized ones with clipping, adding noise, and thresholding.
- [IBM/Diffprivlib](https://github.com/IBM/differential-privacy-library) Diffprivlib is a general-purpose Python library for experimenting with, investigating and developing applications in, differential privacy.
- [microsoft/synthetic-data-showcase](https://github.com/microsoft/synthetic-data-showcase) Generates synthetic data and user interfaces for privacy-preserving data sharing and analysis.




## Companies Adopting Differential Privacy

- [Apple: Differential Privacy Overview](https://www.apple.com/privacy/docs/Differential_Privacy_Overview.pdf)
  - [Learning with Privacy at Scale](https://machinelearning.apple.com/research/learning-with-privacy-at-scale) (2017)
- [Google: How we're helping developers with differential privacy](https://developers.googleblog.com/2021/01/how-were-helping-developers-with-differential-privacy.html)
  - For example, Google Map uses DP algorithms for sharing histograms of vistors to restaurants. 
- Micorosoft
  - [AI Lab projects related to differential privacy](https://www.microsoft.com/en-us/ai/ai-lab-differential-privacy)
  - [Project Laplace](https://www.microsoft.com/en-us/research/project/project-laplace/)
- LinkedIn [A Members First Approach to Enabling LinkedIn's Labor Market Insights at Scale](https://arxiv.org/abs/2010.13981) (2020)
- [Tumult Labs](https://www.tmlt.io/)
- [Amazon: Differential Privacy](https://www.amazon.science/tag/differential-privacy)

# Readings in Differential Privacy

A list of papers and materialies for understanding differential privacy (DP) and its applications to real-world systems. 

## Introduction to Differential Privacy

- [Programming Differential Privacy](https://programming-dp.com/index.html) An online text book suited to learning the core concepts and theory around differential privacy. This book is from authors of CHORUS work.
- [Differential Privacy: The Pursuite of Protections by Default](https://dl.acm.org/doi/abs/10.1145/3434228). (2021) (_An online version of the article is also available at [acmqueue](https://queue.acm.org/detail.cfm?id=3439229)_). The authors of Google's DP SQL engine shared their learnings when applying differential privacy to the real world applications. Especially, they pointed out that bounding user-contributions, which is essential for computing sensitivity to adjust the amount of noise, was missing in the past studies. The previously adopted assumption that every user contributes only one record is often impracical in the context of user-log analysis, where individual users will appear multiple groups in the analysis.
- [Differential Privacy: A Primer for a Non-Technical Audience](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3338027) (2019) A good introduction for understanding the overall concepts and motivation behind the differential privacy. 
- [A friendly, non-technical introduction to differential privacy](https://desfontain.es/privacy/friendly-intro-to-differential-privacy.html) (2021) A series of blog posts that illustrate the theory and practice of differential privacy in a succinct manner.
  - [Local vs. central differential privacy](https://desfontain.es/privacy/local-global-differential-privacy.html) (2019) Explaining the differences between Local differential privacy (applying noise to the data) and Global differential privacy (applying noise to the query result). Middle-ground approaches betweem Local and Global DP have also been studied. 

### Tutorials

- Differential Privacy in the Wild. [Part 1](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-1.pdf), [Part 2](http://sigmod2017.org/wp-content/uploads/2017/03/04-Differential-Privacy-in-the-wild-2.pdf) (SIGMOD 2017 Tutorial)


## Differentially Private SQL Engines

- [Differentially Private SQL with Bounded User Contribution](https://arxiv.org/abs/1909.01917) (2019). Google developed a DP SQL engine that adds an appropriate amount of noise to query results by tracking user contributions through query processing. Several techniques described in this paper are apparently applied to building the [privacy polich checks in Google Ads Data Hub (ADH)](https://developers.google.com/ads-data-hub/guides/privacy-checks) service.
  - To restrict the number of maximum user-contributions to different partitions, it applies a randomized [reservoir sampling](https://dl.acm.org/doi/10.1145/3147.3165) (1985) method while scanning records from tables.  
  - The idea of thresholding groups represented by small number of people was originally proposed in [Releasing search queries and clicks privately
](https://dx.doi.org/10.1145/1526709.1526733) (2009)
- [CHORUS: a Programming Framework for Building Scalable Differential Privacy Mechanisms](https://ieeexplore.ieee.org/document/9230409) (Euro S&P 2020). An [open-source implementation of DP SQL engine written in Scala](https://github.com/uvm-plaid/chorus). This is a DBMS-independent approach for building DP SQL engines, which rewrites SQL queries and applies noise to the results as a post process.
- [LinkedIn's Audience Engagements API: A Privacy Preserving Data Analytics System at Scale](https://arxiv.org/abs/2002.05839) (2020) Following the same direction with CHORUS, LinkedIn implemented a DP SQL engine over their real-time SQL engine Pinot without changing the DBMS itself. It also has a privacy budget management sub-system. 
- [PrivateSQL: A Differentially Private SQL Query Engine](https://dl.acm.org/doi/10.14778/3342263.3342274) (2019) An early prototype to apply diffrential privacy to SQL processing. Although only `COUNT(*)` queries are supported, this work formalized join processing between multiple privacy tables (primary/secondary privacy relations) and developed a method to split privacy budget inside pre-defined workloads.

## Differential Privacy in Practice

- [A list of real-world uses of differential privacy](https://desfontain.es/privacy/real-world-differential-privacy.html) (2021). How the big tech companies, including Apple, Google, Facebook (Meta), LinkedIn, Microsoft, etc., applies differential privacy. 
- [Understanding Database Reconstruction Attacks on Public Data: These attacks on statistical databases are no longer a theoretical danger](https://dl.acm.org/doi/10.1145/3291276.3295691) (2018) The 2010 US Census used the notion of k-anonymity and nullified part of table cells for hiding too specific data. [Researchers simulated a database reconstruction attack (DRA) against the 2010 US Census data](https://www.census.gov/data/academy/webinars/2021/disclosure-avoidance-series/simulated-reconstruction-abetted-re-identification-attack-on-the-2010-census.html) and successfully recovered 46% of the original individual records, including the sex, age, race, ethnicity, and fine-grained geographic locations. If allowing errors within one year, it could reconstruct 71% of US population data (219 million records!).
- [Understanding the 2020 Census Disclosure Avoidance System](https://www2.census.gov/about/training-workshops/2021/2021-07-01-das-presentation.pdf) From the learning of the 2010 US Census, the 2020 version of US Census data has applied differential privacy technology to anonymize the published statistics with noise. 

## Open-Source Libraries

- [Google Differential Privacy](https://github.com/google/differential-privacy) C++/Go/Java implementations of differential-privacy algorithms. It include code for adding Laplace/Gaussian noise, computing bounded aggregation, approximate bounding, etc.
- [OpenDP](https://github.com/opendp/opendp) A python library collection for differential privacy. 


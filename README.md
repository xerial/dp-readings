# Readings in Differential Privacy

A list of papers and materialies for understanding differential privacy and its applications to database systems. 

## Introduction to Differential Privacy

- [Programming Differential Privacy](https://programming-dp.com/index.html) An online text book suited to start learning the core concepts and techniques around differential privacy.
- [Differential Privacy: The Pursuite of Protections by Default](https://dl.acm.org/doi/abs/10.1145/3434228). (2021) An online version of the article is also available at [acmqueue](https://queue.acm.org/detail.cfm?id=3439229). The authors of Google's DP SQL engine shared their learnings when applying differential privacy to the real world data. Especially, they pointed out that bounding user-contributions, which is essential for computing sensitivity to adjust the amount of noise, was missing in the past studies. An assumption that every user contributes only one record is not applicable in the context of user-log analysis of the big data.
- [Differential Privacy: A Primer for a Non-Technical Audience](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3338027) (2019) A good introduction for understanding the overall concepts and motivation behind the differential privacy. 
- [A friendly, non-technical introduction to differential privacy](https://desfontain.es/privacy/friendly-intro-to-differential-privacy.html) (2021) A series of great blog posts that illustrate the theory and practice of differential privacy.
- [Local vs. central differential privacy](https://desfontain.es/privacy/local-global-differential-privacy.html) (2019) Explaining the differences between Local differential privacy (applying noise to the data) and Global differential privacy (applying noise to the query result). Middle-ground approaches betweem Local and Global DP have also been studied. 

## Differentially Private SQL Engines

- [Differentially Private SQL with Bounded User Contribution](https://arxiv.org/abs/1909.01917) (2019). Google developed a DP SQL engine that adds an appropriate amount of noise to query results by tracking user contributions through query processing. Several techniques described in this paper are apparently applied to building Google Ads Data Hub (ADH) service.
  - To restrict the number of maximum user-contributions to different partitions, it applies a randomized [reservoir sampling](https://dl.acm.org/doi/10.1145/3147.3165) (1985) method while scanning records from tables.  
- [CHORUS: a Programming Framework for Building Scalable Differential Privacy Mechanisms](https://ieeexplore.ieee.org/document/9230409) (Euro S&P 2020). An [open-source implementation of DP SQL engine written in Scala](https://github.com/uvm-plaid/chorus) This work proposes a DBMS-independent approach for building DP SQL engines. CHORUS rewrites SQL queries and apply noise to the results as a post process.
- [LinkedIn's Audience Engagements API: A Privacy Preserving Data Analytics System at Scale](https://arxiv.org/abs/2002.05839) (2020) Following the same direction with CHORUS, LinkedIn implemented a DP SQL engine over their real-time SQL engine Pinot without changing the DBMS itself. It also has a privacy budget management sub-system. 

## Differential Privacy in Practice

- [Understanding Database Reconstruction Attacks on Public Data: These attacks on statistical databases are no longer a theoretical danger](https://dl.acm.org/doi/10.1145/3291276.3295691) (2018) The 2010 US Census used the notion of k-anonymity and nullified part of table cells for hiding too specific data. [Researchers simulated a database reconstruction attack (DRA) against the 2010 US Census data and successfully recovered 46% of the original individual records, including the sex, age, race, ethnicity, and fine-grained geographic locations. If allowing errors within one year, it could reconstruct 71% of US population data (219 million records!)](https://www.census.gov/data/academy/webinars/2021/disclosure-avoidance-series/simulated-reconstruction-abetted-re-identification-attack-on-the-2010-census.html).
- [Understanding the 2020 Census Disclosure Avoidance System](https://www2.census.gov/about/training-workshops/2021/2021-07-01-das-presentation.pdf) From the learning of the 2010 US Census, the 2020 version of US Census data has applied differential privacy technology to anonymize the published statistics with noise. 

- [A list of real-world uses of differential privacy](https://desfontain.es/privacy/real-world-differential-privacy.html) (2021). How the big tech companies, including Apple, Google, Facebook (Meta), LinkedIn, Microsoft, etc., applies differential privacy. 


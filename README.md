# Readings in Differential Privacy

A list of papers and materialies for understanding differential privacy and its applications to database systems. 

## Introduction to Differential Privacy

- [Programming Differential Privacy](https://programming-dp.com/index.html) An online text book suited to start learning the core concepts and techniques around differential privacy.
- Differential Privacy: The Pursuite of Protections by Default. ([CACM 2021](https://dl.acm.org/doi/abs/10.1145/3434228), A free version is available at [acmqueue](https://queue.acm.org/detail.cfm?id=3439229)) The authors of Google's DP SQL engine shared their learnings when applying differential privacy to the real world data. Especially, they pointed out that bounding user-contributions, which is essential for computing sensitivity to adjust the amount of noise, was missing in the past studies, and implicitely assumed that every user contributes only one record, which is not applicable in the context of user-log analysis in the big data era. 
- [Differential Privacy: A Primer for a Non-Technical Audience](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3338027) A good introduction for understanding the overall concepts of differential privacy, and it is important in real applications.


## Differentially Private SQL Engines

- [Differentially Private SQL with Bounded User Contribution](https://arxiv.org/abs/1909.01917) (2019). Google developed a DP SQL engine that adds an appropriate amount of noise to query results by tracking user contributions through query processing. Several techniques described in this paper are apparently applied to building Google Ads Data Hub (ADH) service.
- [CHORUS: a Programming Framework for Building Scalable Differential Privacy Mechanisms](https://ieeexplore.ieee.org/document/9230409) (Euro S&P 2020). An open-source implementation in Scala (GitHub)[https://github.com/uvm-plaid/chorus] of the DBMS-independent approach for building DP SQL engines. CHORUS rewrites SQL queries and apply noise as pre and post processes over DBMSs. 
- [LinkedIn's Audience Engagements API: A Privacy Preserving Data Analytics System at Scale] (2020) Following the same direction with CHORUS, LinkedIn implemented a DP SQL engine over their real-time SQL engine Pinot without changing the DBMS itself. It also has a privacy budget management sub-system. 

## Differential Privacy in Practice

- [Understanding the 2020 Census Disclosure Avoidance System](https://www2.census.gov/about/training-workshops/2021/2021-07-01-das-presentation.pdf) From the learning of the 2010 US Census, the 2020 version of US Census data has applied differential privacy technology to anonymize the published statistics with noise. 

- [A list of real-world uses of differential privacy](https://desfontain.es/privacy/real-world-differential-privacy.html) (2021). How the big tech companies, including Apple, Google, Facebook (Meta), LinkedIn, Microsoft, etc., applies differential privacy. 


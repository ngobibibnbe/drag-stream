# Benchmarking data stream outlier detection methods

### Main Contributions
A method for abnormal subsequence detection/discord in data stream. 

This work: 

:white_check_mark: Compare some data stream anomaly detection methods on their latences and performances 

:white_check_mark: comparison to other subsequence detection method

### Interested in my work?

Feel free to contact me at: anne.ngobibinbe@gmail.com

*The final version of our paper (in French) on the benchmark of data stream outlier detection methods is being submitted to 2020 ICDM conference.

### README Structure
1. [Methods compared](#Methods-compared): Presentation of methods we compared
2. [Datasets and their characteristics](#Datasets-and-their-characteristics): Brief Description of datasets and characteristics identified 
3. [Description of the experimental protocol](#Description-of-the-experimental-protocol): Description of the experimental protocol
5. [Results](#Results): Presentation of results obtained
6. [Reproducibility](#Reproducibility): Details on how to reproduce our tests
7. [Referencies](#Referencies)


## Methods compared
As it's the case for most of the anomaly detection methods, the following methods produce an anomaly score for each incoming instance showing how well the instance could be an anomaly, finally a threshold fixed by the user permits to say that instances with anomaly scores higher than the threshold are anomalies. In the literature, data stream anomaly detection methods are mostly separated into statistical based, tree based, proximity based and deep learning based approaches. We have chosen highly used and recommended approaches in each of those categories. 

Methods:
1. [LAMP](https://github.com/petrospgithub/onlinearima) : A method for abnormal subsequence detection in data stream inspired from Matrix profile
2. [Drag-stream] : Our proposition for discord detection
3. [Matrix Profile] : Time sries abnormal subsequence detection
. 

## Datasets and their characteristics
We selected datasets mostly from real known life problems.

 

## Description of the experimental protocol
For each dataset, a bayesian optimization is performed to find best hyperparameters (details of the hyperparameter search space of each method could be found in the implementation details (page 8) section of the [summary_of_the_experiment](https://github.com/nams2000/anomaly-detection-in-data-stream/blob/master/summary_of_the_experiments.pdf) file), then we test the method with the best hyperparameters and record the execution time and the f1-score. Finally we process the latence or response time (average time to treat an instance) (**latence =the execution time on the dataset**). To process the f1-score, we process as explain in the paper.

## Results
Due to conception restrictions KitNet couldn't be applied on univariate datasets and Online ARIMA can't be applied on multivariate datasets. 

:link: Anchor Links:
1. [Score](#F1-score)
2. [Execution time](#Execution time (ms))

### F1-score

Dataset | MILOF | IforestASD | HStree | Online ARIMA 
-----|-------------|------------|------------|-----------
ambiant temperature system failure| 0.4| **0.67** | 0.3 | **0.67**
cpu utilization asg misconfiguration|  0.5 |0.42 | 0.45 | **1**
ec2 request latency system failure| 0.5 | 0.343 | **0.94**  | 0.8 
machine temperature system failure| 0.15 | 0.7825 |**0.88** | 0.66
new york taxi|0.25 | 0.31 | 0.5 | **0.6**
rogue agent keyhold|  0.136 | 0.33 | 0.079 | 0.1
rogue agent key up down| 0.4 | **0.67** | 0.15 | 0.11



### Execution time (ms)
we rounded execution time.

 Dataset | MILOF | IforestASD | HStree | Online ARIMA 
-----|-------------|------------|------------|-----------
ambiant temperature system failure| 172 | 200 | 212 | **50**
cpu utilization asg misconfiguration| 430 | 438 | 738 | **129**
ec2 request latency system failure| 51 | 167 | 125 | **38**
machine temperature system failure| 560 | 580 | 9752 | **109**
new york taxi | **275** | 269 | 4776 | 391
rogue agent keyhold|  31 | 76| **16** | 17
rogue agent key up down| 26  | 203 | **8** | 37





## Reproducibility
:link: Anchor Links:
1. [Dependencies](#Dependencies)
2. [Launch test](#Launch-test)

### Dependencies:
Make sure you have at least python 3.6 

to install requirement type:
**pip install -r requirements.txt**

### Launch test:
On univariate dataset:
**python test_discord.py **

The results of the test will be in the folder result. The result file contains (In the result folder):
1. The execution time  on the dataset
2. The F1-score of each method
3. The best hyperparameters of each method
For each dataset and each method.

**Notices:** 
Details on characteristics of the datasets and hyperparameters we found are summarized in the file: [summary_of_the_experiment.pdf](https://github.com/nams2000/anomaly-detection-in-data-stream/blob/master/summary_of_the_experiments.pdf). 


## Referencies:
### 1. Methods:

Togbe, M. U., Y. Chabchoub, A. Boly, M. Barry, R. Chiky, et M. Bahri (2021). Anomalies
Detection Using Isolation in Concept-Drifting Data Streams. Computers 10(1).

Ding, Z. et M. Fei (2013). An anomaly detection approach based on isolation forest algorithm
for streaming data using sliding window. IFAC Proceedings Volumes 46(20), 12–17. 3rd
IFAC Conference on Intelligent Control and Automation Science ICONS 2013

an, S. C., K. M. Ting, et T. F. Liu (2011). Fast anomaly detection for streaming data. In
Proceedings of the Twenty-Second International Joint Conference on Artificial Intelligence Volume Volume Two, IJCAI’11, pp. 1511–1516. AAAI Press.

Salehi, M., C. Leckie, J. C. Bezdek, T. Vaithianathan, et X. Zhang (2016). Fast memory
efficient local outlier detection in data streams. IEEE Transactions on Knowledge and Data
Engineering 28, 3246–3260.

Mirsky, Y., T. Doitshman, Y. Elovici, et A. Shabtai (2018). Kitsune : An ensemble of autoencoders for online network intrusion detection. arXiv :1802.09089 [cs]. version : 2

Liu, C., S. C. H. Hoi, P. Zhao, et J. Sun (2016). Online arima algorithms for time series prediction. In Proceedings of the Thirtieth AAAI Conference on Artificial Intelligence, AAAI’16,
pp. 1867–1873. AAAI Press




### 2. Datasets:

Lavin, A. et S. Ahmad (2015). Evaluating real-time anomaly detection algorithms - the numenta anomaly benchmark. CoRR abs/1510.03336.

Iurii Katser, Viacheslav Kozitsin, V. L. et I. Maksimov (2021). Unsupervised offline change point detection ensembles. Applied sciences 11, 4280


### 3. Comparative studies:

Togbe, M., Y. Chabchoub, A. Boly, R. Chiky, C. Etude, et M. U. Togbe (2020). Etude compa-
rative des méthodes de détection d’anomalies. Revue des Nouvelles Technologies de l’Information Extraction et Gestion des Connaissances , RNTI-E-36, 109–120

SalehiMahsa et RashidiLida (2018). A Survey on Anomaly detection in Evolving Data. ACM
SIGKDD Explorations Newsletter 20(1), 13–23.

Nakamura, T., M. Imamura, R. Mercer, et E. Keogh (2020). Merlin : Parameter-free discovery
of arbitrary length anomalies in massive time series archives. In 2020 IEEE International
Conference on Data Mining (ICDM), pp. 1190–1195

Chandola, V., A. Banerjee, et V. Kumar (2009). Anomaly detection : A survey. ACM Comput.
Surv. 41(3).


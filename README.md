# Benchmarking data stream outlier detection methods

### Main Contributions
A method for abnormal subsequence detection/discord in data stream. 

This work: 

:white_check_mark: Compare some data stream anomaly detection methods on their latences and performances 

:white_check_mark: comparison to other subsequence detection method

### Interested in my work?

Feel free to contact me at: xxxx@xx (Going to be changed after the review, if there is any problem, initiate an issue and i will reply)

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
1. [LAMP]([https://github.com/petrospgithub/onlinearima](https://arxiv.org/pdf/2108.12093.pdf)) : A method for abnormal subsequence detection in data stream inspired from Matrix profile
2. [Drag-stream] : Our proposition for discord detection
3. [Matrix Profile](https://matrixprofile.docs.matrixprofile.org/) : Time sries abnormal subsequence detection
. 

## Datasets and their characteristics
We selected datasets mostly from diverse domains real life problems.

| Dataset       | Domain | Size |Number Of Known Anomalies | Has Concept Drifts |
|----------------------|-----------------|---------------|------------------------------------|-----------------------------|
| stdb\_308\_1         | ECG             | 5400          | 1                                  | no                          |
| xmitdb\_x108\_1      | ECG             | 5400          | 1                                  | yes                         |
| mitdb\_100\_180\_1   | ECG             | 5400          | 1                                  | no                          |
| chfdb\_chf01\_275\_1 | ECG             | 3751          | 1                                  | no                          |
| ltstdb\_20221\_43\_1 | ECG             | 5400          | 1                                  | no                          |
| mitdbx\_108          | ECG             | 16000         | 3                                  | yes                         |
| qtdbsele0606         | ECG             | 15000         | 1                                  | no                          |
| chfdbchf15           | ECG             | 15000         | 1                                  | no                          |
| ann-gun              | video recording | 11248         | 1                                  | no                          |
| patient respiration  | pneumology      | 6500          | 1                                  | yes                         |
| dutch power demand   | power demand    | 35040         | 4                                  | no                          |
| gps trajectory       | GPS             | 17175         | 1                                  | no                          |

 

## Description of the experimental protocol
For each dataset, a bayesian optimization is performed to find best hyperparameters (details of the hyperparameter search space of each method could be found in the implementation details (page 8) section of the [summary_of_the_experiment](https://github.com/nams2000/anomaly-detection-in-data-stream/blob/master/summary_of_the_experiments.pdf) file), then we test the method with the best hyperparameters and record the execution time and the f1-score. Finally we process the latence or response time (average time to treat an instance) (**latence =the execution time on the dataset**). The f1-score,is processed in order to take into account the accuracy and the recall of each method.

## Results
Due to conception restrictions KitNet couldn't be applied on univariate datasets and Online ARIMA can't be applied on multivariate datasets. 

:link: Anchor Links:
1. [Score](#F1-score)
2. [Execution time](#Execution time (ms))

### F1-score
| \textbf{Dataset}     <td colspan=2>DragStream <td colspan=2> LAMP <td colspan=2> Matrix Profile |
|----------------------|---------------------------------------------|---------------------------------------|-------------------------------------------------|
|                      | \textbf{Score}| \textbf{Params}           | \textbf{Score} | \textbf{Params}        | \textbf{Score}   | \textbf{Params} |
| stdb\_308\_1         | 0.19                                        | C=15, W=1330, r=8                     | \textbf{ 0.22}                                  | W=1350          | 0.069            | p=2             |
| xmitdb\_x108\_1      | 0.24                                        | C=14, W=1256, r=2.5                   | 0                                               | W=1350          | \textbf{0.554 }  | p=3             |
| mitdb\_\_100\_180\_1 | 0.5                                         | C=16, W=1236, r=4.5                   | 0                                               | W=1350          | \textbf{ 0.5468} | p=3             |
| chfdb\_chf01\_275\_1 | 0.5                                         | C=17, W=751, r=2.5                    | 0.09                                            | W=937           | \textbf{ 0.63}   | p=3             |
| ltstdb\_20221\_43\_1 | 0.4                                         | C=19, W=440, r=3.0                    | 0.1                                             | W=937           | \textbf{0.415 }  | p=1             |
| mitdbx\_108          | 0.48                                        | C=10, W=4479, r=3.5                   | 0.285                                           | W=5400          | \textbf{0.821 }  | p=3             |
| qtdbsele0606         | 0.01                                        | C=10, W=222, r=4.5                    | \textbf{0.55}                                   | W=3750          | 0.005            | p=1             |
| chfdbchf15           | 0.5                                         | C=15, W=2915, r=1.5                   | 0.067                                           | W=3750          | \textbf{0.81}    | p=1             |
| ann-gun              | \textbf{0.36}                               | C=13, W=178, r=1.0                    | 0.26                                            | W=2812          | 0.026            | p=3             |
| patient respiration  | \textbf{0.67 }                              | C=14, W=1011, r=4.5                   | 0.24                                            | W=1627          | 0.46             | p=3             |
| dutch power demand   | 0.56                                        | C=29, W=4433, r=2.0                   | 0.1639                                          | W=8760          | \textbf{0.75}    | p=5             |
| gps trajectory       | \textbf{0.286}                              | C=18, W=4210, r=8.5                   | 0                                               | W=4293          | 0.08             | p=2             |
| Mean $\pm$ STD       | $0.39 \pm 0.18$                             |                                       | $0.16 \pm 0.15$                                 |                 | $0.43 \pm 0.31$  |                 |

### Execution time (ms)

| extbf{Dataset}       | \texttt{DragStream} | \texttt{LAMP}         | \texttt{Matrix Profile} |
|----------------------|---------------------|-----------------------|-------------------------|
| stdb\_308\_1         | \textbf{7.1}        | 554                   | 9.54                    |
| xmitdb\_x108\_1      | 7.1                 | 442                   | *6.33*          |
| mitdb\_\_100\_180\_1 | 7.29                | 554                   | \textbf{6.34}           |
| chfdb\_chf01\_275\_1 | *1.75*       | 443                   | 2.91                    |
| ltstdb\_20221\_43\_1 | 1.65                | 3.61                  | \textbf{1.57}           |
| mitdbx\_108          | 324                 | 7162                  | \textbf{322}            |
| qtdbsele0606         | 13.43               | 851                   | \textbf{ 7.89}          |
| chfdbchf15           | 49.42               | 2535                  | \textbf{47.41}          |
| ann-gun              | \textbf{13.29}      | 1364                  | 25.86                   |
| patient respiration  | 14.29               | 531                   | \textbf{3.63}           |
| dutch power demand   | \textbf{15.3}       | 9981                  | 1042                    |
| gps trajectory       | \textbf{115}        | 9302                  | 206.27                  |
| Mean $\pm$ STD       | 47.47 $\pm$ 88.77   | 2810.31 $\pm$ 3570.39 | 140.15 $\pm$ 288.6      |





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
Details on characteristics of the datasets and hyperparameters we found are summarized in the file: [summary_of_the_experiment.pdf]


## Referencies:
### 1. Methods:
C.-C. M. Yeh, Y. Zhu, L. Ulanova, N. Begum, Y. Ding, H. A. Dau, D. F. Silva, A. Mueen, and E. Keogh, “Matrix profile i: All pairs similarity joins for time series: A unifying view that includes motifs, discords and shapelets,” in 2016 IEEE 16th International Conference on Data Mining
(ICDM), pp. 1317–1322, 2016.

Z. Zimmerman et al., "Matrix Profile XVIII: Time Series Mining in the Face of Fast Moving Streams using a Learned Approximate Matrix Profile," 2019 IEEE International Conference on Data Mining (ICDM), 2019, pp. 936-945, doi: 10.1109/ICDM.2019.00104.

### 2. Datasets:

T. Nakamura, M. Imamura, R. Mercer, and E. Keogh, “Merlin:Parameter-free discovery of arbitrary length anomalies in massive time series archives,” in IEEE International Conference on Data Mining (ICDM), pp. 1190–1195, 2020.

P. M. Chau, B. M. Duc, and D. T. Anh, “Discord discovery in streaming time series based on an improved hot sax algorithm,” in Proceedings of the Ninth International Symposium on Information and Communication Technology, SoICT 2018, (New York, NY, USA), p. 24–30, Association for Computing Machinery, 2018.


### 3. Comparative studies:

SalehiMahsa et RashidiLida (2018). A Survey on Anomaly detection in Evolving Data. ACM
SIGKDD Explorations Newsletter 20(1), 13–23.

Chandola, V., A. Banerjee, et V. Kumar (2009). Anomaly detection : A survey. ACM Comput.
Surv. 41(3).


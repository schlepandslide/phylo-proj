Short list of required software (Based on Windows x64 archetecture)
- ClustalW2
	- ClustalX 2.1
- IQ-Tree
- mrbayes

# 2/20/25
- removed old data set, new data comes from ncbi. see the fna file for more info
- Used ClustalX2 on new data: pseudomonas.fna

Pros: Very easy to install, UI based
Cons: The same as ClustalW2, may not be as complete as T-coffee

Based on a windows install, you can essentially plug-and-play. Though install clustalW2 beforehand using the documentation
Load the fna file > Ctrl+O > Ctrl+L to make alignments > Save sequence as nexus, and .phy

# 3/4/25
- updated fasta alignments
- wrote r script using ape and pranghorn
	- follows the same process as class, except uses njs() due to an error
*note that this is unessecary for the pipeline and was done as an exercise

# 3/20/25
- replaced the dataset once again, say hello to the 16s gene of *Pseudomonas*
- chose IQ-Tree as my software for max. likelihood
	- mainly due to RAxML not running on windows
		-Pros: runs on windows, Fast!, command-line based
		-Cons: Bias prone, relies on simplification
		-Assumptions: Treelikeness, homogeneity

sample code/commands:
	
.\iqtree -s pseudo-16s.fasta -bb 1000 -nt AUTO #basic ML reconstruction
.\iqtree -s pseudo-16s.fasta -spp pseudo-16s.nxs -bb 1000 -nt AUTO #partition model finder
.\iqtree -s pseudo-16s.fasta -spp pseudo-16s.nxs -bb 1000 -nt AUTO -m MFP+MERGE -rcluster 10 -pre pseudo-16s.merge #partition model merge
.\type pseudo-16s.fasta.treefile pseudo-16s.nxs.treefile >pseudo-16s.trees #log-likelihood test
.\iqtree -s pseudo-16s.fasta -spp pseudo-16s.nxs.best_scheme.nxs -z pseudo-16s.trees -zb 1000 -n 0 -wpl -pre pseudo-16s.test #pass on

TBD: iq-tree beta code?

.\iqtree -s pseudo-16s.fasta -spp pseudo-16s.nxs -bb 1000 -nt AUTO -bsam GENESITE -pre pseudo-16s.bsam

## Real IQ-tree code
.\iqtree2 -s pseudo-16s.phy

```
IQ-TREE multicore version 2.4.0 for Windows 64-bit built Feb  7 2025
Developed by Bui Quang Minh, Nguyen Lam Tung, Olga Chernomor, Heiko Schmidt,
Dominik Schrempf, Michael Woodhams, Ly Trong Nhan, Thomas Wong

Host:    BINCH (AVX512, FMA3, 47 GB RAM)
Command: C:\iqtree\bin\iqtree2.exe -s pseudo-16s.phy
Seed:    682894 (Using SPRNG - Scalable Parallel Random Number Generator)
Time:    Wed May 07 10:46:17 2025
Kernel:  AVX+FMA - 1 threads (16 CPU cores detected)

HINT: Use -nt option to specify number of threads because your CPU has 16 cores!
HINT: -nt AUTO will automatically determine the best number of threads to use.

Reading alignment file pseudo-16s.phy ... Phylip format detected
Alignment most likely contains DNA/RNA sequences
Alignment has 30 sequences with 1510 columns, 328 distinct patterns
126 parsimony-informative, 121 singleton sites, 1263 constant sites
            Gap/Ambiguity  Composition  p-value
Analyzing sequences: done in 3.43e-005 secs
   1  PQ782784.1    5.10%    passed     94.89%
   2  PV256206.1    2.58%    passed     98.60%
   3  PQ897219.1    3.25%    passed     99.44%
   4  PV111332.1    6.03%    passed     99.94%
   5  PQ797033.1    6.29%    passed     99.38%
   6  AB603655.1   23.71%    passed     92.66%
   7  PP237255.1    4.97%    passed     99.95%
   8  PQ656938.1   55.23%    passed     64.39%
   9  PQ554712.1   27.15%    passed     89.65%
  10  PV076873.1    8.74%    passed     99.86%
  11  PV256072.1    5.10%    passed     99.95%
  12  PQ782809.1    5.17%    passed     98.06%
  13  PV195286.1   11.59%    passed     99.98%
  14  OR430114.1    6.62%    passed     99.78%
  15  OQ891268.1    7.02%    passed     99.70%
  16  OR497730.1   56.69%    passed     50.20%
  17  PQ782653.1    4.83%    passed     96.32%
  18  PP082086.1    6.16%    passed     99.50%
  19  PQ812515.1   28.61%    passed     94.74%
  20  OQ983818.1    5.43%    passed     99.02%
  21  PV130052.1    8.74%    passed     99.86%
  22  PQ782692.1    4.70%    passed     96.42%
  23  PQ782438.1    6.89%    passed     99.98%
  24  PQ782870.1    5.17%    passed     97.14%
  25  PQ097984.1   11.06%    passed     99.75%
  26  PQ782302.1    4.64%    passed     88.19%
  27  PQ782679.1    5.03%    passed     99.88%
  28  PQ454920.1   23.71%    passed     93.41%
  29  PQ782693.1    4.64%    passed     98.97%
  30  PQ656875.1   55.23%    passed     70.55%
WARNING: 3 sequences contain more than 50% gaps/ambiguity
****  TOTAL        13.67%  0 sequences failed composition chi2 test (p-value<5%; df=3)
NOTE: PV130052.1 is identical to PV076873.1 but kept for subsequent analysis


Create initial parsimony tree by phylogenetic likelihood library (PLL)... 0.003 seconds
Perform fast likelihood tree search using GTR+I+G model...
Estimate model parameters (epsilon = 5.000)
Perform nearest neighbor interchange...
Estimate model parameters (epsilon = 1.000)
1. Initial log-likelihood: -4907.792
2. Current log-likelihood: -4905.821
3. Current log-likelihood: -4904.155
4. Current log-likelihood: -4902.716
5. Current log-likelihood: -4901.485
6. Current log-likelihood: -4900.441
Optimal log-likelihood: -4899.512
Rate parameters:  A-C: 0.60109  A-G: 1.19769  A-T: 0.96294  C-G: 0.77365  C-T: 1.63780  G-T: 1.00000
Base frequencies:  A: 0.254  C: 0.222  G: 0.313  T: 0.211
Proportion of invariable sites: 0.553
Gamma shape alpha: 0.249
Parameters optimization took 6 rounds (0.053 sec)
Time for fast ML tree search: 0.129 seconds

NOTE: ModelFinder requires 3 MB RAM!
ModelFinder will test up to 484 DNA models (sample size: 1510 epsilon: 0.100) ...
 No. Model         -LnL         df  AIC          AICc         BIC
  1  GTR+F         5373.365     65  10876.730    10882.671    11222.521
  2  GTR+F+I       4971.498     66  10074.996    10081.125    10426.107
  3  GTR+F+G4      4980.657     66  10093.313    10099.442    10444.424
  4  GTR+F+I+G4    4895.759     67  9925.518     9931.837     10281.949
  5  GTR+F+R2      4873.565     67  9881.130     9887.449     10237.561
  6  GTR+F+R3      4873.547     69  9885.094     9891.802     10252.165
 14  GTR+F+I+R2    4874.118     68  9884.235     9890.747     10245.986
+I+R3 reinitialized from +I+R2 with factor 0.500
+I+R3 reinitialized from +I+R2 with factor 0.250
 15  GTR+F+I+R3    4874.056     70  9888.112     9895.020     10260.503
 27  SYM+R2        4893.103     64  9914.206     9919.964     10254.677
 36  SYM+I+R2      4893.357     65  9916.715     9922.656     10262.506
 49  TVM+F+R2      4874.897     66  9881.794     9887.923     10232.905
 58  TVM+F+I+R2    4875.458     67  9884.917     9891.236     10241.348
 71  TVMe+R2       4893.138     63  9912.277     9917.854     10247.428
 80  TVMe+I+R2     4893.421     64  9914.841     9920.599     10255.313
 93  TIM3+F+R2     4873.972     65  9877.943     9883.885     10223.734
102  TIM3+F+I+R2   4874.539     66  9881.077     9887.206     10232.189
115  TIM3e+R2      4894.358     62  9912.716     9918.115     10242.548
124  TIM3e+I+R2    4894.819     63  9915.638     9921.215     10250.790
137  TIM2+F+R2     4876.054     65  9882.108     9888.050     10227.899
146  TIM2+F+I+R2   4876.655     66  9885.311     9891.440     10236.422
159  TIM2e+R2      4895.216     62  9914.431     9919.830     10244.263
168  TIM2e+I+R2    4895.499     63  9916.997     9922.574     10252.149
181  TIM+F+R2      4876.190     65  9882.380     9888.322     10228.171
190  TIM+F+I+R2    4876.822     66  9885.643     9891.772     10236.754
203  TIMe+R2       4896.208     62  9916.416     9921.815     10246.248
212  TIMe+I+R2     4896.699     63  9919.397     9924.974     10254.549
225  TPM3u+F+R2    4875.290     64  9878.581     9884.339     10219.052
234  TPM3u+F+I+R2  4875.855     65  9881.710     9887.651     10227.501
247  TPM3+R2       4894.394     61  9910.789     9916.012     10235.300
256  TPM3+I+R2     4894.836     62  9913.671     9919.070     10243.503
269  TPM2u+F+R2    4877.364     64  9882.727     9888.485     10223.199
278  TPM2u+F+I+R2  4877.937     65  9885.874     9891.816     10231.665
291  TPM2+R2       4895.258     61  9912.517     9917.740     10237.028
300  TPM2+I+R2     4895.542     62  9915.083     9920.482     10244.915
313  K3Pu+F+R2     4877.503     64  9883.005     9888.763     10223.477
322  K3Pu+F+I+R2   4878.113     65  9886.226     9892.168     10232.018
335  K3P+R2        4896.244     61  9914.489     9919.712     10239.000
344  K3P+I+R2      4896.720     62  9917.440     9922.839     10247.272
357  TN+F+R2       4876.231     64  9880.461     9886.219     10220.933
366  TN+F+I+R2     4876.803     65  9883.607     9889.548     10229.398
379  TNe+R2        4896.248     61  9914.497     9919.721     10239.009
388  TNe+I+R2      4896.683     62  9917.365     9922.764     10247.197
401  HKY+F+R2      4877.546     63  9881.092     9886.668     10216.243
410  HKY+F+I+R2    4878.125     64  9884.250     9890.007     10224.721
423  K2P+R2        4896.285     60  9912.571     9917.622     10231.762
432  K2P+I+R2      4896.731     61  9915.463     9920.687     10239.975
445  F81+F+R2      4888.960     62  9901.920     9907.318     10231.751
454  F81+F+I+R2    4889.596     63  9905.192     9910.769     10240.343
467  JC+R2         4908.548     59  9935.097     9939.979     10248.969
476  JC+I+R2       4909.103     60  9938.206     9943.258     10257.398
Akaike Information Criterion:           TIM3+F+R2
Corrected Akaike Information Criterion: TIM3+F+R2
Bayesian Information Criterion:         HKY+F+R2
Best-fit model: HKY+F+R2 chosen according to BIC

All model information printed to pseudo-16s.phy.model.gz
CPU time for ModelFinder: 0.969 seconds (0h:0m:0s)
Wall-clock time for ModelFinder: 1.099 seconds (0h:0m:1s)

NOTE: 0 MB RAM (0 GB) is required!
Estimate model parameters (epsilon = 0.100)
1. Initial log-likelihood: -4889.248
2. Current log-likelihood: -4877.664
Optimal log-likelihood: -4877.565
Rate parameters:  A-C: 1.00000  A-G: 1.64620  A-T: 1.00000  C-G: 1.00000  C-T: 1.64620  G-T: 1.00000
Base frequencies:  A: 0.254  C: 0.222  G: 0.313  T: 0.211
Site proportion and rates:  (0.921,0.184) (0.079,10.533)
Parameters optimization took 2 rounds (0.021 sec)
Wrote distance file to... 
Computing ML distances based on estimated model parameters...
Calculating distance matrix: done in 0.001754 secs
Computing ML distances took 0.006358 sec (of wall-clock time) 0.000000 sec (of CPU time)
Setting up auxiliary I and S matrices: done in 5.31001e-005 secs
Computing RapidNJ tree took 0.001676 sec (of wall-clock time) 0.000000 sec (of CPU time)
Log-likelihood of RapidNJ tree: -4986.849
--------------------------------------------------------------------
|             INITIALIZING CANDIDATE TREE SET                      |
--------------------------------------------------------------------
Generating 98 parsimony trees... 0.129 second
Computing log-likelihood of 98 initial trees ... 0.096 seconds
Current best score: -4869.165

Do NNI search on 20 best initial trees
Estimate model parameters (epsilon = 0.100)
BETTER TREE FOUND at iteration 1: -4861.847
UPDATE BEST LOG-LIKELIHOOD: -4861.847
Iteration 10 / LogL: -4861.847 / Time: 0h:0m:1s
Iteration 20 / LogL: -4863.138 / Time: 0h:0m:1s
Finish initializing candidate tree set (13)
Current best tree score: -4861.847 / CPU time: 0.613
Number of iterations: 20
--------------------------------------------------------------------
|               OPTIMIZING CANDIDATE TREE SET                      |
--------------------------------------------------------------------
UPDATE BEST LOG-LIKELIHOOD: -4861.847
Iteration 30 / LogL: -4861.870 / Time: 0h:0m:1s (0h:0m:2s left)
UPDATE BEST LOG-LIKELIHOOD: -4861.846
Iteration 40 / LogL: -4861.952 / Time: 0h:0m:2s (0h:0m:1s left)
UPDATE BEST LOG-LIKELIHOOD: -4861.846
UPDATE BEST LOG-LIKELIHOOD: -4861.846
Iteration 50 / LogL: -4861.847 / Time: 0h:0m:2s (0h:0m:1s left)
Iteration 60 / LogL: -4861.959 / Time: 0h:0m:2s (0h:0m:1s left)
Iteration 70 / LogL: -4861.948 / Time: 0h:0m:2s (0h:0m:0s left)
Iteration 80 / LogL: -4870.398 / Time: 0h:0m:3s (0h:0m:0s left)
Iteration 90 / LogL: -4862.918 / Time: 0h:0m:3s (0h:0m:0s left)
Iteration 100 / LogL: -4863.278 / Time: 0h:0m:3s (0h:0m:0s left)
TREE SEARCH COMPLETED AFTER 102 ITERATIONS / Time: 0h:0m:3s

--------------------------------------------------------------------
|                    FINALIZING TREE SEARCH                        |
--------------------------------------------------------------------
Performs final model parameters optimization
Estimate model parameters (epsilon = 0.010)
1. Initial log-likelihood: -4861.846
Optimal log-likelihood: -4861.845
Rate parameters:  A-C: 1.00000  A-G: 1.63806  A-T: 1.00000  C-G: 1.00000  C-T: 1.63806  G-T: 1.00000
Base frequencies:  A: 0.254  C: 0.222  G: 0.313  T: 0.211
Site proportion and rates:  (0.921,0.182) (0.079,10.476)
Parameters optimization took 1 rounds (0.013 sec)
BEST SCORE FOUND : -4861.845
Total tree length: 0.608

Total number of iterations: 102
CPU time used for tree search: 2.578 sec (0h:0m:2s)
Wall-clock time used for tree search: 2.240 sec (0h:0m:2s)
Total CPU time used: 3.609 sec (0h:0m:3s)
Total wall-clock time used: 3.443 sec (0h:0m:3s)

Analysis results written to: 
  IQ-TREE report:                pseudo-16s.phy.iqtree
  Maximum-likelihood tree:       pseudo-16s.phy.treefile
  Likelihood distances:          pseudo-16s.phy.mldist
  Screen log file:               pseudo-16s.phy.log

Date and Time: Wed May 07 10:46:21 2025
```

# 4/10/25

- Mr Bayes set-up 
	- Pros: Easy set-up 
	- Cons: Lots of tinkering 
	- Considerations: You actually need to somewhat understand whats happening

> exe pseudo-16s.nxs
> lset nucmodel=codon nst=6 rates=invgamma [!Error in Lset due to STOP codon]
> lset nucmodel=4by4 nst=6 rates=invgamma [works]
> mcmcp ngen=20000 samplefreq=200 diagnfreq=500 burninfrac=0.20 stopval=0.01
> sump [!Error; Could not open file]
[Forgot to actually run mcmc]
> mcmc
> [Continue?] Yes > 20
> [Recieve output]
> sump
- undersampled
> mcmcp ngen=20000 samplefreq=2000 diagnfreq=500 burninfrac=0.20 stopval=0.01
- undersampled again
> mcmcp ngen=1500000 samplefreq=5 diagnfreq=50 burninfrac=0.20 stopval=0.01
> mcmc
> sump
> sumt conformat=simple

[final data set run]
> exe pseudo-16s.nxs
> lset nucmodel=4by4 nst=6 rates=invgamma
> mcmcp ngen=1500000 samplefreq=5 diagnfreq=50 burninfrac=0.20 stopval=0.01
```
   Analysis completed in 53 mins 56 seconds
   Analysis used 3235.94 seconds of CPU time
   Likelihood of best state for "cold" chain of run 1 was -4894.78
   Likelihood of best state for "cold" chain of run 2 was -4896.49

   Acceptance rates for the moves in the "cold" chain of run 1:
      With prob.   (last 100)   chain accepted proposals by move
         31.2 %     ( 23 %)     Dirichlet(Revmat)
         45.8 %     ( 31 %)     Slider(Revmat)
         21.2 %     ( 19 %)     Dirichlet(Pi)
         25.7 %     ( 31 %)     Slider(Pi)
         28.0 %     ( 25 %)     Multiplier(Alpha)
         30.5 %     ( 32 %)     Slider(Pinvar)
         20.4 %     ( 25 %)     ExtSPR(Tau,V)
         14.5 %     ( 14 %)     ExtTBR(Tau,V)
         26.1 %     ( 28 %)     NNI(Tau,V)
         13.5 %     (  8 %)     ParsSPR(Tau,V)
         26.4 %     ( 28 %)     Multiplier(V)
         46.7 %     ( 41 %)     Nodeslider(V)
         25.6 %     ( 31 %)     TLMultiplier(V)

   Acceptance rates for the moves in the "cold" chain of run 2:
      With prob.   (last 100)   chain accepted proposals by move
         31.1 %     ( 23 %)     Dirichlet(Revmat)
         46.4 %     ( 29 %)     Slider(Revmat)
         21.7 %     ( 19 %)     Dirichlet(Pi)
         25.2 %     ( 20 %)     Slider(Pi)
         27.6 %     ( 34 %)     Multiplier(Alpha)
         31.0 %     ( 25 %)     Slider(Pinvar)
         20.4 %     ( 11 %)     ExtSPR(Tau,V)
         14.7 %     ( 12 %)     ExtTBR(Tau,V)
         26.1 %     ( 26 %)     NNI(Tau,V)
         13.5 %     ( 12 %)     ParsSPR(Tau,V)
         26.3 %     ( 28 %)     Multiplier(V)
         46.9 %     ( 51 %)     Nodeslider(V)
         25.5 %     ( 34 %)     TLMultiplier(V)

   Chain swap information for run 1:

                1       2       3       4
        ----------------------------------
      1 |            0.56    0.25    0.09
      2 |  250068            0.56    0.25
      3 |  250463  249448            0.57
      4 |  249869  249943  250209

   Chain swap information for run 2:

                1       2       3       4
        ----------------------------------
      1 |            0.54    0.22    0.07
      2 |  250670            0.54    0.22
      3 |  249511  249914            0.55
      4 |  249684  250792  249429

   Upper diagonal: Proportion of successful state exchanges between chains
   Lower diagonal: Number of attempted state exchanges between chains

   Chain information:

     ID -- Heat
    -----------
      1 -- 1.00  (cold chain)
      2 -- 0.91
      3 -- 0.83
      4 -- 0.77

   Heat = 1 / (1 + T * (ID - 1))
      (where T = 0.10 is the temperature and ID is the chain number)

```
> sump
```
  Summarizing parameters in files pseudo-16s.nxs.run1.p and pseudo-16s.nxs.run2.p
   Writing summary statistics to file pseudo-16s.nxs.pstat
   Using relative burnin ('relburnin=yes'), discarding the first 20 % of samples

   Below are rough plots of the generation (x-axis) versus the log
   probability of observing the data (y-axis). You can use these
   graphs to determine what the burn in for your analysis should be.
   When the log probability starts to plateau you may be at station-
   arity. Sample trees and parameters after the log probability
   plateaus. Of course, this is not a guarantee that you are at sta-
   tionarity. Also examine the convergence diagnostics provided by
   the 'sump' and 'sumt' commands for all the parameters in your
   model. Remember that the burn in is the number of samples to dis-
   card. There are a total of ngen / samplefreq samples taken during
   a MCMC analysis.

   Overlay plot for both runs:
   (1 = Run number 1; 2 = Run number 2; * = Both runs)

   +------------------------------------------------------------+ -4914.26
   |    2             2                    1          2         |
   |                                                        2   |
   |         1      2        2   1        1              2    22|
   |                      1                      1     1     1  |
   |     121      2 12 1           2 122     11 1         2  2  |
   |  2  2        1     2   1     1     2       2 1  1  1       |
   |      1     *  *  1 1      11            221   11   2     11|
   |        *                 12  211 1  *  2    2 2       2    |
   |*1 11                       2      1   2   2  2  2   11     |
   | 2     2 21        2  2121       2    2 1                   |
   |           *         * 2  2         1                       |
   |   2         1               2  2                 1    11   |
   |          2                                        2        |
   |             2   1                              2           |
   |  1                                                         |
   +------+-----+-----+-----+-----+-----+-----+-----+-----+-----+ -4919.22
   ^                                                            ^
   300000                                                       1500000


   Estimated marginal likelihoods for runs sampled in files
      "pseudo-16s.nxs.run1.p" and "pseudo-16s.nxs.run2.p":
      (Use the harmonic mean for Bayes factor comparisons of models)

      (Values are saved to the file pseudo-16s.nxs.lstat)

   Run   Arithmetic mean   Harmonic mean
   --------------------------------------
     1      -4904.35         -4946.40
     2      -4904.77         -4941.20
   --------------------------------------
   TOTAL    -4904.54         -4945.71
   --------------------------------------


   Model parameter summaries over the runs sampled in files
      "pseudo-16s.nxs.run1.p" and "pseudo-16s.nxs.run2.p":
      Summaries are based on a total of 480002 samples from 2 runs.
      Each run produced 300001 samples of which 240001 samples were included.
      Parameter summaries saved to file "pseudo-16s.nxs.pstat".

                                         95% HPD Interval
                                       --------------------
   Parameter      Mean      Variance     Lower       Upper       Median    min ESS*  avg ESS    PSRF+
   --------------------------------------------------------------------------------------------------
   TL          0.714282    0.004965    0.579476    0.853255    0.710395   5089.59   5434.61    1.000
   r(A<->C)    0.105851    0.000347    0.069959    0.142747    0.105113   1826.97   1995.86    1.000
   r(A<->G)    0.200932    0.000491    0.158264    0.244417    0.200148   1481.01   1889.55    1.000
   r(A<->T)    0.157603    0.000465    0.117004    0.200091    0.156963   2366.86   2480.08    1.000
   r(C<->G)    0.126712    0.000346    0.091526    0.163388    0.126249   2293.11   2337.55    1.001
   r(C<->T)    0.254841    0.000773    0.202937    0.310941    0.254200   1522.56   1755.00    1.000
   r(G<->T)    0.154061    0.000399    0.116372    0.193919    0.153206   2675.93   2739.17    1.000
   pi(A)       0.254649    0.000107    0.235307    0.275645    0.254634   2779.47   3105.61    1.000
   pi(C)       0.222102    0.000100    0.202837    0.242133    0.221884   2548.38   2767.82    1.000
   pi(G)       0.307584    0.000120    0.285572    0.328603    0.307621   2801.64   3008.64    1.000
   pi(T)       0.215665    0.000093    0.197275    0.234762    0.215543   2598.92   3026.19    1.000
   alpha       0.394140    0.005952    0.263504    0.553382    0.382889   2275.50   2423.15    1.000
   pinvar      0.671395    0.001132    0.604991    0.735583    0.672615   2256.78   2483.66    1.000
   --------------------------------------------------------------------------------------------------
   * Convergence diagnostic (ESS = Estimated Sample Size); min and avg values
     correspond to minimal and average ESS among runs.
     ESS value below 100 may indicate that the parameter is undersampled.
   + Convergence diagnostic (PSRF = Potential Scale Reduction Factor; Gelman
     and Rubin, 1992) should approach 1.0 as runs converge.
```
>sumt conformat=simple
```
 Setting sumt conformat to Simple
   Summarizing trees in files "pseudo-16s.nxs.run1.t" and "pseudo-16s.nxs.run2.t"
   Using relative burnin ('relburnin=yes'), discarding the first 20 % of sampled trees
   Writing statistics to files pseudo-16s.nxs.<parts|tstat|vstat|trprobs|con>
   Examining first file ...
   Found one tree block in file "pseudo-16s.nxs.run1.t" with 300001 trees in last block
   Expecting the same number of trees in the last tree block of all files

   Tree reading status:

   0      10      20      30      40      50      60      70      80      90     100
   v-------v-------v-------v-------v-------v-------v-------v-------v-------v-------v
   *********************************************************************************

   Read a total of 600002 trees in 2 files (sampling 480002 of them)
      (Each file contained 300001 trees of which 240001 were sampled)

   General explanation:

   In an unrooted tree, a taxon bipartition (split) is specified by removing a
   branch, thereby dividing the species into those to the left and those to the
   right of the branch. Here, taxa to one side of the removed branch are denoted
   '.' and those to the other side are denoted '*'. Specifically, the '.' symbol
   is used for the taxa on the same side as the outgroup.

   In a rooted or clock tree, the tree is rooted using the model and not by
   reference to an outgroup. Each bipartition therefore corresponds to a clade,
   that is, a group that includes all the descendants of a particular branch in
   the tree.  Taxa that are included in each clade are denoted using '*', and
   taxa that are not included are denoted using the '.' symbol.

   The output first includes a key to all the bipartitions with frequency larger
   or equual to (Minpartfreq) in at least one run. Minpartfreq is a parameter to
   sumt command and currently it is set to 0.10.  This is followed by a table
   with statistics for the informative bipartitions (those including at least
   two taxa), sorted from highest to lowest probability. For each bipartition,
   the table gives the number of times the partition or split was observed in all
   runs (#obs) and the posterior probability of the bipartition (Probab.), which
   is the same as the split frequency. If several runs are summarized, this is
   followed by the minimum split frequency (Min(s)), the maximum frequency
   (Max(s)), and the standard deviation of frequencies (Stddev(s)) across runs.
   The latter value should approach 0 for all bipartitions as MCMC runs converge.

   This is followed by a table summarizing branch lengths, node heights (if a
   clock model was used) and relaxed clock parameters (if a relaxed clock model
   was used). The mean, variance, and 95 % credible interval are given for each
   of these parameters. If several runs are summarized, the potential scale
   reduction factor (PSRF) is also given; it should approach 1 as runs converge.
   Node heights will take calibration points into account, if such points were
   used in the analysis.

   Note that Stddev may be unreliable if the partition is not present in all
   runs (the last column indicates the number of runs that sampled the partition
   if more than one run is summarized). The PSRF is not calculated at all if
   the partition is not present in all runs.The PSRF is also sensitive to small
   sample sizes and it should only be considered a rough guide to convergence
   since some of the assumptions allowing one to interpret it as a true potential
   scale reduction factor are violated in MrBayes.

   List of taxa in bipartitions:

      1 -- PQ782784.1
      2 -- PV256206.1
      3 -- PQ897219.1
      4 -- PV111332.1
      5 -- PQ797033.1
      6 -- AB603655.1
      7 -- PP237255.1
      8 -- PQ656938.1
      9 -- PQ554712.1
     10 -- PV076873.1
     11 -- PV256072.1
     12 -- PQ782809.1
     13 -- PV195286.1
     14 -- OR430114.1
     15 -- OQ891268.1
     16 -- OR497730.1
     17 -- PQ782653.1
     18 -- PP082086.1
     19 -- PQ812515.1
     20 -- OQ983818.1
     21 -- PV130052.1
     22 -- PQ782692.1
     23 -- PQ782438.1
     24 -- PQ782870.1
     25 -- PQ097984.1
     26 -- PQ782302.1
     27 -- PQ782679.1
     28 -- PQ454920.1
     29 -- PQ782693.1
     30 -- PQ656875.1

   Key to taxon bipartitions (saved to file "pseudo-16s.nxs.parts"):

   ID -- Partition
   ------------------------------------
    1 -- .*****************************
    2 -- .*............................
    3 -- ..*...........................
    4 -- ...*..........................
    5 -- ....*.........................
    6 -- .....*........................
    7 -- ......*.......................
    8 -- .......*......................
    9 -- ........*.....................
   10 -- .........*....................
   11 -- ..........*...................
   12 -- ...........*..................
   13 -- ............*.................
   14 -- .............*................
   15 -- ..............*...............
   16 -- ...............*..............
   17 -- ................*.............
   18 -- .................*............
   19 -- ..................*...........
   20 -- ...................*..........
   21 -- ....................*.........
   22 -- .....................*........
   23 -- ......................*.......
   24 -- .......................*......
   25 -- ........................*.....
   26 -- .........................*....
   27 -- ..........................*...
   28 -- ...........................*..
   29 -- ............................*.
   30 -- .............................*
   31 -- ........*....***.*.*..........
   32 -- .........*..........*.........
   33 -- .**********************.*.****
   34 -- .........*.*....*...*.*...*..*
   35 -- ...*..*.**.*.*****.****.*.****
   36 -- ........**.*.*****.****...*.**
   37 -- .***.*****.************.*.****
   38 -- .........*..........*.....*...
   39 -- ........*....***..............
   40 -- .************************.****
   41 -- .....................*......*.
   42 -- ........*....*................
   43 -- ..**.*****.************.*.****
   44 -- ......*.**.*.*****.****.*.****
   45 -- ..............**..............
   46 -- .*********.************.*.****
   47 -- .................*.*..........
   48 -- .......*....*.....*...........
   49 -- ................*............*
   50 -- ......*.**.*.*****.****...****
   51 -- ........**.*.*****.**.*...*..*
   52 -- .........*.*....*...***...*.**
   53 -- ........**.*.*****.****...****
   54 -- ......*....................*..
   55 -- ..*..*.*....*.....*...........
   56 -- .......*....*.................
   57 -- ..*....*....*.....*...........
   58 -- ...........*..........*.......
   59 -- ............*.....*...........
   60 -- ...........*....*.....*......*
   61 -- ........*....**...............
   62 -- ..*..*........................
   63 -- ........*....***.*............
   64 -- ....*.....*...................
   65 -- ...........*....*............*
   66 -- ..**..****.************.*.****
   67 -- ......*.................*..*..
   68 -- .......*..........*...........
   69 -- .........*.*....*...*.....*..*
   70 -- .**..*.*....*.....*...........
   71 -- .......................*.*....
   72 -- .........*.*....*...*.*...*...
   73 -- .........*.*........*.*...*...
   74 -- .........*.*....*...*.*...*.**
   75 -- .***.******************.*.****
   76 -- ......*.**.*.*****.****...*.**
   77 -- ......................*......*
   78 -- ...........*..........*......*
   79 -- ...*..*.................*..*..
   80 -- ...*....................*.....
   81 -- ......*.................*.....
   82 -- ...*.**.**.*.*****.****.*.****
   83 -- .........*......*...*.....*..*
   84 -- ........*.....**..............
   85 -- .............***..............
   86 -- ...........*....*.............
   87 -- ........*....***...*..........
   ------------------------------------

   Summary statistics for informative taxon bipartitions
      (saved to file "pseudo-16s.nxs.tstat"):

   ID   #obs      Probab.     Sd(s)+      Min(s)      Max(s)   Nruns
   ------------------------------------------------------------------
   31  480002    1.000000    0.000000    1.000000    1.000000    2
   32  480002    1.000000    0.000000    1.000000    1.000000    2
   33  478948    0.997804    0.002805    0.995821    0.999788    2
   34  474301    0.988123    0.000851    0.987521    0.988725    2
   35  473822    0.987125    0.011325    0.979117    0.995133    2
   36  473371    0.986185    0.014222    0.976129    0.996242    2
   37  471409    0.982098    0.011034    0.974296    0.989900    2
   38  466308    0.971471    0.009546    0.964721    0.978221    2
   39  430714    0.897317    0.004349    0.894242    0.900392    2
   40  390573    0.813690    0.003833    0.810980    0.816401    2
   41  378202    0.787918    0.009593    0.781134    0.794701    2
   42  354926    0.739426    0.002769    0.737468    0.741384    2
   43  352500    0.734372    0.012663    0.725418    0.743326    2
   44  310989    0.647891    0.004134    0.644968    0.650814    2
   45  300970    0.627018    0.004431    0.623885    0.630152    2
   46  288960    0.601997    0.006788    0.597198    0.606797    2
   47  283302    0.590210    0.014549    0.579923    0.600497    2
   48  271410    0.565435    0.016087    0.554060    0.576810    2
   49  257282    0.536002    0.019610    0.522135    0.549869    2
   50  256836    0.535073    0.001844    0.533769    0.536377    2
   51  238111    0.496063    0.016431    0.484444    0.507681    2
   52  205747    0.428638    0.016166    0.417207    0.440069    2
   53  191391    0.398730    0.001022    0.398007    0.399453    2
   54  183464    0.382215    0.013476    0.372686    0.391744    2
   55  180070    0.375144    0.003223    0.372865    0.377423    2
   56  177476    0.369740    0.004991    0.366211    0.373269    2
   57  177116    0.368990    0.009752    0.362094    0.375886    2
   58  175984    0.366632    0.010565    0.359161    0.374103    2
   59  168432    0.350899    0.004667    0.347599    0.354199    2
   60  142369    0.296601    0.007121    0.291565    0.301636    2
   61  134061    0.279293    0.003238    0.277003    0.281582    2
   62  124536    0.259449    0.005009    0.255907    0.262991    2
   63  121317    0.252743    0.010716    0.245166    0.260320    2
   64  120032    0.250066    0.014142    0.240066    0.260066    2
   65   94928    0.197766    0.007059    0.192774    0.202757    2
   66   91196    0.189991    0.001420    0.188987    0.190995    2
   67   82147    0.171139    0.010297    0.163858    0.178420    2
   68   81324    0.169424    0.005498    0.165537    0.173312    2
   69   76584    0.159549    0.013948    0.149687    0.169412    2
   70   73890    0.153937    0.008992    0.147579    0.160295    2
   71   73616    0.153366    0.003960    0.150566    0.156166    2
   72   70044    0.145924    0.012162    0.137324    0.154524    2
   73   69551    0.144897    0.004151    0.141962    0.147833    2
   74   68775    0.143281    0.003662    0.140691    0.145870    2
   75   67616    0.140866    0.001803    0.139591    0.142141    2
   76   63029    0.131310    0.006072    0.127016    0.135604    2
   77   58186    0.121220    0.001550    0.120124    0.122316    2
   78   57025    0.118802    0.001517    0.117729    0.119875    2
   79   56540    0.117791    0.009198    0.111287    0.124295    2
   80   56227    0.117139    0.001158    0.116320    0.117958    2
   81   53717    0.111910    0.001240    0.111033    0.112787    2
   82   53236    0.110908    0.002487    0.109150    0.112666    2
   83   52888    0.110183    0.006423    0.105641    0.114725    2
   84   52502    0.109379    0.001232    0.108508    0.110250    2
   85   51704    0.107716    0.000642    0.107262    0.108170    2
   86   50160    0.104500    0.005887    0.100337    0.108662    2
   87   47099    0.098123    0.004240    0.095125    0.101120    2
   ------------------------------------------------------------------
   + Convergence diagnostic (standard deviation of split frequencies)
     should approach 0.0 as runs converge.


   Summary statistics for branch and node parameters
      (saved to file "pseudo-16s.nxs.vstat"):

                                           95% HPD Interval
                                         --------------------
   Parameter      Mean       Variance     Lower       Upper       Median     PSRF+  Nruns
   --------------------------------------------------------------------------------------
   length[1]     0.003320    0.000005    0.000000    0.007508    0.002951    1.000    2
   length[2]     0.013557    0.000021    0.005620    0.022931    0.013067    1.000    2
   length[3]     0.004706    0.000005    0.000786    0.009138    0.004407    1.000    2
   length[4]     0.001226    0.000002    0.000000    0.003682    0.000843    1.000    2
   length[5]     0.005295    0.000012    0.000002    0.011763    0.004735    1.000    2
   length[6]     0.073147    0.000177    0.048771    0.099946    0.071947    1.002    2
   length[7]     0.005462    0.000021    0.000000    0.014499    0.004363    1.000    2
   length[8]     0.002577    0.000007    0.000000    0.007821    0.001750    1.000    2
   length[9]     0.003561    0.000006    0.000078    0.008499    0.002964    1.000    2
   length[10]    0.001354    0.000002    0.000000    0.004049    0.000936    1.000    2
   length[11]    0.046337    0.000093    0.028345    0.064901    0.045384    1.000    2
   length[12]    0.003570    0.000005    0.000000    0.007952    0.003181    1.000    2
   length[13]    0.005807    0.000021    0.000000    0.014542    0.004784    1.000    2
   length[14]    0.001084    0.000001    0.000000    0.003206    0.000757    1.000    2
   length[15]    0.001669    0.000003    0.000000    0.005049    0.001145    1.001    2
   length[16]    0.007698    0.000031    0.000140    0.018471    0.006383    1.000    2
   length[17]    0.020556    0.000113    0.000002    0.036740    0.021855    1.001    2
   length[18]    0.001469    0.000002    0.000000    0.004376    0.001033    1.000    2
   length[19]    0.013609    0.000030    0.004369    0.024837    0.012840    1.001    2
   length[20]    0.017437    0.000029    0.007500    0.029463    0.017147    1.000    2
   length[21]    0.001334    0.000002    0.000000    0.003953    0.000915    1.000    2
   length[22]    0.073970    0.000178    0.049719    0.100715    0.072929    1.000    2
   length[23]    0.005466    0.000008    0.000010    0.010774    0.005064    1.000    2
   length[24]    0.009777    0.000018    0.002184    0.018136    0.009260    1.000    2
   length[25]    0.006066    0.000010    0.001138    0.012388    0.005491    1.000    2
   length[26]    0.003117    0.000005    0.000000    0.007394    0.002668    1.000    2
   length[27]    0.006676    0.000010    0.001104    0.012819    0.006259    1.000    2
   length[28]    0.086025    0.000298    0.054912    0.120787    0.084388    1.000    2
   length[29]    0.006758    0.000024    0.000001    0.016171    0.005805    1.000    2
   length[30]    0.005264    0.000015    0.000038    0.012828    0.004376    1.000    2
   length[31]    0.028184    0.000075    0.012209    0.045239    0.027459    1.000    2
   length[32]    0.009578    0.000017    0.002612    0.017812    0.008981    1.000    2
   length[33]    0.023968    0.000049    0.011448    0.038382    0.023395    1.001    2
   length[34]    0.024615    0.000066    0.009344    0.041845    0.024170    1.000    2
   length[35]    0.018817    0.000032    0.008693    0.030330    0.018304    1.000    2
   length[36]    0.040637    0.000152    0.015143    0.065188    0.040416    1.000    2
   length[37]    0.021378    0.000047    0.008467    0.035071    0.020933    1.000    2
   length[38]    0.007313    0.000010    0.001726    0.013358    0.006932    1.000    2
   length[39]    0.005788    0.000010    0.000504    0.011841    0.005353    1.000    2
   length[40]    0.006545    0.000011    0.000583    0.013129    0.006067    1.000    2
   length[41]    0.011045    0.000035    0.000903    0.022677    0.010278    1.000    2
   length[42]    0.002443    0.000003    0.000000    0.005888    0.002076    1.000    2
   length[43]    0.006275    0.000011    0.000388    0.012631    0.005855    1.000    2
   length[44]    0.006051    0.000020    0.000001    0.014627    0.005210    1.000    2
   length[45]    0.002947    0.000005    0.000002    0.007152    0.002459    1.000    2
   length[46]    0.008756    0.000039    0.000002    0.020676    0.007666    1.000    2
   length[47]    0.003544    0.000006    0.000000    0.008338    0.003093    1.000    2
   length[48]    0.005215    0.000018    0.000000    0.013384    0.004243    1.000    2
   length[49]    0.015116    0.000088    0.000006    0.031329    0.014499    1.000    2
   length[50]    0.007638    0.000028    0.000000    0.017497    0.006867    1.000    2
   length[51]    0.010257    0.000028    0.000999    0.020736    0.009644    1.000    2
   length[52]    0.011011    0.000045    0.000001    0.023284    0.010312    1.000    2
   length[53]    0.014202    0.000106    0.000001    0.033910    0.012195    1.000    2
   length[54]    0.007880    0.000026    0.000000    0.017383    0.007060    1.000    2
   length[55]    0.002304    0.000003    0.000000    0.005937    0.001865    1.000    2
   length[56]    0.004983    0.000017    0.000000    0.012929    0.004021    1.000    2
   length[57]    0.002176    0.000003    0.000000    0.005315    0.001836    1.000    2
   length[58]    0.003625    0.000007    0.000002    0.008755    0.003092    1.000    2
   length[59]    0.004937    0.000016    0.000000    0.012868    0.003984    1.000    2
   length[60]    0.002926    0.000007    0.000001    0.007891    0.002249    1.002    2
   length[61]    0.004010    0.000010    0.000003    0.010015    0.003354    1.000    2
   length[62]    0.002527    0.000004    0.000000    0.006458    0.002047    1.000    2
   length[63]    0.003442    0.000009    0.000000    0.009198    0.002653    1.001    2
   length[64]    0.005697    0.000020    0.000001    0.014346    0.004773    1.000    2
   length[65]    0.002487    0.000004    0.000001    0.006279    0.002074    1.000    2
   length[66]    0.002378    0.000004    0.000000    0.006496    0.001803    1.001    2
   length[67]    0.005052    0.000019    0.000000    0.013501    0.003918    1.000    2
   length[68]    0.003065    0.000008    0.000000    0.008936    0.002203    1.000    2
   length[69]    0.002442    0.000004    0.000000    0.006441    0.001935    1.002    2
   length[70]    0.005189    0.000011    0.000005    0.011391    0.004705    1.000    2
   length[71]    0.003344    0.000004    0.000003    0.007342    0.002999    1.001    2
   length[72]    0.008125    0.000051    0.000002    0.022697    0.006013    1.000    2
   length[73]    0.002801    0.000006    0.000000    0.007776    0.002100    1.001    2
   length[74]    0.011191    0.000030    0.000976    0.021417    0.010647    1.001    2
   length[75]    0.003331    0.000009    0.000001    0.009119    0.002529    1.000    2
   length[76]    0.006169    0.000021    0.000000    0.014743    0.005314    1.000    2
   length[77]    0.003632    0.000007    0.000001    0.008661    0.003096    1.000    2
   length[78]    0.003353    0.000006    0.000000    0.008292    0.002793    1.000    2
   length[79]    0.004730    0.000016    0.000018    0.011102    0.003928    1.004    2
   length[80]    0.001560    0.000002    0.000000    0.004471    0.001129    1.000    2
   length[81]    0.004105    0.000015    0.000001    0.011960    0.002957    1.001    2
   length[82]    0.001634    0.000003    0.000001    0.004855    0.001159    1.000    2
   length[83]    0.002280    0.000004    0.000000    0.006436    0.001682    1.002    2
   length[84]    0.001282    0.000002    0.000000    0.003869    0.000863    1.000    2
   length[85]    0.001207    0.000001    0.000000    0.003567    0.000848    1.000    2
   length[86]    0.002483    0.000004    0.000003    0.006288    0.002038    1.000    2
   length[87]    0.001604    0.000003    0.000001    0.004824    0.001093    1.000    2
   --------------------------------------------------------------------------------------
   + Convergence diagnostic (PSRF = Potential Scale Reduction Factor; Gelman
     and Rubin, 1992) should approach 1.0 as runs converge. NA is reported when
     deviation of parameter values within all runs is 0 or when a parameter
     value (a branch length, for instance) is not sampled in all runs.


   Summary statistics for partitions with frequency >= 0.10 in at least one run:
       Average standard deviation of split frequencies = 0.006764
       Maximum standard deviation of split frequencies = 0.019610
       Average PSRF for parameter values (excluding NA and >10.0) = 1.000
       Maximum PSRF for parameter values = 1.004


   Clade credibility values:

   Subtree rooted at node 48:

                   /----------------------------------------------- PV256206.1 (2)
                   |
                   |    /------------------------------------------ PQ897219.1 (3)
                   |    |
                   |    |    /------------------------------------- PV111332.1 (4)
                   |    |    |
                   |    |    |          /-------------------------- PP237255.1 (7)
                   |    |    |          |
                   |    |    |          |                    /----- PQ554712.1 (9)
                   |    |    |          |               /-74-+
                   |    |    |          |               |    \----- OR430114.1 (14)
                   |    |    |          |         /--90-+
              /-98-+    |    |          |         |     |    /----- OQ891268.1 (15)
              |    |    |    |          |         |     \-63-+
              |    |    |    |          |    /-100+          \----- OR497730.1 (16)
              |    |    |    |          |    |    |
              |    |    |    |          |    |    |          /----- PP082086.1 (18)
              |    |    |    |          |    |    \----59----+
              |    |    |-99-+          |    |               \----- OQ983818.1 (20)
              |    |    |    |          |    |
              |    |    |    |          |    |               /----- PV076873.1 (10)
              |    |    |    |          |    |          /-100+
              |    |    |    |     /-54-+    |          |    \----- PV130052.1 (21)
              |    |    |    |     |    |    |    /--97-+
              |    \-73-+    |     |    |    |    |     \---------- PQ782679.1 (27)
              |         |    |     |    |-99-+    |
              |         |    |     |    |    |    |---------------- PQ782809.1 (12)
              |         |    |     |    |    |    |
              |         |    |     |    |    |-99-+          /----- PQ782653.1 (17)
              |         |    |     |    |    |    |----54----+
              |         |    |     |    |    |    |          \----- PQ656875.1 (30)
        /--60-+         |    \--65-+    |    |    |
        |     |         |          |    |    |    \---------------- PQ782438.1 (23)
        |     |         |          |    |    |
        |     |         |          |    |    |               /----- PQ782692.1 (22)
        |     |         |          |    |    \-------79------+
        |     |         |          |    |                    \----- PQ782693.1 (29)
        |     |         |          |    |
        |     |         |          |    \-------------------------- PQ454920.1 (28)
        |     |         |          |
        |     |         |          \------------------------------- PQ097984.1 (25)
        |     |         |
   --100+     |         |------------------------------------------ AB603655.1 (6)
        |     |         |
        |     |         |                                    /----- PQ656938.1 (8)
        |     |         |                                    |
        |     |         \-----------------57-----------------+----- PV195286.1 (13)
        |     |                                              |
        |     |                                              \----- PQ812515.1 (19)
        |     |
        |     \---------------------------------------------------- PQ797033.1 (5)
        |
        \---------------------------------------------------------- PV256072.1 (11)

   Root part of tree:

   /--------------------------------------------------------------- PQ782784.1 (1)
   |
   |--------------------------------------------------------------- PQ782302.1 (26)
   +
   |                               /------------------------------- (48)
   \---------------81--------------+
                                   \------------------------------- PQ782870.1 (24)


   Phylogram (based on average branch lengths):

   /- PQ782784.1 (1)
   |
   |- PQ782302.1 (26)
   |
   |                /---- PV256206.1 (2)
   |                |
   |                |/-- PQ897219.1 (3)
   |                ||
   |                ||     / PV111332.1 (4)
   |                ||     |
   |                ||     |  /-- PP237255.1 (7)
   |                ||     |  |
   |                ||     |  |                     /- PQ554712.1 (9)
   |                ||     |  |                    /+
   |                ||     |  |                    |\ OR430114.1 (14)
   |                ||     |  |                   /+
   |          /-----+|     |  |                   ||/ OQ891268.1 (15)
   |          |     ||     |  |                   |\+
   |          |     ||     |  |           /-------+ \-- OR497730.1 (16)
   |          |     ||     |  |           |       |
   |          |     ||     |  |           |       |/ PP082086.1 (18)
   |          |     ||     |  |           |       \+
   |          |     ||-----+  |           |        \----- OQ983818.1 (20)
   |          |     ||     |  |           |
   |          |     ||     |  |           |           / PV076873.1 (10)
   |          |     ||     |  |           |        /--+
   +          |     ||     |/-+           |        |  \ PV130052.1 (21)
   |          |     ||     || |           |      /-+
   |          |     \+     || |           |      | \-- PQ782679.1 (27)
   |          |      |     || |-----------+      |
   |          |      |     || |           |      |- PQ782809.1 (12)
   |          |      |     || |           |      |
   |          |      |     || |           |------+   /------ PQ782653.1 (17)
   |          |      |     || |           |      |---+
   |          |      |     || |           |      |   \- PQ656875.1 (30)
   |        /-+      |     \+ |           |      |
   |        | |      |      | |           |      \- PQ782438.1 (23)
   |        | |      |      | |           |
   |        | |      |      | |           |  /--------------------- PQ782692.1 (22)
   |        | |      |      | |           \--+
   |        | |      |      | |              \-- PQ782693.1 (29)
   |        | |      |      | |
   |        | |      |      | \------------------------- PQ454920.1 (28)
   |        | |      |      |
   |        | |      |      \-- PQ097984.1 (25)
   |        | |      |
   | /------+ |      |--------------------- AB603655.1 (6)
   | |      | |      |
   | |      | |      | / PQ656938.1 (8)
   | |      | |      | |
   | |      | |      \-+- PV195286.1 (13)
   | |      | |        |
   \-+      | |        \--- PQ812515.1 (19)
     |      | |
     |      | \- PQ797033.1 (5)
     |      |
     |      \------------- PV256072.1 (11)
     |
     \-- PQ782870.1 (24)

   |-------------| 0.050 expected changes per site

   Calculating tree probabilities...

   Credible sets of trees (210198 trees sampled):
      50 % credible set contains 45301 trees
      90 % credible set contains 162198 trees
      95 % credible set contains 186198 trees
      99 % credible set contains 205398 trees
```

# 4/22/25

- ASTRAL
	- Pros: Easy install, handles gene duplication/loss
	- Cons: Command line only, needs multiple genes/markers to work
	- Considerations: The outcome here is dependant on what we do in Mr. Bayes

Command list

>java -jar astral.5.7.1.jar -i pseudo-16s.nxs.con.tre [!Error; if only it were so simple]

WHEN RUNNING SUMT IN MR. BAYES, ADD conformat=simple!!!
My data may not be able to be run due to it using a single gene so I'm uing the example set

>java -jar astral.5.7.1.jar -q test_data/simulated_14taxon.default.tre -i test_data/simulated_14taxon.gene.tre -o test_data/simulated_scored.tre 2> test_data/simulated_scored.log
[data stored in the new file specified in the -o]
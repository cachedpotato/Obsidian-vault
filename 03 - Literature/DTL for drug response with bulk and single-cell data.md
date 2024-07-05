---
tags:
  - DeepLearning
  - DrugResponse
  - RNAseq/scRNAseq
---
Review Date: 2024-04-29
Author:
Link:

## Abstract
- Drug screening data from massive bulk gene expression DB can be analyzed to determine optimal clinical application of cancer drugs
- scRNA-seq provides insights into improving therapeutic effectiveness
- scRNA-seq helps the study of heterogeneity of drug responses
- scDEAL: harmonization of bulk and single-cell *RNA*seq data
- Integrated gradient feature interpretation to infer the signature genes 

## Main Body
cancer drug treatments suffer from low efficacies and high relapse rates
- cancer heterogeniety > differentiated response > cancer relapse

scRNA-seq can help analyze heterogeniety by virtue of being a cell-level analysis

bulk data cannot be directly user for larger scale and highly intricate single cell data
- computational methods to infer cancer drug response are needed
- insufficient training power due to limited number of benchmarked data remains a problem
- [[Deep Transfer Learning]] may help alleviate this problem
- DTL has been used to leverage multiple bulk data sources for cancer drug response predictions > scDEAL

### scDEAL summary
[[Domain-Adaptive Neural Network]] to predict drug responses from bulk scRNA data
establish bridge among drug sensitivity, gene features in single cells & gene features in bulk samples


Key Points:
-  can use a large amount of bulk-level drug response
-  to account for data-structure differences, scDEAL harmonizes single cell and bulk embeddings
-  includes cell cluster labels for loss function regularization to avoid losing heterogeniety
-  integrated gradient (IG) interpretation infers signature genes of drug response predictions
	identify crucial signatures by tracing and accumulating IG

### scDEAL framework
![[스크린샷 2024-04-29 162237.png]]
scDEAL models relations between gene expression and drug response at bulk level
	annotations for cell lines available here
shared low dimensional feature identified in order to harmonize 
- drug response - bulk RNA
- scRNA - bulk RNA 

DTL model is trained to learn the solution to the two relations through meta relation of:
- gene expresion at sc level
- gene expression at bulk level
- drug response in DTL model

the 5 steps of scDEAL
![[스크린샷 2024-04-29 162441.png]]
1. extract bulk gene features
to add random noise to input
$$ X_{b}'' = D_{b}(E_{b}(X'_{b})) $$ where D: decoder, B: encoder

2. predicting drug response in each bulk cell line
- uses features extracted in step 1
$$ Y = P(E_{b}(X_{b})) $$
$$ min(loss_{class}(P, Y_{b}, Y_{b}^{0})) = min(CrossEntropy(Y_{b}, Y_{b}^{0})) $$
3. extract single cell gene features
$$ X_{s}'' = D_{c}(E_{s}(x_{s})) $$

4.  jointly training and updating all the models in previous steps
$$ loss_{MMD}(E_{b}(X_{b}), E_{s}(X_{s})) = |\frac{1}{n}\sum_{i=1}^n\phi(x_b^i) - \frac{1}{m}\sum_{j=1}^m\phi(x_s^j)|_H $$
where x are data vectors of different dimensions (bulk and single cell)
H: Universal Reproducing Kernel Hilbert Space (RHKS)
norm $$|.|_H$$ measures the distance between two vectors of different dimensions

DaNN model is trained to update two gene extractors and predictor P
$$ min loss_{DaNN}(X_b, X_s, E_b, E_s, P) = min(loss_{class}(P, Y_{b}, Y_{b}^{0}) + \alpha*loss_{MMD}(E_{b}(X_{b}), E_{s}(X_{s})) + \beta*regularizer) $$
$$regularizer = \sum_{c in CC}^{Cosine_{similarity}}(X_s)$$

where CC is cell cluster categories

5.  transferring and applying the trained model to scRNA-seq data to predict DR
Xs as input, predictability scores Ys for each cell

noise characteristics in bulk RNA-seq and scRNA-seq data quite distinct
- used DAE instead of VAE or AE

### Results - raw stats
Tested in 6 different datasets
Average score

| AUROC | AP    | precision | recall | AMI   | AMI   | ARI   |
| ----- | ----- | --------- | ------ | ----- | ----- | ----- |
| 0.892 | 0.898 | 0.944     | 0.926  | 0.899 | 0.538 | 0.608 |

UMAP
Well aligned with ground truth

Elucidating the rationale of the scDEAL - perturbations
1.  Transfer Learning test
- train model only on bulk data
- scDEAL shows 19% performance increase than the one without single cell data

2. evaluating the training power of transfer model
How much relies on bulk resource?
- GDSC/CCLE/both DB for training
- better performance when both were used

3. can DAE help reduce loss of single cell heterogeneity?
- use common AE/VAE
- DAE showed best performance 

4. Does regularization with cell cluster annotations reduce loss of heterogeneity?
- no regularizer showed lower performance

5. Have relations between gene expression and drug response been properly learned?
- IG analysis
- based on accumulation of gradients of neurons
$$ IG_i(x)::= (x_i-x_i')\int_{\alpha=0}^{1}\frac{{\partial F}(x' + \alpha(x-x'))}{\partial x_i} d $$

sampling methods and bottleneck dimensions were the most important hyperparams to adjust

6. correlation of DEG with ground truth
random sampling: R2 value of 0.001 - meaningful statistics that shows how significant the correlation is.

### Results - implications
scDEAL can identify critical genes responsible for drug response
Critical Genes
- padj < 0.05
- log-fold changge <0.1
- cell percentage in comparison group > 0.2
predicted CGs showed strong correlations with field studies
ex) for IB-reatment of Cisplatin treatment, resistant CGs posessed anti-apoptotic activity
ex) GO enrichment analysis also showed enrichment in DNA repair

scDEAL drug response prediction is highly correlated with [[Pseudotime analysis]]
- trajectory trend starting from DMSO samples towards 1000-ml I-BET treated samples


## Discussion
scDEAL in drug development
- predict drug responses and link gene signatures with treatment effects
- CGs are potential target signatures for CRISPR
- can be applied to existing non-drug treated scRNA seq data

Accuracy of the prediction results in scDEAL varies depending on the collection of bulk gene expression

prediction across different species remains a challenge
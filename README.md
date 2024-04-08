# Customer Segmentation of an e-commerce website

![bannière](https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/3405999d-40e0-4a0a-9e8c-536c8103a05e)

## Context

Olist, a Brazilian company that offers an online sales solution, wants to segment its customers for its e-commerce service in order to define user profiles and adapt its targeted communication campaigns.

The objective is therefore to understand the different types of customers through their behavior, their habits and their personal data. The actionable description of the segmentation and its underlying logic must be understandable to the marketing department.

A maintenance contract proposal is finally drawn up, based on a cluster stability analysis over time.

## Data

Data are available [here](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).

The information is distributed into 9 datasets, grouping information on customers, their location, the type of products purchased, money transfers, reviews left, sellers.

## Segmentation method

The method used for the client segmentation is the RFM method, which makes it possible to segment its customer base according to purchase intention and to target them effectively.

The name RFM comes from the type of features considered for the segmentation:

- **Recency**: date of the last purchase. Note that it is assumed that someone who has purchased recently on the website is more likely to return to order more.
- **Frequency**: number of purchases made over a given period. The more regularly a customer buys from the site, the more likely they are to buy again. We analyze here the level of loyalty.
- **Monetary**: sum of purchases accumulated over a given period. Large buyers respond better than small ones. Here we measure customer value.

Other features can be added to strengthen the model, such as

- Average number of items per basket
- Average review score

This method will allow, among other things, to:

- Save unnecessary costs, by setting aside customers with little or no activity.
- Increase significantly marketing emails impact by sending them to loyal customers to reinforce their loyalty.
- Follow up with inactive customers via a re-engagement campaign to recapture their interest.

## Exploratory Data Analysis

### Single feature analysis
#### Recency

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/3f753e71-b6aa-47e4-8de3-85aa86cd1707" height="400">

Recency distribution appears to be between 44 and 772 days.

#### Frequency

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/1d1800b4-59f2-42cd-b8a7-5b61a69491d0" height="400">

A large majority (97%) of customers have only ordered once.

#### Monetary

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/845dddf3-85fa-4e59-98a9-277af9e4ecbe" height="400">

The majority of the amounts are below the 50 BRL mark. However, standard deviation is important.

#### Review Score

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/47ef27d5-c181-46dc-a6c3-732fb269b60a" height="400">

Review score have a majority of 5.

#### Average number of items

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/aed3072a-72c2-4f1a-9637-327ccc0b42de" height="400">

### Bivariate Analysis

Faced with the possibility of adding features to strengthen the segmentation, it is important to ensure that the added variables are not correlated to those already selected.

<img src="https://github.com/pgrondein/customer_segmentation_e-commerce/assets/113172845/eb7deda8-dbb6-4b0b-a77f-ff74b8dd7324" height="400">

None of the features seem correlated.

## Model

### Hierarchical clustering

Agglomeration of the closest individuals/clusters into fewer and fewer clusters. The choice of the optimum number of clusters is done visually.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/c7883ccb-c072-4fc7-b981-0e6a0bd66540" height="400">

However, the algorithmic complexity of this type of model is heavy and not suitable for a large dataset, such as the one studied here.

### DBScan

Making of clusters is done by neighborhood density, which must be defined in advance.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/ba47c61f-59e1-4d97-b008-0f776ecf8b3e" height="400">

The chosen density is 100. Several neighborhood sizes have been tested. However, this type of model is not suitable for densities of individuals that are too low, as in the dataset studied here.

### K-Means

Groups observations with high similarity.
The optimal number of clusters must be determined beforehand.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/fa867c44-dfd9-4a25-ac2f-6ea972e389f4" height="400">

The model is tested for different numbers of clusters, and the SSE (Sum of Squared Errors) is calculated each time. The optimal number of clusters is selected at the “bend” of the curve, here 5.

It is also possible to determine the optimal number of clusters thanks to the silhouette coefficient.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/7243a4a4-6c97-4e62-b06c-cf0ca49155bf" height="400">

In order to obtain clusters of equivalent size and distribution, we can see that the optimal number of clusters seems to be 5. 
We therefore set k = 5 for the model.

## Results

### Clusters 

| Clusters | Users | % users | Average Recency (days) | Average Frequency | Average Monetary | Average number of items | Average review score |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| `1`  | 11295 | 12 | 441 +/-  95 | 1.032 +/- 0.19 | 158 +/- 206 | 1.09 +/- 0.32 | 3.7 +/- 0.48 |
| `2`  | 15240 | 16 | 182 +/- 74 | 1.044 +/- 0.24 | 161 +/- 208 | 1.08 +/- 0.33 | 3.6  +/- 0.46 |
| `3`  | 31550 | 33 | 170 +/- 72 | 1.038 +/- 0.23 | 160 +/- 210 | 1.08 +/- 0.29 | 4.9 +/- 0.04 |
| `4`  | 13273 | 14 | 289 +/- 144 | 1.020 +/- 0.15 | 193 +/- 293 | 1.21 +/- 0.49 | 1.2 +/- 0.41 |
| `5`  | 23362 | 25 | 436 +/- 95 | 1.030 +/- 0.19 | 163 +/- 227 | 1.09 +/- 0.30 | 5.0 +/- 0.03 |

### Maintenance contract

It is necessary to find the optimal update frequency for the stability of the segmentation system (distribution of users into stable groups). For this, we use the ARI (Adjusted Rand Index), which gives a measure of the group stability, and we calculate the average of this value according to the update period.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/0081a6be-9a5b-4949-a092-c34119931051" height="400">

## Conclusion

It is possible to identify three customer profiles:

- Already loyal customers: groups 2 and 3 come often, spend less but regularly and seem satisfied with the site
- High-potential customers: group 4 came the most recently, is not yet loyal but has spent more than the others, with a fairly low satisfaction rating. Customers to follow up.
- Two groups of customers of little interest for our study, to be left aside.

The recommended update frequency of the segmentation system is 15 days, which can be pushed to 7 days for better stability.

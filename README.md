# Customer Segmentation of an e-commerce website

![bannière](https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/ec65bafc-2f4a-4ccd-8067-8194bb38d778)

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

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/e0e944dc-2bc1-4f46-85c6-066b29568efc" height="400">

Recency distribution appears to be between 44 and 772 days.

#### Frequency

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/9ab1c6a1-451b-4988-b56f-27fdbf4f323b" height="400">

A large majority (97%) of customers have only ordered once.

#### Monetary

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/6262f5c6-7fe7-48d1-bf54-98a1e5f223e0" height="400">

The majority of the amounts are below the 50 BRL mark. However, standard deviation is important.

#### Review Score

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/ec3a0bb0-0919-4792-94f6-839c3e55a1ac" height="400">

Review score have a majority of 5.

#### Average number of items

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/8416dc4b-e465-473c-9981-34f1a7cc177e" height="400">

### Bivariate Analysis

Faced with the possibility of adding features to strengthen the segmentation, it is important to ensure that the added variables are not correlated to those already selected.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/5e1a8133-2a86-41ff-9606-c143a077f968" height="400">

None of the features seem correlated.

## Model

### Hierarchical clustering

Agglomeration of the closest individuals/clusters into fewer and fewer clusters. The choice of the optimum number of clusters is done visually.

<img src="https://github.com/pgrondein/client_segmentation_e-commerce/assets/113172845/c7883ccb-c072-4fc7-b981-0e6a0bd66540" height="400">





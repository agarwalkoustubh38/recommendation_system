# Product-Recsys <a href="http://product-recsys.herokuapp.com/" target="_blank">applink</a>
[![Generic badge](https://img.shields.io/badge/API-Fastapi-<COLOR>.svg)](https://shields.io/) [![Generic badge](https://img.shields.io/badge/License-MIT-<COLOR>.svg)](https://shields.io/) 

Using the customer orders and rating data from [Olist E-Commerce Public Dataset](https://www.kaggle.com/olistbr/brazilian-ecommerce), which has information about 100k orders made at multiple marketplaces in Brazil from 2016 to 2018, I trained 3 models that generate product recommendations.

*NOTE* 

*- The granularity of orders in the dataset is at product category level, thus recommendations are product categories in the true sense.*

*- The application is deployed on a free server that goes into sleep mode, expect a ~10 seconds delay in loading, If it takes more than 10 seconds, try refreshing! :)*

<img src="https://github.com/abhijitpai000/product-recsys/blob/main/sample-recsys2.gif">


### Model Training
The model training pipeline is in the [product-recsys-training](https://github.com/abhijitpai000/product-recsys-training) repository.

# Architecture
*Architecture Diagram*
<img src="https://github.com/abhijitpai000/product_recommendation_system/blob/main/figures/backend_architecture.png?raw=true" alt="backend" width="918" height="429"/>

The website is divided into 3 sections.
## 1. Top Trending
**Demographic Filtering** - Recommends highest rated products in the dataset.

**Method** - Uses [IMDB weighted average formula](https://help.imdb.com/article/imdb/track-movies-tv/ratings-faq/G67Y87TFYYP6TWAV#calculatetop) and recommends highest rated products.

## 2. Similar Products
**Item based collaborative filtering** - Takes user input of one product and recommends 5 similar products.
      
**Method** - Computes cosine similarity between selected product and others based on historical ratings given by customers using KNN Basic algorithm.

## 3. Products you might like
**User based collaborative filtering** - Takes user input & rating of one product and recommends 3 products based on the rating given for the selected product.
      
**Method** -   Approximates the user's taste by running two algorithms in the backend, first computes the most similar user who has sufficient historical data, and second, makes recommendations based on their taste.


# Repository Structure
    .
    ├── backend
        └── models                                
            ├── similar_items_algo.pkl            # Trained model from product-recsys-training repo. (not included here)
            └── user_predictions_algo.pkl         # Trained model from product-recsys-training repo. (not included here)
        └── src
            ├── config.py                         # database configuration. (not included here)
            ├── trending.py                       # Returns top ten trending products.
            ├── item_rec_sys.py                   # Returns similar product recommendations using the ../models/similer_items_algo.pkl
            └── user_rec_sys.py                   # Returns similar product recommendations using the ../models/user_predictions_algo.pkl
    ├── frontend                                  # Front-end and client-side scripts.
    ├── main.py                                   # Fastapi API
    ├── requirements.txt                          
    ├── LICENSE
    └── README.md

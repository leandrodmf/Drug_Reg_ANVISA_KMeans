# Drug_Reg_ANVISA
**Project Status**: [Current status: In progress, completed, etc.]

## **ATTENTION**
> Run the script in a **Python** environment, but use responsably. Mistakes can be commited.
  ### Dependencies (libraries used):
    import pandas as pd
    import scipy.stats as stats
    from scipy.stats import ttest_ind
    import matplotlib.pyplot as plt
        

  
##  1 Project Overview

This project aims to explore the Brazilian pharmaceutical market by analyzing data on drug registrations from the Brazilian Health Surveillance Agency (ANVISA). Augmenting analysis information with ranking of Billion Brazilian Company and Top 20 drug unit sales.

ANVISA DATABASE: Medicines Registered in Brazil

> _"The open drug registration database is a data intelligence project that extracts information from the Datavisa system to list products that have been registered by Anvisa, including those whose registration is already valid or canceled/expired, as reported on the Agency's consultation portal."_

> URL: https://dados.gov.br/dados/conjuntos-dados/medicamentos-registrados-no-brasil

Billionare companies

> URL: https://cdpipharma.com.br/materias/brasil-tem-18-industrias-farmaceuticas-bilionarias/

Top 20 Unit sales companies

> URL: https://www.abradilan.com.br/mercado/das-20-maiores-farmaceuticas-do-brasil-17-sao-nacionais/

 The dataset includes information about:
- 'PRODUCT_TYPE';
- 'PRODUCT_NAME';
- 'PROCESS_END_DATE';
- 'REGULATORY_CATEGORY';
- 'PRODUCT_REGISTRATION_NUMBER';
- 'REGISTRATION_EXPIRATION_DATE';
- 'PROCESS_NUMBER';
- 'THERAPEUTIC_CLASS';
- 'REGISTRATION_HOLDER_COMPANY';
- 'REGISTRATION_STATUS';
- 'ACTIVE_INGREDIENT'.

## 2 Project guideline
- There is a relationship between the number of records and the company's sales or value?

- Can the portfolio group the companies?

- Can we analyze the competitive landscape in the pharmaceutical market? Are able to identify market niches?

## 3 Project Deliverables

**3.1 Data Cleaning**

The dataframe consists of 31317 entries, divided into 11 nominal categorical variables.

Concerning the auxiliary information for the companie’s value and sales, the data were selected considering only a valid register until the year of 2022. Some companies were evaluated separately, due to names and holders that differed from the names in the tables.

Companies’ value and sales tables were organized adding the information of the drug register number. Was kept separate due to different information. Some companies were evaluated separately, due to names and holders that differed from the names in the tables.

**3.2 Exploratory Data Analysis**

**3.2.1 Hypothesis testing**

Thesis #1

$H_0 :$ The most valuable companies have more medicines registers.\
$H_1 :$ The medicines registers number have no relationship to company value.\

Thesis #2

$H_0 :$ Companies with the highest sales volume have the most of the medicines registers.\
$H_1 :$ Companies with the highest sales volume do not have the highest number of drug registrations.

Using the Independent T-Test, that assumes the population presents identical variance,  considering that 2 independent samples have identical average (expected) values, the results presented suitable, with the p-value of 0.99 and 0.96 for registers number against value and sales, respectively.

However, the hypothesis leads to considering a correlation between the variables, so were evaluated using Pearson correlation coefficient and p-value for testing no correlation. As results:
Thesis #1 -  We fail to reject the null hypothesis. There is not enough evidence to conclude that there is a correlation between 'company value' and '#Registers';
Thesis #2 - We reject the null hypothesis. There is a correlation between 'sales' and '#Registers'.

 **3.2.2 Clustering Analysis**

The aim was to evaluate how clustering analysis works with these categorical data. KMeans was selected to work without the labels of the data, in a attempt to cluster the companies considering the Registration Holder Company, Regulatory Category (RegCat) and Therapeutic Class (TClass) information.

Initially, the dataframe with the information was transformed in a dummy matrix and grouped by Company, having 343 lines (companies) and 522 columns (9 RegCat and 522 TClass). Then scaled. But result in too much information for a simple model, and couldn't be suitable to clustering.

To build a model with parsimony, only RegCat were used, but didn’t presented informative clusters. So Principal Component Analysis (PCA) were performed to preserve the variance when reducing the dimensionality of the data. The resulting KMeans model presented suitable to cluster the companies concerning the portfolio as Regulatory Category.

Model Mistake

However, the silhouette value achieved for the used KMeans model was 0.64, which leads to some samples could be matched to neighboring clusters. EMS and Prati-Donaduzzi was clustered in **Cluster 0**; and Neo Química (Brainfarma) remains in Cluster 2. But verifying their profile belongs to Cluster 2, of the companies with a high register number, predominantly of generic registers. 

Findings

The most valued companies belongs to Cluster 1, which mainly have reference (new) drug registers. Nevertheless, the Top Sales companies are included in Cluster 2, maybe because the high number of registers permits them to achieve high sales values. Although, a company value is presented to be more related to innovative products, demonstrating the predominance of multinational companies, in contrast to the Brazilian ones, which represent the majority in unit sales.

## Acknowledgements

ANVISA for the dataset.

## License

[![Licence](https://img.shields.io/github/license/Ileriayo/markdown-badges?style=for-the-badge)](./LICENSE)
<hr>
<hr>

## Contact

[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/leandrodmf/)

![Gmail](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)(leandrodemouraf@gmail.com)

## Disclaimer

This project is for research and educational purposes only. The findings should not be considered financial or investment advice.



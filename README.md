# A2 - Bias In Data

[![Contributors][contributors-shield]][contributors-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

## About The Project

The goal of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries. We combine a dataset of Wikipedia articles with a dataset of country populations, and use a machine learning service called ORES to estimate the quality of each article.

There are several steps involved in this project:
1. Data Collection
   1. [Politicians by Country from the English-language Wikipedia](https://figshare.com/articles/dataset/Untitled_Item/5513449)
   2. [World Population Dataset](https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit#gid=283125346)
2. Clean the Data
   1. There are some empty rows and irrelevant columns that are cleaned up
3. Collect Predictions
   1. We use the [ORES](https://github.com/wikimedia/ores) model to make predictions for each article in the dataset
4. Combine the 2 datasets
5. Analyze and transform the data
6. Present the results

The analysis will consist of a series of tables that show:
1. the countries with the greatest and least coverage of politicians on Wikipedia compared to their population.
2. the countries with the highest and lowest proportion of high quality articles about politicians.
3. a ranking of geographic regions by articles-per-person and proportion of high quality articles.

The following is the structure of the directory and files present:
```
.
├── LICENSE
├── README.md
├── data
│   ├── errors
│   │   ├── missing_prediction_revids.csv #missing predictions rev_ids
│   │   └── wp_wpds_countries-no_match.csv #unmerged countries
│   ├── processed
│   │   ├── politicians_country.csv #cleaned politicians by country data
│   │   ├── world_population_country_level.csv #cleaned world population (by country) data
│   │   ├── world_population_region_level.csv #cleaned world population (by region) data
│   │   └── wp_wpds_politicians_by_country.csv #merged cleaned data
│   └── raw
│       ├── WPDS_2020_data.csv #world population data
│       └── page_data.csv #politicians by country data
└── src
    └── hcds-a2-bias.ipynb #source code

```

## API Documentation

To make the predictions, we use the ORES scoring interface. Specifically, we use the following API:

1. [Scores Context](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context)
   1. This route provides access to all `{models}` within a `{context}`. This path is useful for either exploring information about `{models}` available within a `{context}` or scoring one or more `{revids}` using one or more `{models` at the same time.
   2. Specifically, we obtain the `prediction` from the response of the API. This prediction can be one of the following categories:
      * FA - Featured article
      * GA - Good article
      * B - B-class article
      * C - C-class article
      * Start - Start-class article
      * Stub - Stub-class article

## Dataset

Once the dataset is cleaned and the predictions are obtained, we merge the 2 datasets and output a [CSV](https://github.com/sharma-apoorv/data-512-a2/blob/master/data/processed/wp_wpds_politicians_by_country.csv) file with the following schema:


| Column Name             | Description                                     |
|-------------------------|-------------------------------------------------|
| country                    | This is the country which the article belongs to |
| article_name                   | The name/title of the article  |
| revision_id     | A unique number that identifies the article |
| article_quality_est. | The ORES prediction of the quality of the article |
| population  | The population of the country |

## Results

For the analysis, we attempt to answer the following 6 questions:
1. Top 10 countries by coverage: 10 highest-ranked countries in terms of number of politician articles as a proportion of country population
2. Bottom 10 countries by coverage: 10 lowest-ranked countries in terms of number of politician articles as a proportion of country population
3. Top 10 countries by relative quality: 10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
4. Bottom 10 countries by relative quality: 10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality
5. Geographic regions by coverage: Ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population
6. Geographic regions by coverage: Ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality
## Dependencies

[Anaconda](https://www.anaconda.com/) was used to maintain and install project dependencies. Additionally, a [requirements.txt](https://github.com/sharma-apoorv/data-512-a2/blob/main/requirements.txt) file has been provided to install all dependencies used in the notebook. 

## Usage

The repo can be cloned using the following command:
```
git clone https://github.com/sharma-apoorv/data-512-a2.git
```

The dependencies can be installed into an environment using the following command:
```
conda create --name <envname> --file requirements.txt
```

The environment is activated as follows:
```
conda activate <envname>
```

Lastly, the jupyter notebook kernel can be started using the following command:
```
jupyter-notebook
```

Executing the above command will open a link in the browser. Navigate to the notebook and click on "Run All" in the notebook to execute the commands.

## License

Distributed under the MIT License. See `LICENSE.md` for more information.

The *Politicians by Country from the English-language Wikipedia* is subject to a [creative commons licence](https://creativecommons.org/licenses/by/4.0/)

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/sharma-apoorv/data-512-a2.svg?style=for-the-badge
[contributors-url]: https://github.com/sharma-apoorv/data-512-a2/graphs/contributors
[license-shield]: https://img.shields.io/github/license/sharma-apoorv/data-512-a2.svg?style=for-the-badge
[license-url]: https://github.com/sharma-apoorv/data-512-a2/blob/main/LICENSE.md
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/sharmavapoorv/
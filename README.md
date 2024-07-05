# Walmart-Sales-Prediction
The project focused on analyzing Walmart's sales data to derive insights and build predictive models. The main steps included:

Data Exploration and Preprocessing:

Loaded and explored the dataset.
Cleaned and processed the data for analysis, handling missing values and categorical data.
Exploratory Data Analysis (EDA):

Performed EDA to understand the distribution of data.
Visualized data using various plots to identify trends and patterns.
Feature Engineering:

Created new features to enhance the predictive power of the models.
Selected the most relevant features based on statistical methods and domain knowledge.
Model Building:
decision trees
Fine-tuned models to improve accuracy.

Model Evaluation:

Compared the performance of different models.
Selected the best-performing model based on evaluation metrics.
Conclusion:

The project successfully identified key factors influencing sales.
The final model provided accurate sales predictions, which can help Walmart optimize their inventory and sales strategies.

https://github.com/Deepa01d/Walmart-Sales-Prediction.git


{
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/Deepa01d/Car-sales-Dashoboard/blob/main/walmartg_ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "1caf4e06",
      "metadata": {
        "id": "1caf4e06"
      },
      "outputs": [],
      "source": [
        "import pandas as pd\n",
        "import matplotlib.pyplot as plt\n",
        "import seaborn as sns"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "19a030f1",
      "metadata": {
        "id": "19a030f1",
        "outputId": "9a799e05-a437-4432-e45e-28ab48040401"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.192192e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>9117.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.811311e+10</td>\n",
              "      <td>2</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "      <td>4010.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.805520e+11</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>313.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.085947e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>4447.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>4.900004e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>9538.0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType  VisitNumber Weekday           Upc  ScanCount  \\\n",
              "0         7           20  Friday  7.192192e+09          1   \n",
              "1         7           20  Friday  6.811311e+10          2   \n",
              "2        25           28  Friday  8.805520e+11          1   \n",
              "3        25           28  Friday  8.085947e+10          1   \n",
              "4        25           28  Friday  4.900004e+09          1   \n",
              "\n",
              "  DepartmentDescription  FinelineNumber  \n",
              "0          FROZEN FOODS          9117.0  \n",
              "1          SERVICE DELI          4010.0  \n",
              "2            LADIESWEAR           313.0  \n",
              "3            LADIESWEAR          4447.0  \n",
              "4           DSD GROCERY          9538.0  "
            ]
          },
          "execution_count": 2,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train = pd.read_csv(\"traindata.csv\")\n",
        "train.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "26e6b07a",
      "metadata": {
        "id": "26e6b07a",
        "outputId": "5e2c62a8-3381-48a6-bd20-0fcb50cd17b5"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>87</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.106841e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4063</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>361</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.727878e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>1605</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>385</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.840007e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>4551</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>413</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.200000e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>IMPULSE MERCHANDISE</td>\n",
              "      <td>135</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>462</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.282133e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>PLUS AND MATERNITY</td>\n",
              "      <td>744</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   VisitNumber Weekday           Upc  ScanCount DepartmentDescription  \\\n",
              "0           87  Friday  7.106841e+09          1          FROZEN FOODS   \n",
              "1          361  Friday  6.727878e+10          1             MENS WEAR   \n",
              "2          385  Friday  2.840007e+09          1           DSD GROCERY   \n",
              "3          413  Friday  2.200000e+09          1   IMPULSE MERCHANDISE   \n",
              "4          462  Friday  7.282133e+10          1    PLUS AND MATERNITY   \n",
              "\n",
              "   FinelineNumber  \n",
              "0            4063  \n",
              "1            1605  \n",
              "2            4551  \n",
              "3             135  \n",
              "4             744  "
            ]
          },
          "execution_count": 3,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "test = pd.read_csv(\"testdata.csv\")\n",
        "test.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "6a8bcc4d",
      "metadata": {
        "id": "6a8bcc4d",
        "outputId": "a8562981-7a9f-40ed-caf4-69e11cf4767d"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.192192e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>9117.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.811311e+10</td>\n",
              "      <td>2</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "      <td>4010.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.805520e+11</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>313.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.085947e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>4447.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>4.900004e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>9538.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>9.933894e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>1180.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>6</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.430004e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>COMM BREAD</td>\n",
              "      <td>3709.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.874299e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>BAKERY</td>\n",
              "      <td>2010.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>8</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.874299e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>BAKERY</td>\n",
              "      <td>2010.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>9</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>4.900001e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>9538.0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType  VisitNumber Weekday           Upc  ScanCount  \\\n",
              "0         7           20  Friday  7.192192e+09          1   \n",
              "1         7           20  Friday  6.811311e+10          2   \n",
              "2        25           28  Friday  8.805520e+11          1   \n",
              "3        25           28  Friday  8.085947e+10          1   \n",
              "4        25           28  Friday  4.900004e+09          1   \n",
              "5        25           28  Friday  9.933894e+09          1   \n",
              "6        25           28  Friday  2.430004e+09          1   \n",
              "7        25           28  Friday  7.874299e+09          1   \n",
              "8        25           28  Friday  7.874299e+09          1   \n",
              "9        25           28  Friday  4.900001e+09          1   \n",
              "\n",
              "  DepartmentDescription  FinelineNumber  \n",
              "0          FROZEN FOODS          9117.0  \n",
              "1          SERVICE DELI          4010.0  \n",
              "2            LADIESWEAR           313.0  \n",
              "3            LADIESWEAR          4447.0  \n",
              "4           DSD GROCERY          9538.0  \n",
              "5            LADIESWEAR          1180.0  \n",
              "6            COMM BREAD          3709.0  \n",
              "7                BAKERY          2010.0  \n",
              "8                BAKERY          2010.0  \n",
              "9           DSD GROCERY          9538.0  "
            ]
          },
          "execution_count": 5,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train.head(10)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "12e5b583",
      "metadata": {
        "id": "12e5b583",
        "outputId": "b53ae585-9d45-400d-e087-7edf37c64e83"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "(77186, 7)"
            ]
          },
          "execution_count": 6,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train.shape"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "f68d61ed",
      "metadata": {
        "id": "f68d61ed",
        "outputId": "dea69c3d-9c73-4d58-e54b-a38f76c2bf55"
      },
      "outputs": [
        {
          "name": "stdout",
          "output_type": "stream",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 77186 entries, 0 to 77185\n",
            "Data columns (total 7 columns):\n",
            " #   Column                 Non-Null Count  Dtype  \n",
            "---  ------                 --------------  -----  \n",
            " 0   TripType               77186 non-null  int64  \n",
            " 1   VisitNumber            77186 non-null  int64  \n",
            " 2   Weekday                77186 non-null  object \n",
            " 3   Upc                    77186 non-null  float64\n",
            " 4   ScanCount              77186 non-null  int64  \n",
            " 5   DepartmentDescription  77186 non-null  object \n",
            " 6   FinelineNumber         77186 non-null  float64\n",
            "dtypes: float64(2), int64(3), object(2)\n",
            "memory usage: 4.1+ MB\n"
          ]
        }
      ],
      "source": [
        "train.info()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "0e7f570a",
      "metadata": {
        "id": "0e7f570a",
        "outputId": "880770e2-dbe7-4040-ff7c-6ebdc3a3e8ed"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "TripType                 0\n",
              "VisitNumber              0\n",
              "Weekday                  0\n",
              "Upc                      0\n",
              "ScanCount                0\n",
              "DepartmentDescription    0\n",
              "FinelineNumber           0\n",
              "dtype: int64"
            ]
          },
          "execution_count": 8,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train.isnull().sum()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "280c724c",
      "metadata": {
        "id": "280c724c"
      },
      "outputs": [],
      "source": [
        "# form hypothesis on the data - what behaviour exists in different trip types"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "aefd9546",
      "metadata": {
        "id": "aefd9546"
      },
      "outputs": [],
      "source": [
        "# weekends - a particular trip type will be dominating"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "f96ccb25",
      "metadata": {
        "id": "f96ccb25",
        "outputId": "c8151800-ac83-4c07-dea2-6efc178621ca"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "array([ 7, 25, 38])"
            ]
          },
          "execution_count": 13,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train['TripType'].unique()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "dafeaeb1",
      "metadata": {
        "id": "dafeaeb1",
        "outputId": "bce5f44d-c4fb-48e3-a0b2-9d6c177117e9"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "38    28525\n",
              "25    26493\n",
              "7     22168\n",
              "Name: TripType, dtype: int64"
            ]
          },
          "execution_count": 14,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train['TripType'].value_counts()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "ffb09097",
      "metadata": {
        "id": "ffb09097"
      },
      "outputs": [],
      "source": [
        "# trip 38 is most frequently occuring one"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "a35d980a",
      "metadata": {
        "id": "a35d980a",
        "outputId": "1bd160b5-2e67-46d0-bc78-3d3fc21715c6"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "Text(0, 0.5, 'Count')"
            ]
          },
          "execution_count": 17,
          "metadata": {},
          "output_type": "execute_result"
        },
        {
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 800x500 with 1 Axes>"
            ]
          },
          "metadata": {},
          "output_type": "display_data"
        }
      ],
      "source": [
        "plt.figure(figsize =(8,5))\n",
        "sns.countplot(data = train, x = 'TripType',palette = 'YlGnBu')\n",
        "plt.title(\"Frequency of trip types\")\n",
        "plt.xlabel(\"Trip Type\")\n",
        "plt.ylabel(\"Count\")"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "35aff9bf",
      "metadata": {
        "id": "35aff9bf"
      },
      "outputs": [],
      "source": [
        "# quantity"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "b6cc3f7a",
      "metadata": {
        "id": "b6cc3f7a",
        "outputId": "6fa80a27-9bb8-4460-db4e-ca88c01a429b"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              " 1     68284\n",
              " 2      6260\n",
              " 3      1016\n",
              "-1       700\n",
              " 4       535\n",
              " 5       162\n",
              " 6        90\n",
              "-2        39\n",
              " 8        30\n",
              " 7        23\n",
              " 10       13\n",
              "-3         7\n",
              " 12        7\n",
              " 9         6\n",
              " 11        5\n",
              " 15        2\n",
              " 30        1\n",
              " 46        1\n",
              " 24        1\n",
              " 18        1\n",
              "-4         1\n",
              " 14        1\n",
              " 13        1\n",
              "Name: ScanCount, dtype: int64"
            ]
          },
          "execution_count": 19,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train['ScanCount'].value_counts()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "e06d7955",
      "metadata": {
        "id": "e06d7955",
        "outputId": "199c78b7-62b2-4f2a-d963-954edf74c8fb"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>TripType</th>\n",
              "      <th>ScanCount</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>84350</td>\n",
              "      <td>38</td>\n",
              "      <td>89</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>127057</td>\n",
              "      <td>38</td>\n",
              "      <td>81</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>71143</td>\n",
              "      <td>38</td>\n",
              "      <td>74</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>188905</td>\n",
              "      <td>38</td>\n",
              "      <td>68</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>27356</td>\n",
              "      <td>38</td>\n",
              "      <td>66</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12304</th>\n",
              "      <td>140036</td>\n",
              "      <td>38</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12305</th>\n",
              "      <td>116544</td>\n",
              "      <td>7</td>\n",
              "      <td>0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12306</th>\n",
              "      <td>136530</td>\n",
              "      <td>38</td>\n",
              "      <td>-1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12307</th>\n",
              "      <td>75132</td>\n",
              "      <td>7</td>\n",
              "      <td>-1</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12308</th>\n",
              "      <td>164446</td>\n",
              "      <td>7</td>\n",
              "      <td>-1</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>12309 rows × 3 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "       VisitNumber  TripType  ScanCount\n",
              "0            84350        38         89\n",
              "1           127057        38         81\n",
              "2            71143        38         74\n",
              "3           188905        38         68\n",
              "4            27356        38         66\n",
              "...            ...       ...        ...\n",
              "12304       140036        38          0\n",
              "12305       116544         7          0\n",
              "12306       136530        38         -1\n",
              "12307        75132         7         -1\n",
              "12308       164446         7         -1\n",
              "\n",
              "[12309 rows x 3 columns]"
            ]
          },
          "execution_count": 23,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "c = train.groupby([\"VisitNumber\",\"TripType\"])['ScanCount'].sum().sort_values(ascending = False).reset_index()\n",
        "c"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "b3a27b05",
      "metadata": {
        "id": "b3a27b05"
      },
      "outputs": [],
      "source": [
        "# average qtys bought in each trip type"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "385282e0",
      "metadata": {
        "id": "385282e0",
        "outputId": "7dbb3ba5-b877-44fb-a493-9609f3777e29"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>ScanCount</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>4.536585</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>25</td>\n",
              "      <td>7.584911</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>38</td>\n",
              "      <td>11.516140</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType  ScanCount\n",
              "0         7   4.536585\n",
              "1        25   7.584911\n",
              "2        38  11.516140"
            ]
          },
          "execution_count": 29,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "c_r = c.groupby(\"TripType\")['ScanCount'].mean().reset_index()\n",
        "c_r"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "29e1859a",
      "metadata": {
        "id": "29e1859a",
        "outputId": "e8494ce4-47ad-4bbe-a69f-e53665f13f7d"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "Text(0, 0.5, 'Average Quanity')"
            ]
          },
          "execution_count": 30,
          "metadata": {},
          "output_type": "execute_result"
        },
        {
          "data": {
            "image/png": "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SkhIsJ/3888/67vvvnOYVUtMTFSdOnVUq1Yth3v06NHDZXmt/+89rDab7abHjhgxQnv27NGWLVskSRkZGfrwww/Vt29flS5dWpLsa2e7du2qjz/+WCkpKQXKUa5cOXXs2FHz589Xbm6uJOns2bNasWKF+vTpY1/2cPfddystLU09evTQihUrdOrUKee+4Jvo3LlzgY8NDAzU3//+d4exnj17Kjc3V5s2bSp0hurVq+uRRx7RrFmz7L8/ixYt0unTp/Odde/Vq5fDfosWLVSlShVt2LBB0u9PkDhz5oz69u2rK1eu2Lfc3Fw9/PDD2r59u8tmrgG4HuUVgNv88ssv2rRpkzp06CDLspSWlqa0tDQ9/vjjkqQPPvjAfmxsbKy2bdum//znP5KkhIQE+fn5ORTT06dPKywsLM998hv7o/LlyysgIECHDx++4XG//fab/P39Va5cuZtes1OnTqpatareeecdSb+vuTx37px9yYAk3X///Vq+fLmuXLmiPn36KDIyUnXq1NHixYtvev3Y2FilpKRo/fr1kn5fRpGdne3wCKvevXvrgw8+0JEjR9S5c2eFhoaqadOm9nNuVXh4eIGPze/3oWLFipJ+/727FSNGjNDBgwftX9c777yj5s2b629/+9t17/nHsasZ/vvf/0qSHn/8cfn4+Dhsr7/+uizL0pkzZ24pLwD3obwCcJsPPvhAlmXp008/VdmyZe1bhw4dJEnz58+3v5mnR48e8vPz07x585STk6MPP/xQMTExKlu2rP165cqVsxePa6Wmpt40i7e3tx544AHt2LFDR48ezfeYo0ePaufOnXrggQcK9PV5eXkpLi5On376qY4fP65Zs2bpwQcf1B133OFwXKdOnfTVV18pPT1dGzduVGRkpHr27Klt27bd8Prt2rVTRESEfUY6ISFBTZs2zTPz3L9/f23dulXp6elas2aNLMvSI488oiNHjhTo67iRgsxAX3Wj35uC/GXgRh544AHVqVNHb7/9trZu3Wp/vFd+8vvvITU11Z6hfPnykn5/bNr27dvz3QryFyIAnkF5BeAWOTk5mj9/vmrUqKENGzbk2Z555hkdP35cX3zxhSSpbNmyiomJ0YIFC7R69WqlpqbmeSNOy5YttXfvXv30008O40uWLClQpnHjxsmyLA0ZMiTPO+BzcnI0ePBg5eTkOLzB6OpzTC9cuJDvNQcOHChfX1/16tVL+/fvv+Gbx/z8/NSyZUu9/vrrkqTdu3ffMK+3t7d69+6t5cuXa/PmzdqxY8cNn1JQqlQptW/fXs8//7wuXbqkffv23fD6rpaZmamVK1c6jC1atEheXl66//77b/n6w4cP15o1azR+/HiFhYWpS5cu+R730UcfOexv3bpVR44cUatWrSRJ99xzj8qUKaOffvpJjRs3znfz9fW95bwA3MSD620B/ImtWrXKkmS9/vrr+b5+8uRJy8/Pz4qJibGPffnll5YkKzIy0oqMjLRycnIczklJSbHKlStnVa5c2Zo3b571xRdfWL1797aqVKliSbISExNvmusf//iHZbPZrGbNmlkLFy60Nm3aZC1cuNBq3ry5JcmaPHmyw/FX38w0aNAga+vWrdb27dutjIwMh2MGDx5sSbKqVKmSJ/OkSZOs/v37WwsXLrQ2btxoLV++3GrdurXl4+Nj7d2796Z59+/fb/+e+Pv753nj18CBA61hw4ZZS5YssRITE62lS5daDRo0sIKDg60TJ07c9PrXfo35vWFr+/bteY6/3hu2ypUrZ0VERFgzZ860vvzyS2vEiBGWJGvw4MEFynGV/vCGravOnz9vlStXzpJkTZw48bq5oqKirAEDBlhr16615s6da4WGhlqVKlWyTp8+bT/2ww8/tLy8vKxu3bpZn3zyiZWYmGh9+umn1qRJk6ynn37aqbwAihblFYBbxMTEWL6+vjcsUN27d7dKlChhpaamWpb1+7u9o6KiLEnW888/n+85e/futdq0aWOVLFnSCgkJsQYMGGDNnz/fkmR9//33Bcq2detWq3PnzlZYWJjl5eVlSbJKlixprVmzJt/jx48fb0VERNiP/eNTDTZu3GhJsqZOnZrn3NWrV1vt27e3KlWqZPn6+lqhoaFWdHS0tXnz5gJltSzLatGihSXJ6tWrV57X5s+fb7Vu3doKCwuzfH19rYiICKtr167WDz/8UODru6q81q5d29q4caPVuHFjy8/PzwoPD7cmTJhgfzJCQV2vvFqWZfXr188qUaKEdfTo0evmWrdundW7d2+rTJkylr+/vxUdHW0dPHgwz/GJiYlWhw4drJCQEMvHx8eqVKmS1aFDB4fvA4Dih4+HBWC8p556SosXL9bp06cL9c+9CxYsUN++ffXcc8/Z/0nfGc8884xmz56t5OTk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AABQxIr1soGVK1eqcePG6tKli0JDQ9WwYUPNnTv3hufEx8crODjYvkVFRRVRWgAAALhbocrrlStX9O9//1vvvvuuMjMzJUnHjh1TVlaWS8P9+uuvmj17tmrWrKkvv/xSTz/9tIYPH64FCxZc95zx48crPT3dviUnJ7s0EwAAADzH6WUDR44c0cMPP6ykpCRlZ2erbdu2CgwM1LRp03Tx4kX985//dFm43NxcNW7cWFOmTJEkNWzYUPv27dPs2bPVp0+ffM/x8/OTn5+fyzIAAACg+HB65nXEiBFq3Lixzp49K39/f/v4o48+qq+++sql4cLDw1WrVi2HsbvuuktJSUkuvQ8AAADM4PTM6zfffKMtW7bI19fXYbxKlSpKSUlxWTBJuueee7R//36HsQMHDqhKlSouvQ8AAADM4PTMa25urnJycvKMHz16VIGBgS4JddWoUaP07bffasqUKfrll1+0aNEizZkzR3FxcS69DwAAAMzgdHlt27atZsyYYd+32WzKysrSiy++qOjoaFdmU5MmTbRs2TItXrxYderU0SuvvKIZM2aoV69eLr0PAAAAzOD0soG33npLrVu3Vq1atXTx4kX17NlTBw8eVPny5bV48WKXB3zkkUf0yCOPuPy6AAAAMI/T5TUiIkJ79uzR4sWLtWvXLuXm5mrAgAHq1auXwxu4AAAAAFcr1Cds+fv7KzY2VrGxsa7OAwAAAFyX0+V15cqV+Y7bbDaVLFlSt912m6pVq3bLwQAAAIA/crq8xsTEyGazybIsh/GrYzabTffee6+WL1+usmXLuiwoAAAA4PTTBtavX68mTZpo/fr19o9gXb9+ve6++26tXr1amzZt0unTp/Xss8+6Iy8AAAD+wpyeeR0xYoTmzJmjFi1a2McefPBBlSxZUk899ZT27dunGTNmsB4WAAAALuf0zOuhQ4cUFBSUZzwoKEi//vqrJKlmzZo6derUracDAAAAruF0eW3UqJHGjBmjkydP2sdOnjyp5557Tk2aNJEkHTx4UJGRka5LCQAAAKgQywbef/99derUSZGRkYqKipLNZlNSUpKqV6+uFStWSJKysrI0adIkl4cFAADAX5vT5fWOO+7Qzz//rC+//FIHDhyQZVm688471bZtW3l5/T6RGxMT4+qcAAAAQOE+pMBms+nhhx/Www8/7Oo8AAAAwHUVqryeO3dOiYmJSkpK0qVLlxxeGz58uEuCAQAAAH/kdHndvXu3oqOjdf78eZ07d04hISE6deqUAgICFBoaSnkFAACA2zj9tIFRo0apY8eOOnPmjPz9/fXtt9/qyJEjatSokaZPn+6OjAAAAICkQpTXPXv26JlnnpG3t7e8vb2VnZ2tqKgoTZs2TRMmTHBHRgAAAEBSIcqrj4+PbDabJCksLExJSUmSpODgYPuvAQAAAHdwes1rw4YNtWPHDt1+++1q3bq1XnjhBZ06dUoffvih6tat646MAAAAgKRCzLxOmTJF4eHhkqRXXnlF5cqV0+DBg3XixAnNmTPH5QEBAACAq5yaebUsSxUqVFDt2rUlSRUqVNDnn3/ulmAAAADAHzk182pZlmrWrKmjR4+6Kw8AAABwXU6VVy8vL9WsWVOnT592Vx4AAADgupxe8zpt2jSNGTNGe/fudUceAAAA4LqcftrAE088ofPnz6t+/fry9fWVv7+/w+tnzpxxWTgAAADgWk6X1xkzZrghBgAAAHBzTpfXvn37uiMHAAAAcFNOr3mVpEOHDmnixInq0aOHTpw4IUlau3at9u3b59JwAAAAwLWcLq+JiYmqW7eu/u///k//+te/lJWVJUn64Ycf9OKLL7o8IAAAAHCV0+V13LhxevXVV7V+/Xr5+vrax1u3bq1t27a5NBwAAABwLafL648//qhHH300z3iFChV4/isAAADcyunyWqZMGR0/fjzP+O7du1WpUiWXhAIAAADy43R57dmzp8aOHavU1FTZbDbl5uZqy5YtevbZZ9WnTx93ZAQAAAAkFaK8vvbaa6pcubIqVaqkrKws1apVS/fff79atGihiRMnuiMjAAAAIKkQz3n18fHRRx99pJdfflm7d+9Wbm6uGjZsqJo1a7ojHwAAAGDndHlNTExUy5YtVaNGDdWoUcMdmQAAAIB8Ob1soG3btqpcubLGjRunvXv3uiMTAAAAkC+ny+uxY8f03HPPafPmzapXr57q1aunadOm6ejRo+7IBwAAANg5XV7Lly+voUOHasuWLTp06JC6deumBQsWqGrVqnrggQfckREAAACQVIjyeq1q1app3Lhxmjp1qurWravExERX5QIAAADyKHR53bJli4YMGaLw8HD17NlTtWvX1urVq12ZDQAAAHDg9NMGJkyYoMWLF+vYsWNq06aNZsyYoZiYGAUE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\n",
            "text/plain": [
              "<Figure size 800x600 with 1 Axes>"
            ]
          },
          "metadata": {},
          "output_type": "display_data"
        }
      ],
      "source": [
        "plt.figure(figsize =(8,6))\n",
        "sns.barplot(x = 'TripType', y = 'ScanCount', data = c_r)\n",
        "plt.title(\"Avg Qtys vs Trip Type\")\n",
        "plt.xlabel(\"Trip Type\")\n",
        "plt.ylabel(\"Average Quanity\")"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "a24f350e",
      "metadata": {
        "id": "a24f350e"
      },
      "outputs": [],
      "source": [
        "# Trip type 38 has bulk shoppers - more basket size"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "61e1a761",
      "metadata": {
        "id": "61e1a761"
      },
      "outputs": [],
      "source": [
        "# hypothesis - Trip type is dependent on weekdays"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "07e9755f",
      "metadata": {
        "scrolled": false,
        "id": "07e9755f",
        "outputId": "8d2960ee-2b70-47a3-8c00-c58fdf1f78de"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>count</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>Friday</td>\n",
              "      <td>3078</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>Monday</td>\n",
              "      <td>3127</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>7</td>\n",
              "      <td>Saturday</td>\n",
              "      <td>3451</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>7</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>3840</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>7</td>\n",
              "      <td>Thursday</td>\n",
              "      <td>2739</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5</th>\n",
              "      <td>7</td>\n",
              "      <td>Tuesday</td>\n",
              "      <td>2825</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>6</th>\n",
              "      <td>7</td>\n",
              "      <td>Wednesday</td>\n",
              "      <td>3108</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>4231</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>8</th>\n",
              "      <td>25</td>\n",
              "      <td>Monday</td>\n",
              "      <td>2811</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>9</th>\n",
              "      <td>25</td>\n",
              "      <td>Saturday</td>\n",
              "      <td>5369</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>10</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>5470</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>11</th>\n",
              "      <td>25</td>\n",
              "      <td>Thursday</td>\n",
              "      <td>3034</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>12</th>\n",
              "      <td>25</td>\n",
              "      <td>Tuesday</td>\n",
              "      <td>2901</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>13</th>\n",
              "      <td>25</td>\n",
              "      <td>Wednesday</td>\n",
              "      <td>2677</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>14</th>\n",
              "      <td>38</td>\n",
              "      <td>Friday</td>\n",
              "      <td>3951</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>15</th>\n",
              "      <td>38</td>\n",
              "      <td>Monday</td>\n",
              "      <td>4175</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>16</th>\n",
              "      <td>38</td>\n",
              "      <td>Saturday</td>\n",
              "      <td>4219</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>17</th>\n",
              "      <td>38</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>6033</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>18</th>\n",
              "      <td>38</td>\n",
              "      <td>Thursday</td>\n",
              "      <td>2980</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>19</th>\n",
              "      <td>38</td>\n",
              "      <td>Tuesday</td>\n",
              "      <td>3744</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>20</th>\n",
              "      <td>38</td>\n",
              "      <td>Wednesday</td>\n",
              "      <td>3423</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "    TripType    Weekday  count\n",
              "0          7     Friday   3078\n",
              "1          7     Monday   3127\n",
              "2          7   Saturday   3451\n",
              "3          7     Sunday   3840\n",
              "4          7   Thursday   2739\n",
              "5          7    Tuesday   2825\n",
              "6          7  Wednesday   3108\n",
              "7         25     Friday   4231\n",
              "8         25     Monday   2811\n",
              "9         25   Saturday   5369\n",
              "10        25     Sunday   5470\n",
              "11        25   Thursday   3034\n",
              "12        25    Tuesday   2901\n",
              "13        25  Wednesday   2677\n",
              "14        38     Friday   3951\n",
              "15        38     Monday   4175\n",
              "16        38   Saturday   4219\n",
              "17        38     Sunday   6033\n",
              "18        38   Thursday   2980\n",
              "19        38    Tuesday   3744\n",
              "20        38  Wednesday   3423"
            ]
          },
          "execution_count": 36,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "w = train.groupby(['TripType','Weekday']).size().reset_index(name = 'count')\n",
        "w"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "e98f4cdb",
      "metadata": {
        "id": "e98f4cdb"
      },
      "outputs": [],
      "source": [
        "weekday_order = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']\n",
        "\n",
        "w['Weekday'] = pd.Categorical(w['Weekday'], categories=weekday_order, ordered=True)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "14c1b70e",
      "metadata": {
        "scrolled": false,
        "id": "14c1b70e",
        "outputId": "355b2194-082c-4a74-f84a-2b5ce99f59f2"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "Text(0, 0.5, 'Count')"
            ]
          },
          "execution_count": 42,
          "metadata": {},
          "output_type": "execute_result"
        },
        {
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 900x700 with 1 Axes>"
            ]
          },
          "metadata": {},
          "output_type": "display_data"
        }
      ],
      "source": [
        "plt.figure(figsize = (9,7))\n",
        "sns.lineplot(data = w, x = 'Weekday', y= 'count', hue = 'TripType', marker = 'o')\n",
        "plt.title(\"Weekday vs Trips\")\n",
        "plt.xlabel(\"Weekday\")\n",
        "plt.ylabel(\"Count\")"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "f6450501",
      "metadata": {
        "id": "f6450501"
      },
      "outputs": [],
      "source": [
        "# sundays have the most visits\n",
        "# Trip type 38 tends to buy more than others on Mondays\n",
        "# Trip type 25 and 38 perform similarly on Thursdays\n",
        "# On Saturdays, when every trip type tends to buy morem trip type 38 visits the store less"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "36c047f2",
      "metadata": {
        "id": "36c047f2"
      },
      "outputs": [],
      "source": [
        "# department"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "5bfdc325",
      "metadata": {
        "id": "5bfdc325",
        "outputId": "75ecf5e4-cb65-475c-8b31-b6dab3b1707a"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>count</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>1-HR PHOTO</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>ACCESSORIES</td>\n",
              "      <td>11</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>7</td>\n",
              "      <td>AUTOMOTIVE</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>7</td>\n",
              "      <td>BAKERY</td>\n",
              "      <td>856</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>7</td>\n",
              "      <td>BATH AND SHOWER</td>\n",
              "      <td>5</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>178</th>\n",
              "      <td>38</td>\n",
              "      <td>SHOES</td>\n",
              "      <td>41</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>179</th>\n",
              "      <td>38</td>\n",
              "      <td>SLEEPWEAR/FOUNDATIONS</td>\n",
              "      <td>24</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>180</th>\n",
              "      <td>38</td>\n",
              "      <td>SPORTING GOODS</td>\n",
              "      <td>24</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>181</th>\n",
              "      <td>38</td>\n",
              "      <td>TOYS</td>\n",
              "      <td>56</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>182</th>\n",
              "      <td>38</td>\n",
              "      <td>WIRELESS</td>\n",
              "      <td>2</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>183 rows × 3 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "     TripType  DepartmentDescription  count\n",
              "0           7             1-HR PHOTO      3\n",
              "1           7            ACCESSORIES     11\n",
              "2           7             AUTOMOTIVE     30\n",
              "3           7                 BAKERY    856\n",
              "4           7        BATH AND SHOWER      5\n",
              "..        ...                    ...    ...\n",
              "178        38                  SHOES     41\n",
              "179        38  SLEEPWEAR/FOUNDATIONS     24\n",
              "180        38         SPORTING GOODS     24\n",
              "181        38                   TOYS     56\n",
              "182        38               WIRELESS      2\n",
              "\n",
              "[183 rows x 3 columns]"
            ]
          },
          "execution_count": 46,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "d = train.groupby(['TripType','DepartmentDescription']).size().reset_index(name = \"count\")\n",
        "d"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "f0089592",
      "metadata": {
        "id": "f0089592"
      },
      "outputs": [],
      "source": [
        "top_departments = d.groupby('TripType').apply(lambda x: x.nlargest(3, 'count')).reset_index(drop=True)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "f5cbdf2d",
      "metadata": {
        "id": "f5cbdf2d",
        "outputId": "67cc95c5-309d-4989-d8eb-59ddc5d0ae56"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>count</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "      <td>3522</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>GROCERY DRY GOODS</td>\n",
              "      <td>3201</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>7</td>\n",
              "      <td>PRODUCE</td>\n",
              "      <td>2879</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>5196</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>3591</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5</th>\n",
              "      <td>25</td>\n",
              "      <td>GIRLS WEAR, 4-6X  AND 7-14</td>\n",
              "      <td>1755</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>6</th>\n",
              "      <td>38</td>\n",
              "      <td>DAIRY</td>\n",
              "      <td>6974</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7</th>\n",
              "      <td>38</td>\n",
              "      <td>GROCERY DRY GOODS</td>\n",
              "      <td>6243</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>8</th>\n",
              "      <td>38</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>3875</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType       DepartmentDescription  count\n",
              "0         7                SERVICE DELI   3522\n",
              "1         7           GROCERY DRY GOODS   3201\n",
              "2         7                     PRODUCE   2879\n",
              "3        25                   MENS WEAR   5196\n",
              "4        25                  LADIESWEAR   3591\n",
              "5        25  GIRLS WEAR, 4-6X  AND 7-14   1755\n",
              "6        38                       DAIRY   6974\n",
              "7        38           GROCERY DRY GOODS   6243\n",
              "8        38                 DSD GROCERY   3875"
            ]
          },
          "execution_count": 48,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "top_departments"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "dcc72f99",
      "metadata": {
        "id": "dcc72f99",
        "outputId": "56767dee-162f-4320-da22-ee6f492ce383"
      },
      "outputs": [
        {
          "data": {
            "image/png": "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REREHwStNzkoJycHLVq0eNu5EBERERERfTDeqNgaNmwYNm7c+LZzISIiIiIi+mC80W2EWVlZWL16NQ4cOIB69epBLpdL9i9YsOCtJEdERERERPS+eqNi66+//kKDBg0AAJcuXZLs42IZREREREREb1hsRUVFve08iIiIiIiIPihv9MwWERERERERFe+NZrY8PDyKvV3w0KFDb5wQERERERHRh+CNiq2C57UK5ObmIi4uDpcuXcKgQYPeRl5ERERERETvtTcqthYuXFhoe0BAAJ4+ffqfEiIiIiIiIvoQvNVntgYOHIiwsLC32SUREREREdF76a0WWydOnICent7b7JKIiIiIiOi99Ea3EX766aeS14IgICkpCWfOnMGMGTPeSmJERERERETvszcqtpRKpeS1lpYWatWqhcDAQHTs2PGtJEZERERERPQ+e6NiKzw8/G3nQURE9F4ImbizTMYZO797mYxDRESa80bFVoGzZ88iPj4eMpkMTk5OaNiw4dvKi4iIiIiI6L32RsXWgwcP8PnnnyM6OhoVKlSAIAhIS0uDh4cHNm/ejEqVKr3tPImIiIiIiN4rb7Qaoa+vL9LT03H58mU8fvwYKSkpuHTpEtLT0zFu3Li3nSMREREREdF7541mtiIjI3HgwAHUrl1bbHNycsKyZcu4QAYRERERERHesNjKz8+HXC5Xa5fL5cjPz//PSX3sGk9ep/Exzs77QuNjEBERERF9zN7oNsK2bdti/PjxuHfvnth29+5dTJgwAe3atXtryREREREREb2v3qjYCgkJwZMnT2Bra4saNWrA3t4ednZ2ePLkCZYuXfq2cyQiIiIiInrvvNFthNbW1jh37hz279+Pq1evQhAEODk5oX379m87PyIiIiIiovdSqWa2Dh06BCcnJ6SnpwMAOnToAF9fX4wbNw5NmzZFnTp1cOTIEY0kSkRERERE9D4pVbG1aNEiDB8+HCYmJmr7lEolRowYgQULFry15IiIiIiIiN5XpSq2Lly4gM6dOxe5v2PHjjh79ux/ToqIiIiIiOh9V6pi6/79+4Uu+V5AR0cHDx8+/M9JERERERERve9KVWxVqVIFFy9eLHL/X3/9hcqVK//npIiIiIiIiN53pSq2unbtim+//RZZWVlq+zIzMzFz5kx4enq+teSIiIiIiIjeV6Va+v2bb77Btm3bULNmTYwdOxa1atWCTCZDfHw8li1bhufPn8Pf319TuRIREREREb03SlVsWVpa4vjx4xg1ahSmTZsGQRAAADKZDJ06dcLy5cthaWmpkUSJiIiIiIjeJ6X+UmMbGxvs2bMHKSkpuHHjBgRBgIODAypWrKiJ/IiIiIiIiN5LpS62ClSsWBFNmzZ9m7kQERERERF9MEq1QAYRERERERGVDIstIiIiIiIiDWCxRUREREREpAEstoiIiIiIiDSAxRYREREREZEGsNgiIiIiIiLSgDde+p3eb7cD65bJONW+vVgm4xARERERvWs4s0VERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDWGwRERERERFpAIstIiIiIiIiDSjXYmvFihWoV68eTExMYGJigubNm2Pv3r3ifkEQEBAQACsrK+jr68Pd3R2XL1+W9JGdnQ1fX1+Ym5vD0NAQPXr0wL///iuJSUlJgbe3N5RKJZRKJby9vZGamloWp0hERERERB+pci22qlatih9++AFnzpzBmTNn0LZtW/Ts2VMsqObOnYsFCxYgJCQEsbGxUKlU6NChA548eSL24efnh+3bt2Pz5s04evQonj59Ck9PTzx//lyM6d+/P+Li4hAZGYnIyEjExcXB29u7zM+XiIiIiIg+HjrlOXj37t0lr2fPno0VK1bg5MmTcHJywqJFi+Dv749PP/0UALB27VpYWlpi48aNGDFiBNLS0hAaGoqff/4Z7du3BwCsX78e1tbWOHDgADp16oT4+HhERkbi5MmTcHFxAQCsWbMGzZs3x7Vr11CrVq1Cc8vOzkZ2drb4Oj09XROXgIiIiIiIPlDvzDNbz58/x+bNm5GRkYHmzZsjISEBycnJ6NixoxijUCjg5uaG48ePAwDOnj2L3NxcSYyVlRWcnZ3FmBMnTkCpVIqFFgC4urpCqVSKMYUJDg4WbztUKpWwtrZ+26dMREREREQfsHIvti5evAgjIyMoFAqMHDkS27dvh5OTE5KTkwEAlpaWknhLS0txX3JyMnR1dVGxYsViYywsLNTGtbCwEGMKM23aNKSlpYnbnTt3/tN5EhERERHRx6VcbyMEgFq1aiEuLg6pqanYunUrBg0ahJiYGHG/TCaTxAuCoNb2qldjCot/XT8KhQIKhaKkp0FERERERCRR7jNburq6sLe3R5MmTRAcHIz69etj8eLFUKlUAKA2+/TgwQNxtkulUiEnJwcpKSnFxty/f19t3IcPH6rNmhEREREREb0t5V5svUoQBGRnZ8POzg4qlQr79+8X9+Xk5CAmJgYtWrQAADRu3BhyuVwSk5SUhEuXLokxzZs3R1paGk6fPi3GnDp1CmlpaWIMERERERHR21autxFOnz4dXbp0gbW1NZ48eYLNmzcjOjoakZGRkMlk8PPzQ1BQEBwcHODg4ICgoCAYGBigf//+AAClUomhQ4di4sSJMDMzg6mpKSZNmoS6deuKqxPWrl0bnTt3xvDhw7Fq1SoAwJdffglPT88iVyIkIiIiIiL6r8q12Lp//z68vb2RlJQEpVKJevXqITIyEh06dAAATJkyBZmZmRg9ejRSUlLg4uKCffv2wdjYWOxj4cKF0NHRQZ8+fZCZmYl27dohIiIC2traYsyGDRswbtw4cdXCHj16ICQkpGxPloiIiIiIPirlWmyFhoYWu18mkyEgIAABAQFFxujp6WHp0qVYunRpkTGmpqZYv379m6ZJRERERERUauW+GiF92FoubVkm4xzzPVYm4xARERERldQ7t0AGERERERHRh4DFFhERERERkQaw2CIiIiIiItIAFltEREREREQawGKLiIiIiIhIA1hsERERERERaQCLLSIiIiIiIg1gsUVERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDWGwRERERERFpAIstIiIiIiIiDWCxRUREREREpAEstoiIiIiIiDSAxRYREREREZEGsNgiIiIiIiLSABZbREREREREGsBii4iIiIiISANYbBEREREREWkAiy0iIiIiIiINYLFFRERERESkASy2iIiIiIiINIDFFhERERERkQaw2CIiIiIiItIAFltEREREREQawGKLiIiIiIhIA1hsERERERERaQCLLSIiIiIiIg1gsUVERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDWGwRERERERFpAIstIiIiIiIiDWCxRUREREREpAEstoiIiIiIiDSAxRYREREREZEGsNgiIiIiIiLSABZbREREREREGsBii4iIiIiISANYbBEREREREWkAiy0iIiIiIiINYLFFRERERESkASy2iIiIiIiINIDFFhERERERkQaw2CIiIiIiItKAci22goOD0bRpUxgbG8PCwgK9evXCtWvXJDGCICAgIABWVlbQ19eHu7s7Ll++LInJzs6Gr68vzM3NYWhoiB49euDff/+VxKSkpMDb2xtKpRJKpRLe3t5ITU3V9CkSEREREdFHqlyLrZiYGIwZMwYnT57E/v37kZeXh44dOyIjI0OMmTt3LhYsWICQkBDExsZCpVKhQ4cOePLkiRjj5+eH7du3Y/PmzTh69CiePn0KT09PPH/+XIzp378/4uLiEBkZicjISMTFxcHb27tMz5eIiIiIiD4eOuU5eGRkpOR1eHg4LCwscPbsWbRp0waCIGDRokXw9/fHp59+CgBYu3YtLC0tsXHjRowYMQJpaWkIDQ3Fzz//jPbt2wMA1q9fD2traxw4cACdOnVCfHw8IiMjcfLkSbi4uAAA1qxZg+bNm+PatWuoVatW2Z44ERERERF98N6pZ7bS0tIAAKampgCAhIQEJCcno2PHjmKMQqGAm5sbjh8/DgA4e/YscnNzJTFWVlZwdnYWY06cOAGlUikWWgDg6uoKpVIpxrwqOzsb6enpko2IiIiIiKik3pliSxAEfPXVV2jVqhWcnZ0BAMnJyQAAS0tLSaylpaW4Lzk5Gbq6uqhYsWKxMRYWFmpjWlhYiDGvCg4OFp/vUiqVsLa2/m8nSEREREREH5V3ptgaO3Ys/vrrL2zatEltn0wmk7wWBEGt7VWvxhQWX1w/06ZNQ1pamrjduXOnJKdBREREREQE4B0ptnx9ffHHH38gKioKVatWFdtVKhUAqM0+PXjwQJztUqlUyMnJQUpKSrEx9+/fVxv34cOHarNmBRQKBUxMTCQbERERERFRSZVrsSUIAsaOHYtt27bh0KFDsLOzk+y3s7ODSqXC/v37xbacnBzExMSgRYsWAIDGjRtDLpdLYpKSknDp0iUxpnnz5khLS8Pp06fFmFOnTiEtLU2MISIiIiIiepvKdTXCMWPGYOPGjfj9999hbGwszmAplUro6+tDJpPBz88PQUFBcHBwgIODA4KCgmBgYID+/fuLsUOHDsXEiRNhZmYGU1NTTJo0CXXr1hVXJ6xduzY6d+6M4cOHY9WqVQCAL7/8Ep6enlyJkIiIiIiINKJci60VK1YAANzd3SXt4eHh8PHxAQBMmTIFmZmZGD16NFJSUuDi4oJ9+/bB2NhYjF+4cCF0dHTQp08fZGZmol27doiIiIC2trYYs2HDBowbN05ctbBHjx4ICQnR7AkSEREREdFHq1yLLUEQXhsjk8kQEBCAgICAImP09PSwdOlSLF26tMgYU1NTrF+//k3SJCIiIiIiKrV3YoEMIiIiIiKiDw2LLSIiIiIiIg1gsUVERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDyvVLjYmIiKhwswd+Vibj+K//rUzGISL6GHFmi4iIiIiISANYbBEREREREWkAiy0iIiIiIiINYLFFRERERESkASy2iIiIiIiINIDFFhERERERkQaw2CIiIiIiItIAFltEREREREQawGKLiIiIiIhIA1hsERERERERaQCLLSIiIiIiIg1gsUVERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDWGwRERERERFpAIstIiIiIiIiDWCxRUREREREpAEstoiIiIiIiDSAxRYREREREZEGsNgiIiIiIiLSABZbREREREREGsBii4iIiIiISANYbBEREREREWkAiy0iIiIiIiINYLFFRERERESkASy2iIiIiIiINIDFFhERERERkQaw2CIiIiIiItIAFltEREREREQawGKLiIiIiIhIA1hsERERERERaQCLLSIiIiIiIg1gsUVERERERKQBLLaIiIiIiIg0gMUWERERERGRBrDYIiIiIiIi0gAWW0RERERERBrAYouIiIiIiEgDWGwRERERERFpAIstIiIiIiIiDSjXYuvw4cPo3r07rKysIJPJsGPHDsl+QRAQEBAAKysr6Ovrw93dHZcvX5bEZGdnw9fXF+bm5jA0NESPHj3w77//SmJSUlLg7e0NpVIJpVIJb29vpKamavjsiIiIiIjoY1auxVZGRgbq16+PkJCQQvfPnTsXCxYsQEhICGJjY6FSqdChQwc8efJEjPHz88P27duxefNmHD16FE+fPoWnpyeeP38uxvTv3x9xcXGIjIxEZGQk4uLi4O3trfHzIyIiIiKij5dOeQ7epUsXdOnSpdB9giBg0aJF8Pf3x6effgoAWLt2LSwtLbFx40aMGDECaWlpCA0Nxc8//4z2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\n",
            "text/plain": [
              "<Figure size 1000x600 with 1 Axes>"
            ]
          },
          "metadata": {},
          "output_type": "display_data"
        }
      ],
      "source": [
        "plt.figure(figsize=(10, 6))\n",
        "sns.barplot(data=top_departments, x='TripType', y='count', hue='DepartmentDescription')\n",
        "plt.title(\"Top 3 Departments for Each TripType\")\n",
        "plt.xlabel(\"TripType\")\n",
        "plt.ylabel(\"Count\")\n",
        "plt.legend(title='Department')\n",
        "plt.show()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "0f8169e4",
      "metadata": {
        "id": "0f8169e4"
      },
      "outputs": [],
      "source": [
        "# trip type 38 tend to buy daily items more\n",
        "# trip type 25 tend to buy garments more, trip type 7 buys service products more"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "cf719a81",
      "metadata": {
        "id": "cf719a81"
      },
      "outputs": [],
      "source": [
        "# classification"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "74e38d9c",
      "metadata": {
        "id": "74e38d9c",
        "outputId": "12858c4e-d3fc-4cb6-9ccf-52f4b2e5fbc0"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.192192e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>9117.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>20</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.811311e+10</td>\n",
              "      <td>2</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "      <td>4010.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.805520e+11</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>313.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>8.085947e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>4447.0</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>28</td>\n",
              "      <td>Friday</td>\n",
              "      <td>4.900004e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>9538.0</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType  VisitNumber Weekday           Upc  ScanCount  \\\n",
              "0         7           20  Friday  7.192192e+09          1   \n",
              "1         7           20  Friday  6.811311e+10          2   \n",
              "2        25           28  Friday  8.805520e+11          1   \n",
              "3        25           28  Friday  8.085947e+10          1   \n",
              "4        25           28  Friday  4.900004e+09          1   \n",
              "\n",
              "  DepartmentDescription  FinelineNumber  \n",
              "0          FROZEN FOODS          9117.0  \n",
              "1          SERVICE DELI          4010.0  \n",
              "2            LADIESWEAR           313.0  \n",
              "3            LADIESWEAR          4447.0  \n",
              "4           DSD GROCERY          9538.0  "
            ]
          },
          "execution_count": 53,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "train.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "e345d5d4",
      "metadata": {
        "id": "e345d5d4",
        "outputId": "c42176e7-0a48-48fd-828d-a7b09896b172"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>87</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.106841e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4063</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>361</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.727878e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>1605</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>385</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.840007e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>4551</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>413</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.200000e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>IMPULSE MERCHANDISE</td>\n",
              "      <td>135</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>462</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.282133e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>PLUS AND MATERNITY</td>\n",
              "      <td>744</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   VisitNumber Weekday           Upc  ScanCount DepartmentDescription  \\\n",
              "0           87  Friday  7.106841e+09          1          FROZEN FOODS   \n",
              "1          361  Friday  6.727878e+10          1             MENS WEAR   \n",
              "2          385  Friday  2.840007e+09          1           DSD GROCERY   \n",
              "3          413  Friday  2.200000e+09          1   IMPULSE MERCHANDISE   \n",
              "4          462  Friday  7.282133e+10          1    PLUS AND MATERNITY   \n",
              "\n",
              "   FinelineNumber  \n",
              "0            4063  \n",
              "1            1605  \n",
              "2            4551  \n",
              "3             135  \n",
              "4             744  "
            ]
          },
          "execution_count": 54,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "test.head()"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "7049d801",
      "metadata": {
        "id": "7049d801",
        "outputId": "488ffe1b-414c-42c6-d10b-80b374de8187"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77181</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>2</td>\n",
              "      <td>MENS WEAR</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77182</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>2</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77183</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>1</td>\n",
              "      <td>IMPULSE MERCHANDISE</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77184</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77185</th>\n",
              "      <td>25</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>77186 rows × 4 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "       TripType Weekday  ScanCount DepartmentDescription\n",
              "0             7  Friday          1          FROZEN FOODS\n",
              "1             7  Friday          2          SERVICE DELI\n",
              "2            25  Friday          1            LADIESWEAR\n",
              "3            25  Friday          1            LADIESWEAR\n",
              "4            25  Friday          1           DSD GROCERY\n",
              "...         ...     ...        ...                   ...\n",
              "77181        25  Sunday          2             MENS WEAR\n",
              "77182        25  Sunday          2           DSD GROCERY\n",
              "77183        25  Sunday          1   IMPULSE MERCHANDISE\n",
              "77184        25  Sunday          1             MENS WEAR\n",
              "77185        25  Sunday          1             MENS WEAR\n",
              "\n",
              "[77186 rows x 4 columns]"
            ]
          },
          "execution_count": 55,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "t = train.drop(['VisitNumber','Upc','FinelineNumber'],axis = 1)\n",
        "t"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "3e0ee0a1",
      "metadata": {
        "id": "3e0ee0a1"
      },
      "outputs": [],
      "source": [
        "from sklearn.preprocessing import LabelEncoder\n",
        "label_encoder = LabelEncoder()\n",
        "\n",
        "t['Weekday_encoded'] = label_encoder.fit_transform(t['Weekday'])\n",
        "t['Dept_encoded'] = label_encoder.fit_transform(t['DepartmentDescription'])"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "e29530eb",
      "metadata": {
        "scrolled": true,
        "id": "e29530eb",
        "outputId": "677588e5-dec4-4aae-e3e1-0425e1faebe6"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>TripType</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>Weekday_encoded</th>\n",
              "      <th>Dept_encoded</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>7</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>0</td>\n",
              "      <td>20</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>7</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2</td>\n",
              "      <td>SERVICE DELI</td>\n",
              "      <td>0</td>\n",
              "      <td>56</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>0</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>0</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>0</td>\n",
              "      <td>16</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>5</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>LADIESWEAR</td>\n",
              "      <td>0</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>6</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>COMM BREAD</td>\n",
              "      <td>0</td>\n",
              "      <td>13</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>7</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>BAKERY</td>\n",
              "      <td>0</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>8</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>BAKERY</td>\n",
              "      <td>0</td>\n",
              "      <td>3</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>9</th>\n",
              "      <td>25</td>\n",
              "      <td>Friday</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>0</td>\n",
              "      <td>16</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   TripType Weekday  ScanCount DepartmentDescription  Weekday_encoded  \\\n",
              "0         7  Friday          1          FROZEN FOODS                0   \n",
              "1         7  Friday          2          SERVICE DELI                0   \n",
              "2        25  Friday          1            LADIESWEAR                0   \n",
              "3        25  Friday          1            LADIESWEAR                0   \n",
              "4        25  Friday          1           DSD GROCERY                0   \n",
              "5        25  Friday          1            LADIESWEAR                0   \n",
              "6        25  Friday          1            COMM BREAD                0   \n",
              "7        25  Friday          1                BAKERY                0   \n",
              "8        25  Friday          1                BAKERY                0   \n",
              "9        25  Friday          1           DSD GROCERY                0   \n",
              "\n",
              "   Dept_encoded  \n",
              "0            20  \n",
              "1            56  \n",
              "2            35  \n",
              "3            35  \n",
              "4            16  \n",
              "5            35  \n",
              "6            13  \n",
              "7             3  \n",
              "8             3  \n",
              "9            16  "
            ]
          },
          "execution_count": 57,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "t.head(10)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "b756e6c9",
      "metadata": {
        "id": "b756e6c9"
      },
      "outputs": [],
      "source": [
        "X = t.drop(['TripType','Weekday','DepartmentDescription'],axis = 1)\n",
        "y = t['TripType']"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "29780fe6",
      "metadata": {
        "id": "29780fe6"
      },
      "outputs": [],
      "source": [
        "from sklearn.model_selection import train_test_split\n",
        "x_train,x_test, y_train, y_test = train_test_split(X,y,test_size = 0.2,random_state = 42)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "4b84e74a",
      "metadata": {
        "id": "4b84e74a",
        "outputId": "074c7e72-97b4-4e71-c20f-3c82fe62d177"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>Weekday_encoded</th>\n",
              "      <th>Dept_encoded</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>20</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>2</td>\n",
              "      <td>0</td>\n",
              "      <td>56</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>16</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77181</th>\n",
              "      <td>2</td>\n",
              "      <td>3</td>\n",
              "      <td>40</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77182</th>\n",
              "      <td>2</td>\n",
              "      <td>3</td>\n",
              "      <td>16</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77183</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77184</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>40</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>77185</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>40</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>77186 rows × 3 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "       ScanCount  Weekday_encoded  Dept_encoded\n",
              "0              1                0            20\n",
              "1              2                0            56\n",
              "2              1                0            35\n",
              "3              1                0            35\n",
              "4              1                0            16\n",
              "...          ...              ...           ...\n",
              "77181          2                3            40\n",
              "77182          2                3            16\n",
              "77183          1                3            30\n",
              "77184          1                3            40\n",
              "77185          1                3            40\n",
              "\n",
              "[77186 rows x 3 columns]"
            ]
          },
          "execution_count": 60,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "X"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "fa2e1075",
      "metadata": {
        "id": "fa2e1075",
        "outputId": "06d26a56-6465-49f6-932a-96a1f122f0ed"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "0         7\n",
              "1         7\n",
              "2        25\n",
              "3        25\n",
              "4        25\n",
              "         ..\n",
              "77181    25\n",
              "77182    25\n",
              "77183    25\n",
              "77184    25\n",
              "77185    25\n",
              "Name: TripType, Length: 77186, dtype: int64"
            ]
          },
          "execution_count": 61,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "y"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "a929cf57",
      "metadata": {
        "id": "a929cf57"
      },
      "outputs": [],
      "source": [
        "from sklearn.ensemble import RandomForestClassifier"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "8e70f186",
      "metadata": {
        "id": "8e70f186",
        "outputId": "edefc9de-94ec-4dfd-c6d2-4159f37cb053"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "RandomForestClassifier(random_state=42)"
            ]
          },
          "execution_count": 63,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "model = RandomForestClassifier(n_estimators = 100, random_state = 42)\n",
        "model.fit(x_train,y_train)"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "23211183",
      "metadata": {
        "id": "23211183"
      },
      "outputs": [],
      "source": [
        "# evaluate the model"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "59ac0aaa",
      "metadata": {
        "id": "59ac0aaa",
        "outputId": "a224c4a5-09eb-4bd9-fc7a-e4d940862435"
      },
      "outputs": [
        {
          "data": {
            "text/plain": [
              "0.696268946754761"
            ]
          },
          "execution_count": 65,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "from sklearn.metrics import accuracy_score, classification_report\n",
        "\n",
        "y_pred = model.predict(x_test)\n",
        "acc = accuracy_score(y_test,y_pred)\n",
        "acc"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "2ed353df",
      "metadata": {
        "id": "2ed353df",
        "outputId": "463308d4-de76-40ba-c62b-88b36d46a7cc"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>87</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.106841e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4063</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>361</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.727878e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>1605</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>385</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.840007e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>4551</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>413</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.200000e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>IMPULSE MERCHANDISE</td>\n",
              "      <td>135</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>462</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.282133e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>PLUS AND MATERNITY</td>\n",
              "      <td>744</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2995</th>\n",
              "      <td>191158</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>5.010046e+09</td>\n",
              "      <td>5</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4138</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2996</th>\n",
              "      <td>191164</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>7.874235e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DAIRY</td>\n",
              "      <td>1508</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2997</th>\n",
              "      <td>191225</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>7.047049e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DAIRY</td>\n",
              "      <td>1344</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2998</th>\n",
              "      <td>191256</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>4.393559e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>5542</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2999</th>\n",
              "      <td>191337</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>2.259120e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MEAT - FRESH &amp; FROZEN</td>\n",
              "      <td>1301</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>3000 rows × 6 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "      VisitNumber Weekday           Upc  ScanCount  DepartmentDescription  \\\n",
              "0              87  Friday  7.106841e+09          1           FROZEN FOODS   \n",
              "1             361  Friday  6.727878e+10          1              MENS WEAR   \n",
              "2             385  Friday  2.840007e+09          1            DSD GROCERY   \n",
              "3             413  Friday  2.200000e+09          1    IMPULSE MERCHANDISE   \n",
              "4             462  Friday  7.282133e+10          1     PLUS AND MATERNITY   \n",
              "...           ...     ...           ...        ...                    ...   \n",
              "2995       191158  Sunday  5.010046e+09          5           FROZEN FOODS   \n",
              "2996       191164  Sunday  7.874235e+09          1                  DAIRY   \n",
              "2997       191225  Sunday  7.047049e+09          1                  DAIRY   \n",
              "2998       191256  Sunday  4.393559e+09          1              MENS WEAR   \n",
              "2999       191337  Sunday  2.259120e+10          1  MEAT - FRESH & FROZEN   \n",
              "\n",
              "      FinelineNumber  \n",
              "0               4063  \n",
              "1               1605  \n",
              "2               4551  \n",
              "3                135  \n",
              "4                744  \n",
              "...              ...  \n",
              "2995            4138  \n",
              "2996            1508  \n",
              "2997            1344  \n",
              "2998            5542  \n",
              "2999            1301  \n",
              "\n",
              "[3000 rows x 6 columns]"
            ]
          },
          "execution_count": 66,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "test"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "de70a0f2",
      "metadata": {
        "id": "de70a0f2",
        "outputId": "ab19915a-19c1-4b47-fc20-8af609125d3f"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>Weekday</th>\n",
              "      <th>Upc</th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>DepartmentDescription</th>\n",
              "      <th>FinelineNumber</th>\n",
              "      <th>Weekday_Encoded</th>\n",
              "      <th>DepartmentDescription_Encoded</th>\n",
              "      <th>Dept_encoded</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>87</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.106841e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4063</td>\n",
              "      <td>0</td>\n",
              "      <td>18</td>\n",
              "      <td>18</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>361</td>\n",
              "      <td>Friday</td>\n",
              "      <td>6.727878e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>1605</td>\n",
              "      <td>0</td>\n",
              "      <td>37</td>\n",
              "      <td>37</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>385</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.840007e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DSD GROCERY</td>\n",
              "      <td>4551</td>\n",
              "      <td>0</td>\n",
              "      <td>14</td>\n",
              "      <td>14</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>413</td>\n",
              "      <td>Friday</td>\n",
              "      <td>2.200000e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>IMPULSE MERCHANDISE</td>\n",
              "      <td>135</td>\n",
              "      <td>0</td>\n",
              "      <td>27</td>\n",
              "      <td>27</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>462</td>\n",
              "      <td>Friday</td>\n",
              "      <td>7.282133e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>PLUS AND MATERNITY</td>\n",
              "      <td>744</td>\n",
              "      <td>0</td>\n",
              "      <td>45</td>\n",
              "      <td>45</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2995</th>\n",
              "      <td>191158</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>5.010046e+09</td>\n",
              "      <td>5</td>\n",
              "      <td>FROZEN FOODS</td>\n",
              "      <td>4138</td>\n",
              "      <td>3</td>\n",
              "      <td>18</td>\n",
              "      <td>18</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2996</th>\n",
              "      <td>191164</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>7.874235e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DAIRY</td>\n",
              "      <td>1508</td>\n",
              "      <td>3</td>\n",
              "      <td>13</td>\n",
              "      <td>13</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2997</th>\n",
              "      <td>191225</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>7.047049e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>DAIRY</td>\n",
              "      <td>1344</td>\n",
              "      <td>3</td>\n",
              "      <td>13</td>\n",
              "      <td>13</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2998</th>\n",
              "      <td>191256</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>4.393559e+09</td>\n",
              "      <td>1</td>\n",
              "      <td>MENS WEAR</td>\n",
              "      <td>5542</td>\n",
              "      <td>3</td>\n",
              "      <td>37</td>\n",
              "      <td>37</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2999</th>\n",
              "      <td>191337</td>\n",
              "      <td>Sunday</td>\n",
              "      <td>2.259120e+10</td>\n",
              "      <td>1</td>\n",
              "      <td>MEAT - FRESH &amp; FROZEN</td>\n",
              "      <td>1301</td>\n",
              "      <td>3</td>\n",
              "      <td>35</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>3000 rows × 9 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "      VisitNumber Weekday           Upc  ScanCount  DepartmentDescription  \\\n",
              "0              87  Friday  7.106841e+09          1           FROZEN FOODS   \n",
              "1             361  Friday  6.727878e+10          1              MENS WEAR   \n",
              "2             385  Friday  2.840007e+09          1            DSD GROCERY   \n",
              "3             413  Friday  2.200000e+09          1    IMPULSE MERCHANDISE   \n",
              "4             462  Friday  7.282133e+10          1     PLUS AND MATERNITY   \n",
              "...           ...     ...           ...        ...                    ...   \n",
              "2995       191158  Sunday  5.010046e+09          5           FROZEN FOODS   \n",
              "2996       191164  Sunday  7.874235e+09          1                  DAIRY   \n",
              "2997       191225  Sunday  7.047049e+09          1                  DAIRY   \n",
              "2998       191256  Sunday  4.393559e+09          1              MENS WEAR   \n",
              "2999       191337  Sunday  2.259120e+10          1  MEAT - FRESH & FROZEN   \n",
              "\n",
              "      FinelineNumber  Weekday_Encoded  DepartmentDescription_Encoded  \\\n",
              "0               4063                0                             18   \n",
              "1               1605                0                             37   \n",
              "2               4551                0                             14   \n",
              "3                135                0                             27   \n",
              "4                744                0                             45   \n",
              "...              ...              ...                            ...   \n",
              "2995            4138                3                             18   \n",
              "2996            1508                3                             13   \n",
              "2997            1344                3                             13   \n",
              "2998            5542                3                             37   \n",
              "2999            1301                3                             35   \n",
              "\n",
              "      Dept_encoded  \n",
              "0               18  \n",
              "1               37  \n",
              "2               14  \n",
              "3               27  \n",
              "4               45  \n",
              "...            ...  \n",
              "2995            18  \n",
              "2996            13  \n",
              "2997            13  \n",
              "2998            37  \n",
              "2999            35  \n",
              "\n",
              "[3000 rows x 9 columns]"
            ]
          },
          "execution_count": 69,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "from sklearn.preprocessing import LabelEncoder\n",
        "label_encoder = LabelEncoder()\n",
        "\n",
        "# Label encode Weekday and DepartmentDescription\n",
        "test['Weekday_Encoded'] = label_encoder.fit_transform(test['Weekday'])\n",
        "test['Dept_encoded'] = label_encoder.fit_transform(test['DepartmentDescription'])\n",
        "\n",
        "test"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "e594b414",
      "metadata": {
        "id": "e594b414",
        "outputId": "7547cb23-0d8b-4eae-a4b8-6c30b09b700f"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>ScanCount</th>\n",
              "      <th>Weekday_Encoded</th>\n",
              "      <th>Dept_encoded</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>18</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>37</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>14</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>27</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>1</td>\n",
              "      <td>0</td>\n",
              "      <td>45</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2995</th>\n",
              "      <td>5</td>\n",
              "      <td>3</td>\n",
              "      <td>18</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2996</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>13</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2997</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>13</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2998</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>37</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2999</th>\n",
              "      <td>1</td>\n",
              "      <td>3</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>3000 rows × 3 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "      ScanCount  Weekday_Encoded  Dept_encoded\n",
              "0             1                0            18\n",
              "1             1                0            37\n",
              "2             1                0            14\n",
              "3             1                0            27\n",
              "4             1                0            45\n",
              "...         ...              ...           ...\n",
              "2995          5                3            18\n",
              "2996          1                3            13\n",
              "2997          1                3            13\n",
              "2998          1                3            37\n",
              "2999          1                3            35\n",
              "\n",
              "[3000 rows x 3 columns]"
            ]
          },
          "execution_count": 70,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "te = test.drop(['VisitNumber','Weekday','Upc','DepartmentDescription','DepartmentDescription_Encoded','FinelineNumber'],axis = 1)\n",
        "te"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "3c6d9c44",
      "metadata": {
        "id": "3c6d9c44",
        "outputId": "ab6fdcf8-d92f-4be9-a1ae-63295df0a07c"
      },
      "outputs": [
        {
          "name": "stderr",
          "output_type": "stream",
          "text": [
            "/Users/megnaroy/opt/anaconda3/lib/python3.9/site-packages/sklearn/base.py:493: FutureWarning: The feature names should match those that were passed during fit. Starting version 1.2, an error will be raised.\n",
            "Feature names unseen at fit time:\n",
            "- Weekday_Encoded\n",
            "Feature names seen at fit time, yet now missing:\n",
            "- Weekday_encoded\n",
            "\n",
            "  warnings.warn(message, FutureWarning)\n"
          ]
        },
        {
          "data": {
            "text/plain": [
              "array([25, 25, 25, ..., 38, 25, 25])"
            ]
          },
          "execution_count": 71,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "test_pred = model.predict(te)\n",
        "test_pred"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "900c3547",
      "metadata": {
        "id": "900c3547",
        "outputId": "bfa3ee77-1249-4b50-dfd4-3ce6ef426833"
      },
      "outputs": [
        {
          "data": {
            "text/html": [
              "<div>\n",
              "<style scoped>\n",
              "    .dataframe tbody tr th:only-of-type {\n",
              "        vertical-align: middle;\n",
              "    }\n",
              "\n",
              "    .dataframe tbody tr th {\n",
              "        vertical-align: top;\n",
              "    }\n",
              "\n",
              "    .dataframe thead th {\n",
              "        text-align: right;\n",
              "    }\n",
              "</style>\n",
              "<table border=\"1\" class=\"dataframe\">\n",
              "  <thead>\n",
              "    <tr style=\"text-align: right;\">\n",
              "      <th></th>\n",
              "      <th>VisitNumber</th>\n",
              "      <th>TripType</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <th>0</th>\n",
              "      <td>87</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>1</th>\n",
              "      <td>361</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2</th>\n",
              "      <td>385</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>3</th>\n",
              "      <td>413</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>4</th>\n",
              "      <td>462</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>...</th>\n",
              "      <td>...</td>\n",
              "      <td>...</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2995</th>\n",
              "      <td>191158</td>\n",
              "      <td>38</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2996</th>\n",
              "      <td>191164</td>\n",
              "      <td>38</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2997</th>\n",
              "      <td>191225</td>\n",
              "      <td>38</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2998</th>\n",
              "      <td>191256</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <th>2999</th>\n",
              "      <td>191337</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "<p>3000 rows × 2 columns</p>\n",
              "</div>"
            ],
            "text/plain": [
              "      VisitNumber  TripType\n",
              "0              87        25\n",
              "1             361        25\n",
              "2             385        25\n",
              "3             413        25\n",
              "4             462        25\n",
              "...           ...       ...\n",
              "2995       191158        38\n",
              "2996       191164        38\n",
              "2997       191225        38\n",
              "2998       191256        25\n",
              "2999       191337        25\n",
              "\n",
              "[3000 rows x 2 columns]"
            ]
          },
          "execution_count": 72,
          "metadata": {},
          "output_type": "execute_result"
        }
      ],
      "source": [
        "sub = pd.DataFrame({'VisitNumber':test['VisitNumber'],'TripType':test_pred})\n",
        "sub"
      ]
    },
    {
      "cell_type": "code",
      "execution_count": null,
      "id": "79546809",
      "metadata": {
        "id": "79546809"
      },
      "outputs": [],
      "source": []
    }
  ],
  "metadata": {
    "kernelspec": {
      "display_name": "Python 3 (ipykernel)",
      "language": "python",
      "name": "python3"
    },
    "language_info": {
      "codemirror_mode": {
        "name": "ipython",
        "version": 3
      },
      "file_extension": ".py",
      "mimetype": "text/x-python",
      "name": "python",
      "nbconvert_exporter": "python",
      "pygments_lexer": "ipython3",
      "version": "3.9.13"
    },
    "colab": {
      "provenance": [],
      "include_colab_link": true
    }
  },
  "nbformat": 4,
  "nbformat_minor": 5
}




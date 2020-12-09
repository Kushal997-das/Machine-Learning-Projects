{
  "nbformat": 4,
  "nbformat_minor": 0,
  "metadata": {
    "kernelspec": {
      "display_name": "Python 3",
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
      "version": "3.7.4"
    },
    "colab": {
      "name": "Task#2 The spark foundation .ipynb",
      "provenance": [],
      "include_colab_link": true
    }
  },
  "cells": [
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "view-in-github",
        "colab_type": "text"
      },
      "source": [
        "<a href=\"https://colab.research.google.com/github/Kushal997-das/THE-SPARKS-FOUNDATION/blob/master/Task%232%20The%20spark%20foundation%20.ipynb\" target=\"_parent\"><img src=\"https://colab.research.google.com/assets/colab-badge.svg\" alt=\"Open In Colab\"/></a>"
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "IY-5VlZdvp3-"
      },
      "source": [
        "# TO EXPLORE SUPERVISED MACHINE LEARNING (LINEAR REGRESSION) "
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "EYKkGfp1vp4H"
      },
      "source": [
        "##Importing important libraries---\n",
        "import pandas as pd\n",
        "import numpy as np\n",
        "import seaborn as sns\n",
        "import matplotlib.pyplot as plt\n",
        "%matplotlib inline"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "QLzz_DHYvp4O",
        "outputId": "e8d93dd6-f14d-407c-a476-9efc436ca7b7"
      },
      "source": [
        "##imprting Dataset-\n",
        "path =  \"http://bit.ly/w-data\"\n",
        "Data = pd.read_csv(path)\n",
        "print(\"Data is successfully imported\")\n",
        "Data"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Data is successfully imported\n"
          ],
          "name": "stdout"
        },
        {
          "output_type": "execute_result",
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
              "      <th>Hours</th>\n",
              "      <th>Scores</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <td>0</td>\n",
              "      <td>2.5</td>\n",
              "      <td>21</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>1</td>\n",
              "      <td>5.1</td>\n",
              "      <td>47</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>2</td>\n",
              "      <td>3.2</td>\n",
              "      <td>27</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>3</td>\n",
              "      <td>8.5</td>\n",
              "      <td>75</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>4</td>\n",
              "      <td>3.5</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>5</td>\n",
              "      <td>1.5</td>\n",
              "      <td>20</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>6</td>\n",
              "      <td>9.2</td>\n",
              "      <td>88</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>7</td>\n",
              "      <td>5.5</td>\n",
              "      <td>60</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>8</td>\n",
              "      <td>8.3</td>\n",
              "      <td>81</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>9</td>\n",
              "      <td>2.7</td>\n",
              "      <td>25</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>10</td>\n",
              "      <td>7.7</td>\n",
              "      <td>85</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>11</td>\n",
              "      <td>5.9</td>\n",
              "      <td>62</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>12</td>\n",
              "      <td>4.5</td>\n",
              "      <td>41</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>13</td>\n",
              "      <td>3.3</td>\n",
              "      <td>42</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>14</td>\n",
              "      <td>1.1</td>\n",
              "      <td>17</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>15</td>\n",
              "      <td>8.9</td>\n",
              "      <td>95</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>16</td>\n",
              "      <td>2.5</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>17</td>\n",
              "      <td>1.9</td>\n",
              "      <td>24</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>18</td>\n",
              "      <td>6.1</td>\n",
              "      <td>67</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>19</td>\n",
              "      <td>7.4</td>\n",
              "      <td>69</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>20</td>\n",
              "      <td>2.7</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>21</td>\n",
              "      <td>4.8</td>\n",
              "      <td>54</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>22</td>\n",
              "      <td>3.8</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>23</td>\n",
              "      <td>6.9</td>\n",
              "      <td>76</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>24</td>\n",
              "      <td>7.8</td>\n",
              "      <td>86</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "    Hours  Scores\n",
              "0     2.5      21\n",
              "1     5.1      47\n",
              "2     3.2      27\n",
              "3     8.5      75\n",
              "4     3.5      30\n",
              "5     1.5      20\n",
              "6     9.2      88\n",
              "7     5.5      60\n",
              "8     8.3      81\n",
              "9     2.7      25\n",
              "10    7.7      85\n",
              "11    5.9      62\n",
              "12    4.5      41\n",
              "13    3.3      42\n",
              "14    1.1      17\n",
              "15    8.9      95\n",
              "16    2.5      30\n",
              "17    1.9      24\n",
              "18    6.1      67\n",
              "19    7.4      69\n",
              "20    2.7      30\n",
              "21    4.8      54\n",
              "22    3.8      35\n",
              "23    6.9      76\n",
              "24    7.8      86"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 2
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "2Ng2v-2Dvp4T",
        "outputId": "f6a49618-18f4-43c8-8612-8783bf78bc51"
      },
      "source": [
        "## Now print the first 5 records...\n",
        "\n",
        "Data.head()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
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
              "      <th>Hours</th>\n",
              "      <th>Scores</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <td>0</td>\n",
              "      <td>2.5</td>\n",
              "      <td>21</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>1</td>\n",
              "      <td>5.1</td>\n",
              "      <td>47</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>2</td>\n",
              "      <td>3.2</td>\n",
              "      <td>27</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>3</td>\n",
              "      <td>8.5</td>\n",
              "      <td>75</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>4</td>\n",
              "      <td>3.5</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   Hours  Scores\n",
              "0    2.5      21\n",
              "1    5.1      47\n",
              "2    3.2      27\n",
              "3    8.5      75\n",
              "4    3.5      30"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 3
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "4hTcsGH7vp4W",
        "outputId": "0db1cfda-44ee-44aa-f951-590748f6e359"
      },
      "source": [
        "##Now print the last 5 records...\n",
        "Data.tail()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
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
              "      <th>Hours</th>\n",
              "      <th>Scores</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <td>20</td>\n",
              "      <td>2.7</td>\n",
              "      <td>30</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>21</td>\n",
              "      <td>4.8</td>\n",
              "      <td>54</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>22</td>\n",
              "      <td>3.8</td>\n",
              "      <td>35</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>23</td>\n",
              "      <td>6.9</td>\n",
              "      <td>76</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>24</td>\n",
              "      <td>7.8</td>\n",
              "      <td>86</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "    Hours  Scores\n",
              "20    2.7      30\n",
              "21    4.8      54\n",
              "22    3.8      35\n",
              "23    6.9      76\n",
              "24    7.8      86"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 4
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "sPRX6tWMvp4Z",
        "outputId": "46956956-e2b1-4f4d-c16b-2862a6f1bd56"
      },
      "source": [
        "#here we use describe() method so that we can able to see percentiles,mean,std,max,count of the given dataset.\n",
        "Data.describe()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
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
              "      <th>Hours</th>\n",
              "      <th>Scores</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <td>count</td>\n",
              "      <td>25.000000</td>\n",
              "      <td>25.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>mean</td>\n",
              "      <td>5.012000</td>\n",
              "      <td>51.480000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>std</td>\n",
              "      <td>2.525094</td>\n",
              "      <td>25.286887</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>min</td>\n",
              "      <td>1.100000</td>\n",
              "      <td>17.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>25%</td>\n",
              "      <td>2.700000</td>\n",
              "      <td>30.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>50%</td>\n",
              "      <td>4.800000</td>\n",
              "      <td>47.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>75%</td>\n",
              "      <td>7.400000</td>\n",
              "      <td>75.000000</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>max</td>\n",
              "      <td>9.200000</td>\n",
              "      <td>95.000000</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "           Hours     Scores\n",
              "count  25.000000  25.000000\n",
              "mean    5.012000  51.480000\n",
              "std     2.525094  25.286887\n",
              "min     1.100000  17.000000\n",
              "25%     2.700000  30.000000\n",
              "50%     4.800000  47.000000\n",
              "75%     7.400000  75.000000\n",
              "max     9.200000  95.000000"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 5
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "UZ8Hka6Kvp4c",
        "outputId": "a50810cf-720b-461f-804a-d4eb206f4de5"
      },
      "source": [
        "#Let's print the full summary of the dataframe .\n",
        "Data.info()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "<class 'pandas.core.frame.DataFrame'>\n",
            "RangeIndex: 25 entries, 0 to 24\n",
            "Data columns (total 2 columns):\n",
            "Hours     25 non-null float64\n",
            "Scores    25 non-null int64\n",
            "dtypes: float64(1), int64(1)\n",
            "memory usage: 528.0 bytes\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "rtVXa1xkvp4e"
      },
      "source": [
        "##importing libraries for plotting Graphs\n",
        "import seaborn as sns"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "ZCgClBglvp4g",
        "outputId": "1026334c-4eb0-4a6d-e5ac-7b93923db35b"
      },
      "source": [
        "plt.boxplot(Data)\n",
        "plt.show()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "bK7flMIBvp4k"
      },
      "source": [
        "## Visualizing Data."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "hrBGgMbhvp4k",
        "outputId": "592a6009-af6c-43ba-93ff-e2e1b15468da"
      },
      "source": [
        "##ploting Scatter plot----\n",
        "plt.xlabel('Hours',fontsize=15)\n",
        "plt.ylabel('Scores',fontsize=15)\n",
        "plt.title('Hours studied vs Score', fontsize=10)\n",
        "plt.scatter(Data.Hours,Data.Scores,color='blue',marker='*')\n",
        "plt.show()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "xXqJTvl0vp4m"
      },
      "source": [
        "## This \"SCATTER PLOT\" indicates positive linear relationship as much as hours You study is a chance of high scoring"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "X5dRxA5Rvp4m",
        "outputId": "38b1535d-0f3e-4aba-808e-dc54008277c1"
      },
      "source": [
        "X = Data.iloc[:,:-1].values\n",
        "Y = Data.iloc[:,1].values\n",
        "X"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([[2.5],\n",
              "       [5.1],\n",
              "       [3.2],\n",
              "       [8.5],\n",
              "       [3.5],\n",
              "       [1.5],\n",
              "       [9.2],\n",
              "       [5.5],\n",
              "       [8.3],\n",
              "       [2.7],\n",
              "       [7.7],\n",
              "       [5.9],\n",
              "       [4.5],\n",
              "       [3.3],\n",
              "       [1.1],\n",
              "       [8.9],\n",
              "       [2.5],\n",
              "       [1.9],\n",
              "       [6.1],\n",
              "       [7.4],\n",
              "       [2.7],\n",
              "       [4.8],\n",
              "       [3.8],\n",
              "       [6.9],\n",
              "       [7.8]])"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 29
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "BgYNghBpvp4o",
        "outputId": "90cdcae9-2d12-4726-d045-7688deb4abd8"
      },
      "source": [
        "Y"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([21, 47, 27, 75, 30, 20, 88, 60, 81, 25, 85, 62, 41, 42, 17, 95, 30,\n",
              "       24, 67, 69, 30, 54, 35, 76, 86], dtype=int64)"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 30
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "_DFZnC5Ovp4q"
      },
      "source": [
        "## Preparing Data and splitting into train and test sets."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "1oY_HaDyvp4r"
      },
      "source": [
        "from sklearn.model_selection import train_test_split\n",
        "X_train,X_test,Y_train,Y_test = train_test_split(X,Y,random_state = 0,test_size=0.2)"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "joXfLbJ5vp4s",
        "outputId": "90abdfbc-af02-4267-c6f5-6b0e764e7a9c"
      },
      "source": [
        "## We have Splitted Our Data Using 80:20 RULe(PARETO)\n",
        "print(\"X train.shape =\", X_train.shape)\n",
        "print(\"Y train.shape =\", Y_train.shape)\n",
        "print(\"X test.shape  =\", X_test.shape)\n",
        "print(\"Y test.shape  =\", Y_test.shape)\n"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "X train.shape = (20, 1)\n",
            "Y train.shape = (20,)\n",
            "X test.shape  = (5, 1)\n",
            "Y test.shape  = (5,)\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "xOBZB52Fvp4u"
      },
      "source": [
        "## Training the Model."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "V8FLHmItvp4v"
      },
      "source": [
        "from sklearn.linear_model import LinearRegression\n",
        "linreg=LinearRegression()"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "lI5wATf6vp4x",
        "outputId": "f5741b28-444f-4b54-c7cc-35b4b50d1d46"
      },
      "source": [
        "##Fitting Training Data\n",
        "linreg.fit(X_train,Y_train)\n",
        "print(\"Training our algorithm is finished\")"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Training our algorithm is finished\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "bMjrBmbYvp4z",
        "outputId": "b29e4af3-931c-437a-8fb7-f561622c4956"
      },
      "source": [
        "print(\"B0 =\",linreg.intercept_,\"\\nB1 =\",linreg.coef_)## β0 is Intercept & Slope of the line is β1.,\""
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "B0 = 2.018160041434683 \n",
            "B1 = [9.91065648]\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "Tyvf4B2ivp41"
      },
      "source": [
        "##plotting the REGRESSION LINE---\n",
        "Y0 = linreg.intercept_ + linreg.coef_*X_train"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "HuvUcKswvp43",
        "outputId": "6923a408-314f-452a-fbe4-99e81258d677"
      },
      "source": [
        "##plotting on train data\n",
        "plt.scatter(X_train,Y_train,color='green',marker='+')\n",
        "plt.plot(X_train,Y0,color='orange')\n",
        "plt.xlabel(\"Hours\",fontsize=15)\n",
        "plt.ylabel(\"Scores\",fontsize=15)\n",
        "plt.title(\"Regression line(Train set)\",fontsize=10)\n",
        "plt.show()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "QC5SMN1Hvp46"
      },
      "source": [
        "## Test Data."
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "P2TZozluvp46",
        "outputId": "506567b3-94e1-4ec1-9534-7481c2a92afb"
      },
      "source": [
        "Y_pred=linreg.predict(X_test)##predicting the Scores for test data\n",
        "print(Y_pred)"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "[16.88414476 33.73226078 75.357018   26.79480124 60.49103328]\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "9tsP8tfovp48",
        "outputId": "14df54a8-d855-48e0-e50f-691f5bdd7109"
      },
      "source": [
        "#now print the Y_test.\n",
        "Y_test"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "array([20, 27, 69, 30, 62], dtype=int64)"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 44
        }
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "iry9Jr72vp4-",
        "outputId": "6e70b59e-a6a0-462a-8d87-459eb9845c32"
      },
      "source": [
        "#plotting line on test data\n",
        "plt.plot(X_test,Y_pred,color='red')\n",
        "plt.scatter(X_test,Y_test,color='black',marker='+')\n",
        "plt.xlabel(\"Hours\",fontsize=15)\n",
        "plt.ylabel(\"Scores\",fontsize=15)\n",
        "plt.title(\"Regression line(Test set)\",fontsize=10)\n",
        "plt.show()"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "display_data",
          "data": {
            "image/png": "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\n",
            "text/plain": [
              "<Figure size 432x288 with 1 Axes>"
            ]
          },
          "metadata": {
            "tags": [],
            "needs_background": "light"
          }
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "4i13c0j7vp5A"
      },
      "source": [
        "## Comparing Actual vs Predicted Scores.¶"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "pmZ9c9KIvp5A",
        "outputId": "1268cf16-460b-4a76-a13f-f97efacc60d2"
      },
      "source": [
        "Y_test1 = list(Y_test)\n",
        "prediction=list(Y_pred)\n",
        "df_compare = pd.DataFrame({ 'Actual':Y_test1,'Result':prediction})\n",
        "df_compare"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
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
              "      <th>Actual</th>\n",
              "      <th>Result</th>\n",
              "    </tr>\n",
              "  </thead>\n",
              "  <tbody>\n",
              "    <tr>\n",
              "      <td>0</td>\n",
              "      <td>20</td>\n",
              "      <td>16.884145</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>1</td>\n",
              "      <td>27</td>\n",
              "      <td>33.732261</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>2</td>\n",
              "      <td>69</td>\n",
              "      <td>75.357018</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>3</td>\n",
              "      <td>30</td>\n",
              "      <td>26.794801</td>\n",
              "    </tr>\n",
              "    <tr>\n",
              "      <td>4</td>\n",
              "      <td>62</td>\n",
              "      <td>60.491033</td>\n",
              "    </tr>\n",
              "  </tbody>\n",
              "</table>\n",
              "</div>"
            ],
            "text/plain": [
              "   Actual     Result\n",
              "0      20  16.884145\n",
              "1      27  33.732261\n",
              "2      69  75.357018\n",
              "3      30  26.794801\n",
              "4      62  60.491033"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 48
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "i7eefjjKvp5D"
      },
      "source": [
        "## ACCURACY OF THE MODEL¶"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "YFoNtOkevp5D",
        "outputId": "5f43afcf-90a2-47f1-e5ef-17a57a629570"
      },
      "source": [
        "from sklearn import metrics\n",
        "metrics.r2_score(Y_test,Y_pred)##Goodness of fit Test"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "execute_result",
          "data": {
            "text/plain": [
              "0.9454906892105356"
            ]
          },
          "metadata": {
            "tags": []
          },
          "execution_count": 49
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "Jly05oP4vp5F"
      },
      "source": [
        "### Above 94% percentage indicates that above fitted Model is a GOOD MODEL. "
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "ukmz5crpvp5F"
      },
      "source": [
        "## Predicting the Error"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "A_klIK68vp5G"
      },
      "source": [
        "from sklearn.metrics import mean_squared_error,mean_absolute_error"
      ],
      "execution_count": null,
      "outputs": []
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "t9mlui33vp5I",
        "outputId": "e756d928-ea28-4c94-96e8-48a2d5f39fc6"
      },
      "source": [
        "MSE = metrics.mean_squared_error(Y_test,Y_pred)\n",
        "root_E = np.sqrt(metrics.mean_squared_error(Y_test,Y_pred))\n",
        "Abs_E = np.sqrt(metrics.mean_squared_error(Y_test,Y_pred))\n",
        "print(\"Mean Squared Error      = \",MSE)\n",
        "print(\"Root Mean Squared Error = \",root_E)\n",
        "print(\"Mean Absolute Error     = \",Abs_E)"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "Mean Squared Error      =  21.5987693072174\n",
            "Root Mean Squared Error =  4.6474476121003665\n",
            "Mean Absolute Error     =  4.6474476121003665\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "0xt6F5IQvp5K"
      },
      "source": [
        "## Predicting the score¶"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "AvSqSm93vp5K",
        "outputId": "f692979a-52bc-449c-e65a-bf8d45751759"
      },
      "source": [
        "Prediction_score = linreg.predict([[9.25]])\n",
        "print(\"predicted score for a student studying 9.25 hours :\",Prediction_score)"
      ],
      "execution_count": null,
      "outputs": [
        {
          "output_type": "stream",
          "text": [
            "predicted score for a student studying 9.25 hours : [93.69173249]\n"
          ],
          "name": "stdout"
        }
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "YaXPAsOHvp5M"
      },
      "source": [
        "## CONCLUSION: "
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "MF9d80LFvp5M"
      },
      "source": [
        "### From the above result we can say that if a studied for 9.25 then student will secured 93.69 MARKS."
      ]
    },
    {
      "cell_type": "markdown",
      "metadata": {
        "id": "OJvM5vPRvp5M"
      },
      "source": [
        "### Completed task#2"
      ]
    },
    {
      "cell_type": "code",
      "metadata": {
        "id": "uqLe9QLzvp5N"
      },
      "source": [
        ""
      ],
      "execution_count": null,
      "outputs": []
    }
  ]
}
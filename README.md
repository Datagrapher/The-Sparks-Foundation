# The-Sparks-Foundation
{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "2916c2bf",
   "metadata": {},
   "source": [
    "# The Sparks Foundation - Data Science & Business Analytics Internship"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a2c55526",
   "metadata": {},
   "source": [
    "## GRIP @ The Sparks Foundation"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "f8637328",
   "metadata": {},
   "source": [
    "### By : Tirthankar Sarkar "
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3083c6bc",
   "metadata": {},
   "source": [
    "## TASK 2 - Prediction using Unsupervised Machine Learning"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "df3e1462",
   "metadata": {},
   "source": [
    "In this task, we require to predict the optimum number of clusters for the iris data set using Unsupervised machine learning"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "7c0b35ce",
   "metadata": {},
   "source": [
    "## Steps :"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "d9c488ed",
   "metadata": {},
   "source": [
    "<ul>\n",
    "<li>Import libraries</li>\n",
    "<li>Read the data</li>\n",
    "<li>Explore the data</li>\n",
    "<li>Find the optimal number of clusters</li>\n",
    "<li>Bulid the model using K_means</li>\n",
    "<li>Visualising the clusters</li>\n",
    "</ul>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "deded88f",
   "metadata": {},
   "source": [
    "## Import libraties\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "7543a0bb",
   "metadata": {},
   "outputs": [],
   "source": [
    "import numpy as np \n",
    "import pandas as pd\n",
    "import matplotlib.pyplot as plt\n",
    "import seaborn as sns"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "29b7ccd6",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Reading the data from csv file"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "442d1cda",
   "metadata": {},
   "outputs": [],
   "source": [
    "df = pd.read_csv('Iris.xls')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "b3a8cf65",
   "metadata": {
    "scrolled": true
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
       "      <th>Id</th>\n",
       "      <th>SepalLengthCm</th>\n",
       "      <th>SepalWidthCm</th>\n",
       "      <th>PetalLengthCm</th>\n",
       "      <th>PetalWidthCm</th>\n",
       "      <th>Species</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>1</td>\n",
       "      <td>5.1</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>Iris-setosa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>2</td>\n",
       "      <td>4.9</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>Iris-setosa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>3</td>\n",
       "      <td>4.7</td>\n",
       "      <td>3.2</td>\n",
       "      <td>1.3</td>\n",
       "      <td>0.2</td>\n",
       "      <td>Iris-setosa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4</td>\n",
       "      <td>4.6</td>\n",
       "      <td>3.1</td>\n",
       "      <td>1.5</td>\n",
       "      <td>0.2</td>\n",
       "      <td>Iris-setosa</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5</td>\n",
       "      <td>5.0</td>\n",
       "      <td>3.6</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "      <td>Iris-setosa</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   Id  SepalLengthCm  SepalWidthCm  PetalLengthCm  PetalWidthCm      Species\n",
       "0   1            5.1           3.5            1.4           0.2  Iris-setosa\n",
       "1   2            4.9           3.0            1.4           0.2  Iris-setosa\n",
       "2   3            4.7           3.2            1.3           0.2  Iris-setosa\n",
       "3   4            4.6           3.1            1.5           0.2  Iris-setosa\n",
       "4   5            5.0           3.6            1.4           0.2  Iris-setosa"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c9514f62",
   "metadata": {},
   "source": [
    "## Explore the data"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "8116ec39",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 150 entries, 0 to 149\n",
      "Data columns (total 6 columns):\n",
      " #   Column         Non-Null Count  Dtype  \n",
      "---  ------         --------------  -----  \n",
      " 0   Id             150 non-null    int64  \n",
      " 1   SepalLengthCm  150 non-null    float64\n",
      " 2   SepalWidthCm   150 non-null    float64\n",
      " 3   PetalLengthCm  150 non-null    float64\n",
      " 4   PetalWidthCm   150 non-null    float64\n",
      " 5   Species        150 non-null    object \n",
      "dtypes: float64(4), int64(1), object(1)\n",
      "memory usage: 7.2+ KB\n"
     ]
    }
   ],
   "source": [
    "df.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "368d26ad",
   "metadata": {},
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
       "      <th>Id</th>\n",
       "      <th>SepalLengthCm</th>\n",
       "      <th>SepalWidthCm</th>\n",
       "      <th>PetalLengthCm</th>\n",
       "      <th>PetalWidthCm</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>count</th>\n",
       "      <td>150.000000</td>\n",
       "      <td>150.000000</td>\n",
       "      <td>150.000000</td>\n",
       "      <td>150.000000</td>\n",
       "      <td>150.000000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>mean</th>\n",
       "      <td>75.500000</td>\n",
       "      <td>5.843333</td>\n",
       "      <td>3.054000</td>\n",
       "      <td>3.758667</td>\n",
       "      <td>1.198667</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>std</th>\n",
       "      <td>43.445368</td>\n",
       "      <td>0.828066</td>\n",
       "      <td>0.433594</td>\n",
       "      <td>1.764420</td>\n",
       "      <td>0.763161</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>min</th>\n",
       "      <td>1.000000</td>\n",
       "      <td>4.300000</td>\n",
       "      <td>2.000000</td>\n",
       "      <td>1.000000</td>\n",
       "      <td>0.100000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>25%</th>\n",
       "      <td>38.250000</td>\n",
       "      <td>5.100000</td>\n",
       "      <td>2.800000</td>\n",
       "      <td>1.600000</td>\n",
       "      <td>0.300000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>50%</th>\n",
       "      <td>75.500000</td>\n",
       "      <td>5.800000</td>\n",
       "      <td>3.000000</td>\n",
       "      <td>4.350000</td>\n",
       "      <td>1.300000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>75%</th>\n",
       "      <td>112.750000</td>\n",
       "      <td>6.400000</td>\n",
       "      <td>3.300000</td>\n",
       "      <td>5.100000</td>\n",
       "      <td>1.800000</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>max</th>\n",
       "      <td>150.000000</td>\n",
       "      <td>7.900000</td>\n",
       "      <td>4.400000</td>\n",
       "      <td>6.900000</td>\n",
       "      <td>2.500000</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "               Id  SepalLengthCm  SepalWidthCm  PetalLengthCm  PetalWidthCm\n",
       "count  150.000000     150.000000    150.000000     150.000000    150.000000\n",
       "mean    75.500000       5.843333      3.054000       3.758667      1.198667\n",
       "std     43.445368       0.828066      0.433594       1.764420      0.763161\n",
       "min      1.000000       4.300000      2.000000       1.000000      0.100000\n",
       "25%     38.250000       5.100000      2.800000       1.600000      0.300000\n",
       "50%     75.500000       5.800000      3.000000       4.350000      1.300000\n",
       "75%    112.750000       6.400000      3.300000       5.100000      1.800000\n",
       "max    150.000000       7.900000      4.400000       6.900000      2.500000"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "3c5c58f4",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Id               0\n",
       "SepalLengthCm    0\n",
       "SepalWidthCm     0\n",
       "PetalLengthCm    0\n",
       "PetalWidthCm     0\n",
       "Species          0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "574757e1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Iris-setosa        50\n",
       "Iris-versicolor    50\n",
       "Iris-virginica     50\n",
       "Name: Species, dtype: int64"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "df.Species.value_counts()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "1844560b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<seaborn.axisgrid.FacetGrid at 0x24817524a88>"
      ]
     },
     "execution_count": 9,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 463.25x360 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.relplot(x='SepalLengthCm',y='PetalLengthCm',hue='Species',data=df)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "e82e321c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<seaborn.axisgrid.FacetGrid at 0x24819900c48>"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 463.25x360 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.relplot(x='SepalWidthCm',y='PetalWidthCm',hue='Species',data=df)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "e38f5da9",
   "metadata": {},
   "outputs": [],
   "source": [
    "data = df\n",
    "Iris_df = data.drop(columns= ['Species' ,'Id'] )"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "167d114e",
   "metadata": {},
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
       "      <th>SepalLengthCm</th>\n",
       "      <th>SepalWidthCm</th>\n",
       "      <th>PetalLengthCm</th>\n",
       "      <th>PetalWidthCm</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>5.1</td>\n",
       "      <td>3.5</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>4.9</td>\n",
       "      <td>3.0</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>4.7</td>\n",
       "      <td>3.2</td>\n",
       "      <td>1.3</td>\n",
       "      <td>0.2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>4.6</td>\n",
       "      <td>3.1</td>\n",
       "      <td>1.5</td>\n",
       "      <td>0.2</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>5.0</td>\n",
       "      <td>3.6</td>\n",
       "      <td>1.4</td>\n",
       "      <td>0.2</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "   SepalLengthCm  SepalWidthCm  PetalLengthCm  PetalWidthCm\n",
       "0            5.1           3.5            1.4           0.2\n",
       "1            4.9           3.0            1.4           0.2\n",
       "2            4.7           3.2            1.3           0.2\n",
       "3            4.6           3.1            1.5           0.2\n",
       "4            5.0           3.6            1.4           0.2"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Iris_df.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9c1c6959",
   "metadata": {},
   "source": [
    "## Find the optimal number of clusters"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "id": "20e3cd2c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Text(0, 0.5, 'Within-cluster Sum of Squares')"
      ]
     },
     "execution_count": 47,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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\n",
      "text/plain": [
       "<Figure size 648x432 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "from sklearn.cluster import KMeans\n",
    "plt.figure(figsize=(9,6))\n",
    "wcss = []\n",
    "# 'cl_num' is a that keeps track the highest number of clusters we want to use the WCSS method for.\n",
    "# Note that 'range' doesn't include the upper boundery\n",
    "cl_num = 11\n",
    "for i in range (1,cl_num):\n",
    "    kmeans= KMeans(i)\n",
    "    kmeans.fit(Iris_df)\n",
    "    wcss_iter = kmeans.inertia_\n",
    "    wcss.append(wcss_iter)\n",
    "\n",
    "number_clusters = range(1,cl_num)\n",
    "plt.plot(number_clusters, wcss,'bo--')\n",
    "plt.title('The Elbow Method')\n",
    "plt.xlabel('Number of clusters')\n",
    "plt.ylabel('Within-cluster Sum of Squares')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9adc2632",
   "metadata": {},
   "source": [
    "## Bulid the model using K_means"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "82aa96e0",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "78.94084142614601\n"
     ]
    }
   ],
   "source": [
    "from sklearn.cluster import KMeans\n",
    "model = KMeans(n_clusters = 3, init = 'k-means++', max_iter = 300, n_init = 10, random_state = 0)\n",
    "predictions = model.fit_predict(Iris_df)\n",
    "print(model.inertia_)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "bd51542e",
   "metadata": {},
   "source": [
    "## Visualising the clusters"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 51,
   "id": "f23efed1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAlMAAAGdCAYAAAA2S/axAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMSwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/YYfK9AAAACXBIWXMAAAsTAAALEwEAmpwYAABWU0lEQVR4nO3df3xT9b0/8NenaZuUtPJD+WErgxbjCCA2EOROr6yMyxjKUAd81asOrgr4Ra5M9F636e1Y53bd3cbcBnfilW0IDhS47uuQDh0uotPbayAZomELtHTQiiDF2qRN0p58vn+kzfojbZOcJCdJX8/Hgwfwyfnk8z7vc9K8e358jpBSgoiIiIjik6N1AERERESZjMUUERERkQospoiIiIhUYDFFREREpAKLKSIiIiIVWEwRERERqRB1MSWE0AkhHEKIfRFeWyGEOC+EcHb+uS+xYRIRERGlp9wYll0HwAXgkn5ef0FKuTbaN7vsssvkxIkTYxg+M3i9XhiNRq3DSDvMS/+Ym8iYl/4xN5ExL5ExL/2LJTeHDx/+WEo5OtJrURVTQogrANwE4LsA1kcb5EAmTpwIu92eiLdKKzabDRUVFVqHkXaYl/4xN5ExL/1jbiJjXiJjXvoXS26EEPX9vRbtab6nAPwrgOAAyywRQhwVQuwRQoyP8n2JiIiIMpoY7HEyQohFAG6UUq4RQlQAeERKuajXMpcC8Egp/UKI1QBuk1J+IcJ7rQKwCgDGjh07c9euXYlZizTi8XhQWFiodRhph3npH3MTGfPSP+YmMuYlMualf7HkZu7cuYellNZIr0VTTP07gLsBdAAwIHTN1H9LKe/qZ3kdgCYp5fCB3tdqtUqe5hs6mJf+MTeRMS/9Y24iY14iY176F+Npvn6LqUGvmZJSfgPANzrfqAKhI1M9CikhxOVSyg87/7sYoQvViYiIhrz29nacOXMGPp9Pk/GHDx8Ol4tfy5FEyo3BYMAVV1yBvLy8qN8nlrv5ehBCVAGwSylfBvCgEGIxQkevmgCsiPd9iYiIssmZM2dQVFSEiRMnQgiR8vFbWlpQVFSU8nEzQe/cSClx4cIFnDlzBqWlpVG/T0zFlJTSBsDW+e/Kbu3ho1dERET0Nz6fT7NCimIjhMCll16K8+fPx9SPM6ATERElGQupzBHPtmIxRURElOUGumPtuuuuS9q43/ve95L23umExRQREdEQ1NHRAQB4++23kzYGiykiIiLKKjabDTfccAMWL16MKVOmAPjbUasPP/wQc+bMQXl5OaZNm4Y333yzT//3338f1157LcrLyzF9+nS43W4AwI4dO8Ltq1evhqIo+PrXv462tjaUl5fjzjvvBABs3LgR06ZNw7Rp0/DUU08BCD3S5aabbsI111yDadOm4YUXXgAAVFVVYdasWZg2bRpWrVqFwaZy0lLcd/MRERFR4imKRLXNC8cHflim6LGwwgidLnHXXB05cgTHjh3rc7far3/9ayxYsACPPfYYFEVBa2trn75PP/001q1bhzvvvBOBQACKosDlcuGFF17AH//4R+Tl5WHNmjV4/vnn8eSTT2LTpk1wOp0AgMOHD+OXv/wlampqIKXE7Nmz8fnPfx61tbUoLi7GK6+8AgBobm4GAKxduxaVlaF73e6++27s27cPX/7ylxOWh0RiMUVERJQmFEViwfIG1Dh98LZJGAsEZpcbcGBbScIKqmuvvTbibf+zZs3CPffcg/b2dtxyyy0oLy/vs8znPvc5fPe738WZM2fwla98BSaTCQcPHsThw4cxa9YsAEBbWxvGjBnTp+9bb72FW2+9Nfxg4a985St488038aUvfQkPP/wwHn30USxatAg33HADAOAPf/gD/uM//gOtra1oamrC1KlT07aY4mk+IiKiNFFt86LG6YOnVUJKwNMqUeP0odrmTdgYXcVMb3PmzMGhQ4dQUlKCFStW4LnnnsNLL72E8vJylJeXw2634x//8R/x8ssvo6CgADfeeCNef/11SCmxfPlyOJ1OOJ1O/PnPf8aGDRuijueqq67CkSNHcPXVV+Pxxx9HVVUVfD4f1qxZgz179uC9997DypUrNZv0NBospoiGCEVRYLfb8eKLL8Jut0NRFK1DIqJeHB/44W3reW2Qt03C6Qokfez6+nqMHTsWK1euxH333YcjR47g1ltvDRdJVqsVtbW1KCsrw4MPPoibb74ZR48exbx587Bnzx6cO3cOANDU1IT6+noAQF5eHtrb2wEAN9xwA37zm9+gtbUVXq8XL730Em644QY0NjZi2LBhuOuuu/Av//IvOHLkSLhwuuyyy+DxeLBnz56kr78aPM1HNAQoioKqqiq43W74/X7o9XqYTCZUVlZCp9NpHR4RdbJM0cNYIOBp/VtBZSwQKDfnJ31s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\n",
      "text/plain": [
       "<Figure size 720x504 with 1 Axes>"
      ]
     },
     "metadata": {
      "needs_background": "light"
     },
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.figure(figsize=(10,7))\n",
    "X = Iris_df.iloc[:, [0, 1, 2, 3]].values\n",
    "plt.scatter(X[predictions == 0, 0], X[predictions == 0, 1], s = 25, c = '#0021DA', label = 'Iris-setosa')\n",
    "plt.scatter(X[predictions == 1, 0], X[predictions == 1, 1], s = 25, c = '#515151', label = 'Iris-versicolour')\n",
    "plt.scatter(X[predictions == 2, 0], X[predictions == 2, 1], s = 25, c = '#B87171', label = 'Iris-virginica')\n",
    "\n",
    "# Plotting the cluster centers\n",
    "\n",
    "plt.scatter(model.cluster_centers_[:, 0], model.cluster_centers_[:,1], s = 100, c = 'red', label = 'Centroids')\n",
    "plt.legend()\n",
    "plt.grid()\n",
    "plt.show()"
   ]
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
   "version": "3.7.11"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
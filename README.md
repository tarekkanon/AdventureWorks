---
jupyter:
  colab:
    gpuType: T4
  kernelspec:
    display_name: Python 3
    name: python3
  language_info:
    name: python
  nbformat: 4
  nbformat_minor: 0
---

::: {.cell .code execution_count="1" id="lT1eD1ZBR1i-"}
``` python
# imports
import pandas as pd
import datetime as dt
```
:::

::: {.cell .code execution_count="2" id="uPGAdeIhR7_V"}
``` python
# options
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', 20)
```
:::

::: {.cell .code execution_count="3" id="X_Sb3Nzkrzp4"}
``` python
df_sales = pd.read_csv('/content/drive/MyDrive/AnalysisData/fact_sales.csv', encoding='latin-1')
df_customers = pd.read_csv('/content/drive/MyDrive/AnalysisData/dim_customers.csv', encoding='latin-1')
df_sales_territory = pd.read_csv('/content/drive/MyDrive/AnalysisData/dim_sales_terrotry.csv', encoding='latin-1')
df_dates = pd.read_csv('/content/drive/MyDrive/AnalysisData/dim_date.csv', encoding='latin-1')
df_products = pd.read_csv('/content/drive/MyDrive/AnalysisData/dim_products.csv', encoding='latin-1')
df_geography = pd.read_csv('/content/drive/MyDrive/AnalysisData/dim_geography.csv', encoding='latin-1')
```
:::

::: {.cell .code execution_count="4" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":964}" id="4hnJlYJJQvQD" outputId="1f8eed4c-5ef4-41db-fa29-e269b036a0f4"}
``` python
df_customers
```

::: {.output .execute_result execution_count="4"}
```{=html}

  <div id="df-00f45bf4-e802-4587-8978-381c3f16a002" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CustomerKey</th>
      <th>GeographyKey</th>
      <th>CustomerAlternateKey</th>
      <th>Title</th>
      <th>FirstName</th>
      <th>MiddleName</th>
      <th>LastName</th>
      <th>NameStyle</th>
      <th>BirthDate</th>
      <th>MaritalStatus</th>
      <th>Suffix</th>
      <th>Gender</th>
      <th>EmailAddress</th>
      <th>YearlyIncome</th>
      <th>TotalChildren</th>
      <th>NumberChildrenAtHome</th>
      <th>EnglishEducation</th>
      <th>SpanishEducation</th>
      <th>FrenchEducation</th>
      <th>EnglishOccupation</th>
      <th>SpanishOccupation</th>
      <th>FrenchOccupation</th>
      <th>HouseOwnerFlag</th>
      <th>NumberCarsOwned</th>
      <th>AddressLine1</th>
      <th>AddressLine2</th>
      <th>Phone</th>
      <th>DateFirstPurchase</th>
      <th>CommuteDistance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11000</td>
      <td>26</td>
      <td>AW00011000</td>
      <td>NaN</td>
      <td>Jon</td>
      <td>V</td>
      <td>Yang</td>
      <td>False</td>
      <td>23-Dec-62</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>jon24@adventure-works.com</td>
      <td>$90,000.00</td>
      <td>2</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>0</td>
      <td>3761 N. 14th St</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0162</td>
      <td>22-Jul-05</td>
      <td>1-2 Miles</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11001</td>
      <td>37</td>
      <td>AW00011001</td>
      <td>NaN</td>
      <td>Eugene</td>
      <td>L</td>
      <td>Huang</td>
      <td>False</td>
      <td>23-Jun-76</td>
      <td>S</td>
      <td>NaN</td>
      <td>M</td>
      <td>eugene10@adventure-works.com</td>
      <td>$60,000.00</td>
      <td>3</td>
      <td>3</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>1</td>
      <td>2243 W St.</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0110</td>
      <td>18-Jul-05</td>
      <td>0-1 Miles</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11002</td>
      <td>31</td>
      <td>AW00011002</td>
      <td>NaN</td>
      <td>Ruben</td>
      <td>NaN</td>
      <td>Torres</td>
      <td>False</td>
      <td>19-Aug-66</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>ruben35@adventure-works.com</td>
      <td>$60,000.00</td>
      <td>3</td>
      <td>3</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>1</td>
      <td>5844 Linden Land</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0184</td>
      <td>10-Jul-05</td>
      <td>2-5 Miles</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11003</td>
      <td>11</td>
      <td>AW00011003</td>
      <td>NaN</td>
      <td>Christy</td>
      <td>NaN</td>
      <td>Zhu</td>
      <td>False</td>
      <td>09-Dec-87</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>christy12@adventure-works.com</td>
      <td>$70,000.00</td>
      <td>0</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>1</td>
      <td>1825 Village Pl.</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0162</td>
      <td>01-Jul-05</td>
      <td>5-10 Miles</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11004</td>
      <td>19</td>
      <td>AW00011004</td>
      <td>NaN</td>
      <td>Elizabeth</td>
      <td>NaN</td>
      <td>Johnson</td>
      <td>False</td>
      <td>06-Jun-90</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>elizabeth5@adventure-works.com</td>
      <td>$80,000.00</td>
      <td>5</td>
      <td>5</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>4</td>
      <td>7553 Harness Circle</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0131</td>
      <td>26-Jul-05</td>
      <td>1-2 Miles</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18479</th>
      <td>29479</td>
      <td>209</td>
      <td>AW00029479</td>
      <td>NaN</td>
      <td>Tommy</td>
      <td>L</td>
      <td>Tang</td>
      <td>False</td>
      <td>13-May-96</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>tommy2@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>1</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>111, rue Maillard</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0136</td>
      <td>08-Mar-07</td>
      <td>0-1 Miles</td>
    </tr>
    <tr>
      <th>18480</th>
      <td>29480</td>
      <td>248</td>
      <td>AW00029480</td>
      <td>NaN</td>
      <td>Nina</td>
      <td>W</td>
      <td>Raji</td>
      <td>False</td>
      <td>21-Sep-71</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>nina21@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>9 Katherine Drive</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0146</td>
      <td>18-Jan-08</td>
      <td>0-1 Miles</td>
    </tr>
    <tr>
      <th>18481</th>
      <td>29481</td>
      <td>120</td>
      <td>AW00029481</td>
      <td>NaN</td>
      <td>Ivan</td>
      <td>NaN</td>
      <td>Suri</td>
      <td>False</td>
      <td>16-Nov-93</td>
      <td>S</td>
      <td>NaN</td>
      <td>M</td>
      <td>ivan0@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>0</td>
      <td>0</td>
      <td>Knaackstr 4</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0144</td>
      <td>13-Feb-06</td>
      <td>0-1 Miles</td>
    </tr>
    <tr>
      <th>18482</th>
      <td>29482</td>
      <td>179</td>
      <td>AW00029482</td>
      <td>NaN</td>
      <td>Clayton</td>
      <td>NaN</td>
      <td>Zhang</td>
      <td>False</td>
      <td>08-Apr-78</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>clayton0@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>1080, quai de Grenelle</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0137</td>
      <td>22-Mar-07</td>
      <td>0-1 Miles</td>
    </tr>
    <tr>
      <th>18483</th>
      <td>29483</td>
      <td>217</td>
      <td>AW00029483</td>
      <td>NaN</td>
      <td>Jésus</td>
      <td>L</td>
      <td>Navarro</td>
      <td>False</td>
      <td>08-May-86</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>jésus9@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>0</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>244, rue de la Centenaire</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0141</td>
      <td>13-Mar-07</td>
      <td>0-1 Miles</td>
    </tr>
  </tbody>
</table>
<p>18484 rows × 29 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-00f45bf4-e802-4587-8978-381c3f16a002')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-00f45bf4-e802-4587-8978-381c3f16a002 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-00f45bf4-e802-4587-8978-381c3f16a002');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-064f5818-5c40-4ee3-9a17-ca818621e55a">
  <button class="colab-df-quickchart" onclick="quickchart('df-064f5818-5c40-4ee3-9a17-ca818621e55a')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-064f5818-5c40-4ee3-9a17-ca818621e55a button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_003c9dfe-b6f9-4f0f-8d82-892e100b993f">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_customers')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_003c9dfe-b6f9-4f0f-8d82-892e100b993f button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_customers');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="5" id="Y4pKfnzKTs-i"}
``` python
# fixing date issue wrong century #BUG with python library

def fix_date(x):

    if x.year > 2024:
        year = x.year - 100
    elif x.year < 1900:
        year = x.year + 100
    else:
        year = x.year

    return dt.date(year,x.month,x.day)
```
:::

::: {.cell .code execution_count="6" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="DumHKZvCRbcZ" outputId="a81a3a9f-5eb1-4833-8243-8d67f435823e"}
``` python
# fix dates first
df_customers["BirthDate"] = pd.to_datetime(df_customers['BirthDate'])
df_customers["BirthDate"] = df_customers["BirthDate"].apply(fix_date)

# add calculated column for age
df_customers['age'] = df_customers["BirthDate"].apply(lambda x : (pd.datetime.now().year - x.year))
```

::: {.output .stream .stderr}
    <ipython-input-6-3d19f54c3c4e>:6: FutureWarning: The pandas.datetime class is deprecated and will be removed from pandas in a future version. Import from datetime module instead.
      df_customers['age'] = df_customers["BirthDate"].apply(lambda x : (pd.datetime.now().year - x.year))
:::
:::

::: {.cell .code execution_count="7" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="_fJqVAYaSKuL" outputId="006ba650-673b-4f80-f07a-72ff7621d6bc"}
``` python
df_customers["BirthDate"]
```

::: {.output .execute_result execution_count="7"}
    0        1962-12-23
    1        1976-06-23
    2        1966-08-19
    3        1987-12-09
    4        1990-06-06
                ...    
    18479    1996-05-13
    18480    1971-09-21
    18481    1993-11-16
    18482    1978-04-08
    18483    1986-05-08
    Name: BirthDate, Length: 18484, dtype: object
:::
:::

::: {.cell .code execution_count="8" id="viAt4ajGyt_e"}
``` python
# average age of customers
cust_avg_age = df_customers['age'].mean()

# total customers
total_customers = df_customers['CustomerKey'].count()

# total distinct customers (making sure no duplicates)
total_unqiue_customers = len(pd.unique(df_customers['CustomerKey']))
```
:::

::: {.cell .code execution_count="9" colab="{\"base_uri\":\"https://localhost:8080/\"}" id="fkB1lmvGViA3" outputId="0aeed791-55f7-49c6-ba03-a284cb8c4247"}
``` python
print('Customers average age: ' + str(cust_avg_age))
print('Total count of customers: ' + str(total_customers))
print('Total unique count of customers: ' + str(total_unqiue_customers))
```

::: {.output .stream .stdout}
    Customers average age: 44.45017312270071
    Total count of customers: 18484
    Total unique count of customers: 18484
:::
:::

::: {.cell .code execution_count="10" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":443}" id="nTnqI7maW75Q" outputId="ec0b3fad-0578-446c-a79b-fbbb60c30240"}
``` python
df_sales
```

::: {.output .execute_result execution_count="10"}
```{=html}

  <div id="df-70190471-5530-4b5e-8faf-faef4b4778cd" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ProductKey</th>
      <th>OrderDateKey</th>
      <th>DueDateKey</th>
      <th>ShipDateKey</th>
      <th>CustomerKey</th>
      <th>PromotionKey</th>
      <th>CurrencyKey</th>
      <th>SalesTerritoryKey</th>
      <th>SalesOrderNumber</th>
      <th>SalesOrderLineNumber</th>
      <th>RevisionNumber</th>
      <th>OrderQuantity</th>
      <th>UnitPrice</th>
      <th>ExtendedAmount</th>
      <th>UnitPriceDiscountPct</th>
      <th>DiscountAmount</th>
      <th>ProductStandardCost</th>
      <th>TotalProductCost</th>
      <th>SalesAmount</th>
      <th>TaxAmt</th>
      <th>Freight</th>
      <th>CarrierTrackingNumber</th>
      <th>CustomerPONumber</th>
      <th>OrderDate</th>
      <th>DueDate</th>
      <th>ShipDate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>344</td>
      <td>20050722</td>
      <td>20050803</td>
      <td>20050729</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO43793</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>$3,399.99</td>
      <td>$3,399.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1,912.15</td>
      <td>$1,912.15</td>
      <td>$3,399.99</td>
      <td>$272.00</td>
      <td>$85.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2021</td>
      <td>03/08/2021</td>
      <td>29/07/2021</td>
    </tr>
    <tr>
      <th>1</th>
      <td>353</td>
      <td>20070722</td>
      <td>20070803</td>
      <td>20070729</td>
      <td>11000</td>
      <td>2</td>
      <td>6</td>
      <td>9</td>
      <td>SO51522</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>$2,319.99</td>
      <td>$2,319.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1,265.62</td>
      <td>$1,265.62</td>
      <td>$2,319.99</td>
      <td>$185.60</td>
      <td>$58.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2022</td>
      <td>03/08/2022</td>
      <td>29/07/2022</td>
    </tr>
    <tr>
      <th>2</th>
      <td>485</td>
      <td>20070722</td>
      <td>20070803</td>
      <td>20070729</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO51522</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>$21.98</td>
      <td>$21.98</td>
      <td>0</td>
      <td>0</td>
      <td>$8.22</td>
      <td>$8.22</td>
      <td>$21.98</td>
      <td>$1.76</td>
      <td>$0.55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2022</td>
      <td>03/08/2022</td>
      <td>29/07/2022</td>
    </tr>
    <tr>
      <th>3</th>
      <td>573</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>$2,384.07</td>
      <td>$2,384.07</td>
      <td>0</td>
      <td>0</td>
      <td>$1,481.94</td>
      <td>$1,481.94</td>
      <td>$2,384.07</td>
      <td>$190.73</td>
      <td>$59.60</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
    </tr>
    <tr>
      <th>4</th>
      <td>541</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>$28.99</td>
      <td>$28.99</td>
      <td>0</td>
      <td>0</td>
      <td>$10.84</td>
      <td>$10.84</td>
      <td>$28.99</td>
      <td>$2.32</td>
      <td>$0.72</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>60393</th>
      <td>217</td>
      <td>20080118</td>
      <td>20080130</td>
      <td>20080125</td>
      <td>29480</td>
      <td>1</td>
      <td>98</td>
      <td>10</td>
      <td>SO62341</td>
      <td>4</td>
      <td>1</td>
      <td>16</td>
      <td>$34.99</td>
      <td>$34.99</td>
      <td>0</td>
      <td>0</td>
      <td>$13.09</td>
      <td>$13.09</td>
      <td>$34.99</td>
      <td>$2.80</td>
      <td>$0.87</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18/01/2022</td>
      <td>30/01/2022</td>
      <td>25/01/2022</td>
    </tr>
    <tr>
      <th>60394</th>
      <td>225</td>
      <td>20080118</td>
      <td>20080130</td>
      <td>20080125</td>
      <td>29480</td>
      <td>1</td>
      <td>98</td>
      <td>10</td>
      <td>SO62341</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
      <td>$8.99</td>
      <td>$8.99</td>
      <td>0</td>
      <td>0</td>
      <td>$6.92</td>
      <td>$6.92</td>
      <td>$8.99</td>
      <td>$0.72</td>
      <td>$0.22</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>18/01/2022</td>
      <td>30/01/2022</td>
      <td>25/01/2022</td>
    </tr>
    <tr>
      <th>60395</th>
      <td>349</td>
      <td>20060213</td>
      <td>20060225</td>
      <td>20060220</td>
      <td>29481</td>
      <td>1</td>
      <td>100</td>
      <td>8</td>
      <td>SO45427</td>
      <td>1</td>
      <td>1</td>
      <td>13</td>
      <td>$3,374.99</td>
      <td>$3,374.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1,898.09</td>
      <td>$1,898.09</td>
      <td>$3,374.99</td>
      <td>$270.00</td>
      <td>$84.37</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13/02/2021</td>
      <td>25/02/2021</td>
      <td>20/02/2021</td>
    </tr>
    <tr>
      <th>60396</th>
      <td>358</td>
      <td>20070322</td>
      <td>20070403</td>
      <td>20070329</td>
      <td>29482</td>
      <td>1</td>
      <td>100</td>
      <td>7</td>
      <td>SO49746</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>$2,049.10</td>
      <td>$2,049.10</td>
      <td>0</td>
      <td>0</td>
      <td>$1,105.81</td>
      <td>$1,105.81</td>
      <td>$2,049.10</td>
      <td>$163.93</td>
      <td>$51.23</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/03/2022</td>
      <td>03/04/2022</td>
      <td>29/03/2022</td>
    </tr>
    <tr>
      <th>60397</th>
      <td>360</td>
      <td>20070313</td>
      <td>20070325</td>
      <td>20070320</td>
      <td>29483</td>
      <td>1</td>
      <td>100</td>
      <td>7</td>
      <td>SO49665</td>
      <td>1</td>
      <td>1</td>
      <td>7</td>
      <td>$2,049.10</td>
      <td>$2,049.10</td>
      <td>0</td>
      <td>0</td>
      <td>$1,105.81</td>
      <td>$1,105.81</td>
      <td>$2,049.10</td>
      <td>$163.93</td>
      <td>$51.23</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>13/03/2022</td>
      <td>25/03/2022</td>
      <td>20/03/2022</td>
    </tr>
  </tbody>
</table>
<p>60398 rows × 26 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-70190471-5530-4b5e-8faf-faef4b4778cd')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-70190471-5530-4b5e-8faf-faef4b4778cd button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-70190471-5530-4b5e-8faf-faef4b4778cd');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-db3d80f0-fd4d-4472-9296-e02f02b4702d">
  <button class="colab-df-quickchart" onclick="quickchart('df-db3d80f0-fd4d-4472-9296-e02f02b4702d')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-db3d80f0-fd4d-4472-9296-e02f02b4702d button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_562d206b-6d4a-47d7-87f2-d57c9c7df13f">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_sales')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_562d206b-6d4a-47d7-87f2-d57c9c7df13f button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_sales');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="11" id="UNI4BThIgBqJ"}
``` python
# we need to fix the sales amount since it is string and contain dollar sign
df_sales['SalesAmountFix'] = (df_sales['SalesAmount'].str[1:]).str.replace(',','').astype(float)
```
:::

::: {.cell .code execution_count="12" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":423}" id="N_CEGlEuYpdT" outputId="bbc09ccd-f4cf-4655-d440-3f6b77007a19"}
``` python
# create dataframe for all customers orders count and total amount
df_customers_orders = df_sales.groupby('CustomerKey', as_index=False).agg(**{'CountSalesOrders' : ('SalesOrderNumber' , 'nunique'), 'TotalAmount' : ('SalesAmountFix' , 'sum')}).reset_index()
df_customers_orders
```

::: {.output .execute_result execution_count="12"}
```{=html}

  <div id="df-482daf16-0713-4891-b442-42d33e9b6051" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CustomerKey</th>
      <th>CountSalesOrders</th>
      <th>TotalAmount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>11000</td>
      <td>3</td>
      <td>8248.99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>11001</td>
      <td>3</td>
      <td>6383.88</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>11002</td>
      <td>3</td>
      <td>8114.04</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>11003</td>
      <td>3</td>
      <td>8139.29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>11004</td>
      <td>3</td>
      <td>8196.01</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18479</th>
      <td>18479</td>
      <td>29479</td>
      <td>1</td>
      <td>2049.10</td>
    </tr>
    <tr>
      <th>18480</th>
      <td>18480</td>
      <td>29480</td>
      <td>1</td>
      <td>2442.03</td>
    </tr>
    <tr>
      <th>18481</th>
      <td>18481</td>
      <td>29481</td>
      <td>1</td>
      <td>3374.99</td>
    </tr>
    <tr>
      <th>18482</th>
      <td>18482</td>
      <td>29482</td>
      <td>1</td>
      <td>2049.10</td>
    </tr>
    <tr>
      <th>18483</th>
      <td>18483</td>
      <td>29483</td>
      <td>1</td>
      <td>2049.10</td>
    </tr>
  </tbody>
</table>
<p>18484 rows × 4 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-482daf16-0713-4891-b442-42d33e9b6051')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-482daf16-0713-4891-b442-42d33e9b6051 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-482daf16-0713-4891-b442-42d33e9b6051');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-4a7bb5fd-07a6-42e5-b5cc-c1ab42dfe909">
  <button class="colab-df-quickchart" onclick="quickchart('df-4a7bb5fd-07a6-42e5-b5cc-c1ab42dfe909')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-4a7bb5fd-07a6-42e5-b5cc-c1ab42dfe909 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_53268745-7710-4d09-9a31-609fc08a2a77">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_customers_orders')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_53268745-7710-4d09-9a31-609fc08a2a77 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_customers_orders');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="13" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":320}" id="FS5W1E4fbUdW" outputId="bf2551a4-a11f-4fde-e8e2-71f95836a9da"}
``` python
# to make sure count and sum is correct
df_test_result = df_sales[(df_sales['CustomerKey'] == 11000)]
df_test_result
```

::: {.output .execute_result execution_count="13"}
```{=html}

  <div id="df-ed57fe77-f48e-4fb9-a099-a42a41e14480" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ProductKey</th>
      <th>OrderDateKey</th>
      <th>DueDateKey</th>
      <th>ShipDateKey</th>
      <th>CustomerKey</th>
      <th>PromotionKey</th>
      <th>CurrencyKey</th>
      <th>SalesTerritoryKey</th>
      <th>SalesOrderNumber</th>
      <th>SalesOrderLineNumber</th>
      <th>RevisionNumber</th>
      <th>OrderQuantity</th>
      <th>UnitPrice</th>
      <th>ExtendedAmount</th>
      <th>UnitPriceDiscountPct</th>
      <th>DiscountAmount</th>
      <th>ProductStandardCost</th>
      <th>TotalProductCost</th>
      <th>SalesAmount</th>
      <th>TaxAmt</th>
      <th>Freight</th>
      <th>CarrierTrackingNumber</th>
      <th>CustomerPONumber</th>
      <th>OrderDate</th>
      <th>DueDate</th>
      <th>ShipDate</th>
      <th>SalesAmountFix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>344</td>
      <td>20050722</td>
      <td>20050803</td>
      <td>20050729</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO43793</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>$3,399.99</td>
      <td>$3,399.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1,912.15</td>
      <td>$1,912.15</td>
      <td>$3,399.99</td>
      <td>$272.00</td>
      <td>$85.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2021</td>
      <td>03/08/2021</td>
      <td>29/07/2021</td>
      <td>3399.99</td>
    </tr>
    <tr>
      <th>1</th>
      <td>353</td>
      <td>20070722</td>
      <td>20070803</td>
      <td>20070729</td>
      <td>11000</td>
      <td>2</td>
      <td>6</td>
      <td>9</td>
      <td>SO51522</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>$2,319.99</td>
      <td>$2,319.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1,265.62</td>
      <td>$1,265.62</td>
      <td>$2,319.99</td>
      <td>$185.60</td>
      <td>$58.00</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2022</td>
      <td>03/08/2022</td>
      <td>29/07/2022</td>
      <td>2319.99</td>
    </tr>
    <tr>
      <th>2</th>
      <td>485</td>
      <td>20070722</td>
      <td>20070803</td>
      <td>20070729</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO51522</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>$21.98</td>
      <td>$21.98</td>
      <td>0</td>
      <td>0</td>
      <td>$8.22</td>
      <td>$8.22</td>
      <td>$21.98</td>
      <td>$1.76</td>
      <td>$0.55</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>22/07/2022</td>
      <td>03/08/2022</td>
      <td>29/07/2022</td>
      <td>21.98</td>
    </tr>
    <tr>
      <th>3</th>
      <td>573</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>$2,384.07</td>
      <td>$2,384.07</td>
      <td>0</td>
      <td>0</td>
      <td>$1,481.94</td>
      <td>$1,481.94</td>
      <td>$2,384.07</td>
      <td>$190.73</td>
      <td>$59.60</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
      <td>2384.07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>541</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>$28.99</td>
      <td>$28.99</td>
      <td>0</td>
      <td>0</td>
      <td>$10.84</td>
      <td>$10.84</td>
      <td>$28.99</td>
      <td>$2.32</td>
      <td>$0.72</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
      <td>28.99</td>
    </tr>
    <tr>
      <th>5</th>
      <td>530</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>$4.99</td>
      <td>$4.99</td>
      <td>0</td>
      <td>0</td>
      <td>$1.87</td>
      <td>$1.87</td>
      <td>$4.99</td>
      <td>$0.40</td>
      <td>$0.12</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
      <td>4.99</td>
    </tr>
    <tr>
      <th>6</th>
      <td>214</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>$34.99</td>
      <td>$34.99</td>
      <td>0</td>
      <td>0</td>
      <td>$13.09</td>
      <td>$13.09</td>
      <td>$34.99</td>
      <td>$2.80</td>
      <td>$0.87</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
      <td>34.99</td>
    </tr>
    <tr>
      <th>7</th>
      <td>488</td>
      <td>20071104</td>
      <td>20071116</td>
      <td>20071111</td>
      <td>11000</td>
      <td>1</td>
      <td>6</td>
      <td>9</td>
      <td>SO57418</td>
      <td>5</td>
      <td>1</td>
      <td>1</td>
      <td>$53.99</td>
      <td>$53.99</td>
      <td>0</td>
      <td>0</td>
      <td>$41.57</td>
      <td>$41.57</td>
      <td>$53.99</td>
      <td>$4.32</td>
      <td>$1.35</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>04/11/2022</td>
      <td>16/11/2022</td>
      <td>11/11/2022</td>
      <td>53.99</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-ed57fe77-f48e-4fb9-a099-a42a41e14480')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-ed57fe77-f48e-4fb9-a099-a42a41e14480 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-ed57fe77-f48e-4fb9-a099-a42a41e14480');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-fb1d69cf-b979-45d1-b2d3-2baf4eaf332c">
  <button class="colab-df-quickchart" onclick="quickchart('df-fb1d69cf-b979-45d1-b2d3-2baf4eaf332c')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-fb1d69cf-b979-45d1-b2d3-2baf4eaf332c button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_7f071622-d243-40fc-8492-4b094c5cd85d">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_test_result')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_7f071622-d243-40fc-8492-4b094c5cd85d button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_test_result');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="14" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":423}" id="IcY8Cn52cYEA" outputId="ee081306-d0f0-42af-c14f-2ce0e252e0e6"}
``` python
# categorizing customers
df_customers_orders['CustomerCategory'] = df_customers_orders.loc[:,'CustomerCategory']= ['VIP' if d1>=2 and d2>=100 else 'Loyal' if d1>=2 else 'Periodic buyers' for d1,d2 in zip(df_customers_orders.CountSalesOrders,df_customers_orders.TotalAmount)]
df_customers_orders.head(100)
```

::: {.output .execute_result execution_count="14"}
```{=html}

  <div id="df-5ba47d5a-95c4-4c2f-ac16-f963731e5e74" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>CustomerKey</th>
      <th>CountSalesOrders</th>
      <th>TotalAmount</th>
      <th>CustomerCategory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>11000</td>
      <td>3</td>
      <td>8248.99</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>11001</td>
      <td>3</td>
      <td>6383.88</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>11002</td>
      <td>3</td>
      <td>8114.04</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>11003</td>
      <td>3</td>
      <td>8139.29</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>11004</td>
      <td>3</td>
      <td>8196.01</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>95</th>
      <td>95</td>
      <td>11095</td>
      <td>3</td>
      <td>8158.01</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>96</th>
      <td>96</td>
      <td>11096</td>
      <td>3</td>
      <td>8063.04</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>97</th>
      <td>97</td>
      <td>11097</td>
      <td>3</td>
      <td>8099.03</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>98</th>
      <td>98</td>
      <td>11098</td>
      <td>3</td>
      <td>88.96</td>
      <td>Loyal</td>
    </tr>
    <tr>
      <th>99</th>
      <td>99</td>
      <td>11099</td>
      <td>3</td>
      <td>8215.99</td>
      <td>VIP</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 5 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-5ba47d5a-95c4-4c2f-ac16-f963731e5e74')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-5ba47d5a-95c4-4c2f-ac16-f963731e5e74 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-5ba47d5a-95c4-4c2f-ac16-f963731e5e74');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-469f1849-8898-4df3-8dd5-53c0df69d246">
  <button class="colab-df-quickchart" onclick="quickchart('df-469f1849-8898-4df3-8dd5-53c0df69d246')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-469f1849-8898-4df3-8dd5-53c0df69d246 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="15" id="nNozTWi4mh2z"}
``` python
# add flag for having childern or no
df_customers['HaveChildern'] = [True if d1>0 else False for d1 in df_customers.TotalChildren]
```
:::

::: {.cell .code execution_count="16" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":964}" id="AhFmvrLToKRC" outputId="04f252e9-aeb4-4669-c1e9-acd4f5f2d7f2"}
``` python
# join 2 dataframes together for customers and customer orders and total amounts
df_customers_revenue = pd.concat([df_customers.set_index('CustomerKey'), df_customers_orders.set_index('CustomerKey')], axis=1, join='inner').reset_index()
df_customers_revenue
```

::: {.output .execute_result execution_count="16"}
```{=html}

  <div id="df-88b24dbe-84cd-40e6-8ffc-2e8f40450afd" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CustomerKey</th>
      <th>GeographyKey</th>
      <th>CustomerAlternateKey</th>
      <th>Title</th>
      <th>FirstName</th>
      <th>MiddleName</th>
      <th>LastName</th>
      <th>NameStyle</th>
      <th>BirthDate</th>
      <th>MaritalStatus</th>
      <th>Suffix</th>
      <th>Gender</th>
      <th>EmailAddress</th>
      <th>YearlyIncome</th>
      <th>TotalChildren</th>
      <th>NumberChildrenAtHome</th>
      <th>EnglishEducation</th>
      <th>SpanishEducation</th>
      <th>FrenchEducation</th>
      <th>EnglishOccupation</th>
      <th>SpanishOccupation</th>
      <th>FrenchOccupation</th>
      <th>HouseOwnerFlag</th>
      <th>NumberCarsOwned</th>
      <th>AddressLine1</th>
      <th>AddressLine2</th>
      <th>Phone</th>
      <th>DateFirstPurchase</th>
      <th>CommuteDistance</th>
      <th>age</th>
      <th>HaveChildern</th>
      <th>index</th>
      <th>CountSalesOrders</th>
      <th>TotalAmount</th>
      <th>CustomerCategory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>11000</td>
      <td>26</td>
      <td>AW00011000</td>
      <td>NaN</td>
      <td>Jon</td>
      <td>V</td>
      <td>Yang</td>
      <td>False</td>
      <td>1962-12-23</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>jon24@adventure-works.com</td>
      <td>$90,000.00</td>
      <td>2</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>0</td>
      <td>3761 N. 14th St</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0162</td>
      <td>22-Jul-05</td>
      <td>1-2 Miles</td>
      <td>62</td>
      <td>True</td>
      <td>0</td>
      <td>3</td>
      <td>8248.99</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11001</td>
      <td>37</td>
      <td>AW00011001</td>
      <td>NaN</td>
      <td>Eugene</td>
      <td>L</td>
      <td>Huang</td>
      <td>False</td>
      <td>1976-06-23</td>
      <td>S</td>
      <td>NaN</td>
      <td>M</td>
      <td>eugene10@adventure-works.com</td>
      <td>$60,000.00</td>
      <td>3</td>
      <td>3</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>1</td>
      <td>2243 W St.</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0110</td>
      <td>18-Jul-05</td>
      <td>0-1 Miles</td>
      <td>48</td>
      <td>True</td>
      <td>1</td>
      <td>3</td>
      <td>6383.88</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11002</td>
      <td>31</td>
      <td>AW00011002</td>
      <td>NaN</td>
      <td>Ruben</td>
      <td>NaN</td>
      <td>Torres</td>
      <td>False</td>
      <td>1966-08-19</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>ruben35@adventure-works.com</td>
      <td>$60,000.00</td>
      <td>3</td>
      <td>3</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>1</td>
      <td>5844 Linden Land</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0184</td>
      <td>10-Jul-05</td>
      <td>2-5 Miles</td>
      <td>58</td>
      <td>True</td>
      <td>2</td>
      <td>3</td>
      <td>8114.04</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>3</th>
      <td>11003</td>
      <td>11</td>
      <td>AW00011003</td>
      <td>NaN</td>
      <td>Christy</td>
      <td>NaN</td>
      <td>Zhu</td>
      <td>False</td>
      <td>1987-12-09</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>christy12@adventure-works.com</td>
      <td>$70,000.00</td>
      <td>0</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>1</td>
      <td>1825 Village Pl.</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0162</td>
      <td>01-Jul-05</td>
      <td>5-10 Miles</td>
      <td>37</td>
      <td>False</td>
      <td>3</td>
      <td>3</td>
      <td>8139.29</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>4</th>
      <td>11004</td>
      <td>19</td>
      <td>AW00011004</td>
      <td>NaN</td>
      <td>Elizabeth</td>
      <td>NaN</td>
      <td>Johnson</td>
      <td>False</td>
      <td>1990-06-06</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>elizabeth5@adventure-works.com</td>
      <td>$80,000.00</td>
      <td>5</td>
      <td>5</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>4</td>
      <td>7553 Harness Circle</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0131</td>
      <td>26-Jul-05</td>
      <td>1-2 Miles</td>
      <td>34</td>
      <td>True</td>
      <td>4</td>
      <td>3</td>
      <td>8196.01</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>18479</th>
      <td>29479</td>
      <td>209</td>
      <td>AW00029479</td>
      <td>NaN</td>
      <td>Tommy</td>
      <td>L</td>
      <td>Tang</td>
      <td>False</td>
      <td>1996-05-13</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>tommy2@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>1</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>111, rue Maillard</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0136</td>
      <td>08-Mar-07</td>
      <td>0-1 Miles</td>
      <td>28</td>
      <td>True</td>
      <td>18479</td>
      <td>1</td>
      <td>2049.10</td>
      <td>Periodic buyers</td>
    </tr>
    <tr>
      <th>18480</th>
      <td>29480</td>
      <td>248</td>
      <td>AW00029480</td>
      <td>NaN</td>
      <td>Nina</td>
      <td>W</td>
      <td>Raji</td>
      <td>False</td>
      <td>1971-09-21</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>nina21@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>9 Katherine Drive</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0146</td>
      <td>18-Jan-08</td>
      <td>0-1 Miles</td>
      <td>53</td>
      <td>True</td>
      <td>18480</td>
      <td>1</td>
      <td>2442.03</td>
      <td>Periodic buyers</td>
    </tr>
    <tr>
      <th>18481</th>
      <td>29481</td>
      <td>120</td>
      <td>AW00029481</td>
      <td>NaN</td>
      <td>Ivan</td>
      <td>NaN</td>
      <td>Suri</td>
      <td>False</td>
      <td>1993-11-16</td>
      <td>S</td>
      <td>NaN</td>
      <td>M</td>
      <td>ivan0@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Graduate Degree</td>
      <td>Estudios de postgrado</td>
      <td>Bac + 3</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>0</td>
      <td>0</td>
      <td>Knaackstr 4</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0144</td>
      <td>13-Feb-06</td>
      <td>0-1 Miles</td>
      <td>31</td>
      <td>True</td>
      <td>18481</td>
      <td>1</td>
      <td>3374.99</td>
      <td>Periodic buyers</td>
    </tr>
    <tr>
      <th>18482</th>
      <td>29482</td>
      <td>179</td>
      <td>AW00029482</td>
      <td>NaN</td>
      <td>Clayton</td>
      <td>NaN</td>
      <td>Zhang</td>
      <td>False</td>
      <td>1978-04-08</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>clayton0@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>3</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>1080, quai de Grenelle</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0137</td>
      <td>22-Mar-07</td>
      <td>0-1 Miles</td>
      <td>46</td>
      <td>True</td>
      <td>18482</td>
      <td>1</td>
      <td>2049.10</td>
      <td>Periodic buyers</td>
    </tr>
    <tr>
      <th>18483</th>
      <td>29483</td>
      <td>217</td>
      <td>AW00029483</td>
      <td>NaN</td>
      <td>Jésus</td>
      <td>L</td>
      <td>Navarro</td>
      <td>False</td>
      <td>1986-05-08</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>jésus9@adventure-works.com</td>
      <td>$30,000.00</td>
      <td>0</td>
      <td>0</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Clerical</td>
      <td>Administrativo</td>
      <td>Employé</td>
      <td>1</td>
      <td>0</td>
      <td>244, rue de la Centenaire</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0141</td>
      <td>13-Mar-07</td>
      <td>0-1 Miles</td>
      <td>38</td>
      <td>False</td>
      <td>18483</td>
      <td>1</td>
      <td>2049.10</td>
      <td>Periodic buyers</td>
    </tr>
  </tbody>
</table>
<p>18484 rows × 35 columns</p>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-88b24dbe-84cd-40e6-8ffc-2e8f40450afd')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-88b24dbe-84cd-40e6-8ffc-2e8f40450afd button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-88b24dbe-84cd-40e6-8ffc-2e8f40450afd');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-4d6ca70c-3817-4665-babe-40f2a3d703f8">
  <button class="colab-df-quickchart" onclick="quickchart('df-4d6ca70c-3817-4665-babe-40f2a3d703f8')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-4d6ca70c-3817-4665-babe-40f2a3d703f8 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_64bb5af4-e8d0-4e0f-97e7-553b1a10ca9c">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_customers_revenue')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_64bb5af4-e8d0-4e0f-97e7-553b1a10ca9c button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_customers_revenue');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="17" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":125}" id="erVSqu-SqAbu" outputId="b276117a-97e2-436b-d11b-42c671e3149e"}
``` python
# get total revenue based on customers having childern or not
df_customers_revenue_child = df_customers_revenue.groupby('HaveChildern', as_index=False).agg(**{'SumTotalAmount' : ('TotalAmount' , 'sum')}).reset_index()
df_customers_revenue_child
```

::: {.output .execute_result execution_count="17"}
```{=html}

  <div id="df-7918c478-b41a-4761-bff7-0bf5bfe89302" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>HaveChildern</th>
      <th>SumTotalAmount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>False</td>
      <td>8634027.29</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>True</td>
      <td>20724650.60</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-7918c478-b41a-4761-bff7-0bf5bfe89302')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-7918c478-b41a-4761-bff7-0bf5bfe89302 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-7918c478-b41a-4761-bff7-0bf5bfe89302');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-ca7a5876-7c85-40f2-b31f-249d24ecdd68">
  <button class="colab-df-quickchart" onclick="quickchart('df-ca7a5876-7c85-40f2-b31f-249d24ecdd68')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-ca7a5876-7c85-40f2-b31f-249d24ecdd68 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_e6251100-27af-46c3-b9f8-7412fae5d888">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_customers_revenue_child')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_e6251100-27af-46c3-b9f8-7412fae5d888 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_customers_revenue_child');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="18" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":125}" id="okMqNjoTrp1H" outputId="2a3994d5-b66b-4d8a-f50c-f8f567e6093b"}
``` python
# get total revenue based on customers gender
df_customers_revenue_gender = df_customers_revenue.groupby('Gender', as_index=False).agg(**{'SumTotalAmount' : ('TotalAmount' , 'sum')}).reset_index()
df_customers_revenue_gender
```

::: {.output .execute_result execution_count="18"}
```{=html}

  <div id="df-9e807ee5-a084-4f0a-84af-19652cc693fa" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>index</th>
      <th>Gender</th>
      <th>SumTotalAmount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>F</td>
      <td>14813619.09</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>M</td>
      <td>14545058.80</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-9e807ee5-a084-4f0a-84af-19652cc693fa')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-9e807ee5-a084-4f0a-84af-19652cc693fa button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-9e807ee5-a084-4f0a-84af-19652cc693fa');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-c7e783bc-9442-4aa5-912a-2270c3ed26d8">
  <button class="colab-df-quickchart" onclick="quickchart('df-c7e783bc-9442-4aa5-912a-2270c3ed26d8')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-c7e783bc-9442-4aa5-912a-2270c3ed26d8 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_282c85e0-7196-41ec-b50d-8df671ce59f5">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_customers_revenue_gender')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_282c85e0-7196-41ec-b50d-8df671ce59f5 button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_customers_revenue_gender');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

::: {.cell .code execution_count="19" colab="{\"base_uri\":\"https://localhost:8080/\",\"height\":903}" id="d-rfcliGsD2n" outputId="aca4b7fd-f7f1-408f-97ca-82dea7d8b62c"}
``` python
# get top 10 customers who spent more
df_top_customers = df_customers_revenue.sort_values('TotalAmount', ascending=False).head(10)
df_top_customers
```

::: {.output .execute_result execution_count="19"}
```{=html}

  <div id="df-04823755-567b-4188-887e-c78a45192f93" class="colab-df-container">
    <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>CustomerKey</th>
      <th>GeographyKey</th>
      <th>CustomerAlternateKey</th>
      <th>Title</th>
      <th>FirstName</th>
      <th>MiddleName</th>
      <th>LastName</th>
      <th>NameStyle</th>
      <th>BirthDate</th>
      <th>MaritalStatus</th>
      <th>Suffix</th>
      <th>Gender</th>
      <th>EmailAddress</th>
      <th>YearlyIncome</th>
      <th>TotalChildren</th>
      <th>NumberChildrenAtHome</th>
      <th>EnglishEducation</th>
      <th>SpanishEducation</th>
      <th>FrenchEducation</th>
      <th>EnglishOccupation</th>
      <th>SpanishOccupation</th>
      <th>FrenchOccupation</th>
      <th>HouseOwnerFlag</th>
      <th>NumberCarsOwned</th>
      <th>AddressLine1</th>
      <th>AddressLine2</th>
      <th>Phone</th>
      <th>DateFirstPurchase</th>
      <th>CommuteDistance</th>
      <th>age</th>
      <th>HaveChildern</th>
      <th>index</th>
      <th>CountSalesOrders</th>
      <th>TotalAmount</th>
      <th>CustomerCategory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1301</th>
      <td>12301</td>
      <td>223</td>
      <td>AW00012301</td>
      <td>NaN</td>
      <td>Nichole</td>
      <td>NaN</td>
      <td>Nara</td>
      <td>False</td>
      <td>1988-11-03</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>nichole16@adventure-works.com</td>
      <td>$100,000.00</td>
      <td>2</td>
      <td>3</td>
      <td>Bachelors</td>
      <td>Licenciatura</td>
      <td>Bac + 4</td>
      <td>Management</td>
      <td>Gestión</td>
      <td>Direction</td>
      <td>1</td>
      <td>4</td>
      <td>21, avenue de la Gare</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0152</td>
      <td>10-Nov-05</td>
      <td>10+ Miles</td>
      <td>36</td>
      <td>True</td>
      <td>1301</td>
      <td>5</td>
      <td>13295.38</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1132</th>
      <td>12132</td>
      <td>224</td>
      <td>AW00012132</td>
      <td>NaN</td>
      <td>Kaitlyn</td>
      <td>J</td>
      <td>Henderson</td>
      <td>False</td>
      <td>1961-07-06</td>
      <td>M</td>
      <td>NaN</td>
      <td>F</td>
      <td>kaitlyn72@adventure-works.com</td>
      <td>$110,000.00</td>
      <td>3</td>
      <td>4</td>
      <td>Partial College</td>
      <td>Estudios universitarios (en curso)</td>
      <td>Baccalauréat</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>4</td>
      <td>2222, rue Ste-Honoré</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0154</td>
      <td>02-Aug-05</td>
      <td>5-10 Miles</td>
      <td>63</td>
      <td>True</td>
      <td>1132</td>
      <td>5</td>
      <td>13294.27</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1308</th>
      <td>12308</td>
      <td>184</td>
      <td>AW00012308</td>
      <td>NaN</td>
      <td>Margaret</td>
      <td>NaN</td>
      <td>He</td>
      <td>False</td>
      <td>1994-01-16</td>
      <td>M</td>
      <td>NaN</td>
      <td>F</td>
      <td>margaret25@adventure-works.com</td>
      <td>$100,000.00</td>
      <td>3</td>
      <td>4</td>
      <td>High School</td>
      <td>Educación secundaria</td>
      <td>Bac + 2</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>2</td>
      <td>12bis, boulevard du Montparnasse</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0112</td>
      <td>04-Dec-05</td>
      <td>10+ Miles</td>
      <td>30</td>
      <td>True</td>
      <td>1308</td>
      <td>5</td>
      <td>13269.27</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1131</th>
      <td>12131</td>
      <td>186</td>
      <td>AW00012131</td>
      <td>NaN</td>
      <td>Randall</td>
      <td>M</td>
      <td>Dominguez</td>
      <td>False</td>
      <td>1988-04-06</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>randall14@adventure-works.com</td>
      <td>$90,000.00</td>
      <td>2</td>
      <td>1</td>
      <td>High School</td>
      <td>Educación secundaria</td>
      <td>Bac + 2</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>2</td>
      <td>244, rue des Rosiers</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0136</td>
      <td>24-Aug-05</td>
      <td>2-5 Miles</td>
      <td>36</td>
      <td>True</td>
      <td>1131</td>
      <td>5</td>
      <td>13265.99</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1300</th>
      <td>12300</td>
      <td>180</td>
      <td>AW00012300</td>
      <td>NaN</td>
      <td>Adriana</td>
      <td>L</td>
      <td>Gonzalez</td>
      <td>False</td>
      <td>1966-07-21</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>adriana19@adventure-works.com</td>
      <td>$80,000.00</td>
      <td>5</td>
      <td>0</td>
      <td>Partial College</td>
      <td>Estudios universitarios (en curso)</td>
      <td>Baccalauréat</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>2</td>
      <td>310, rue des Rosiers</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0129</td>
      <td>24-Nov-05</td>
      <td>10+ Miles</td>
      <td>58</td>
      <td>True</td>
      <td>1300</td>
      <td>5</td>
      <td>13242.70</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1321</th>
      <td>12321</td>
      <td>211</td>
      <td>AW00012321</td>
      <td>NaN</td>
      <td>Rosa</td>
      <td>K</td>
      <td>Hu</td>
      <td>False</td>
      <td>1964-10-14</td>
      <td>M</td>
      <td>NaN</td>
      <td>F</td>
      <td>rosa20@adventure-works.com</td>
      <td>$70,000.00</td>
      <td>5</td>
      <td>2</td>
      <td>Partial High School</td>
      <td>Educación secundaria (en curso)</td>
      <td>Niveau bac</td>
      <td>Skilled Manual</td>
      <td>Obrero especializado</td>
      <td>Technicien</td>
      <td>1</td>
      <td>2</td>
      <td>28, place du Tertre</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0192</td>
      <td>03-Dec-05</td>
      <td>2-5 Miles</td>
      <td>60</td>
      <td>True</td>
      <td>1321</td>
      <td>5</td>
      <td>13215.65</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1124</th>
      <td>12124</td>
      <td>192</td>
      <td>AW00012124</td>
      <td>NaN</td>
      <td>Brandi</td>
      <td>D</td>
      <td>Gill</td>
      <td>False</td>
      <td>1971-06-14</td>
      <td>S</td>
      <td>NaN</td>
      <td>F</td>
      <td>brandi13@adventure-works.com</td>
      <td>$110,000.00</td>
      <td>2</td>
      <td>4</td>
      <td>Partial College</td>
      <td>Estudios universitarios (en curso)</td>
      <td>Baccalauréat</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>3</td>
      <td>8, rue de l´Avenir</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0115</td>
      <td>01-Aug-05</td>
      <td>5-10 Miles</td>
      <td>53</td>
      <td>True</td>
      <td>1124</td>
      <td>5</td>
      <td>13195.64</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1307</th>
      <td>12307</td>
      <td>226</td>
      <td>AW00012307</td>
      <td>NaN</td>
      <td>Brad</td>
      <td>NaN</td>
      <td>She</td>
      <td>False</td>
      <td>1963-01-11</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>brad1@adventure-works.com</td>
      <td>$90,000.00</td>
      <td>4</td>
      <td>2</td>
      <td>High School</td>
      <td>Educación secundaria</td>
      <td>Bac + 2</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>1</td>
      <td>1</td>
      <td>12, rue Henri Gagnon</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0136</td>
      <td>29-Nov-05</td>
      <td>2-5 Miles</td>
      <td>61</td>
      <td>True</td>
      <td>1307</td>
      <td>5</td>
      <td>13173.19</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>1296</th>
      <td>12296</td>
      <td>211</td>
      <td>AW00012296</td>
      <td>NaN</td>
      <td>Francisco</td>
      <td>A</td>
      <td>Sara</td>
      <td>False</td>
      <td>1998-08-29</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>francisco11@adventure-works.com</td>
      <td>$70,000.00</td>
      <td>5</td>
      <td>1</td>
      <td>High School</td>
      <td>Educación secundaria</td>
      <td>Bac + 2</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>2</td>
      <td>24, rue Descartes</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0166</td>
      <td>19-Nov-05</td>
      <td>2-5 Miles</td>
      <td>26</td>
      <td>True</td>
      <td>1296</td>
      <td>5</td>
      <td>13164.64</td>
      <td>VIP</td>
    </tr>
    <tr>
      <th>433</th>
      <td>11433</td>
      <td>224</td>
      <td>AW00011433</td>
      <td>NaN</td>
      <td>Maurice</td>
      <td>M</td>
      <td>Shan</td>
      <td>False</td>
      <td>1996-04-27</td>
      <td>M</td>
      <td>NaN</td>
      <td>M</td>
      <td>maurice11@adventure-works.com</td>
      <td>$80,000.00</td>
      <td>5</td>
      <td>2</td>
      <td>High School</td>
      <td>Educación secundaria</td>
      <td>Bac + 2</td>
      <td>Professional</td>
      <td>Profesional</td>
      <td>Cadre</td>
      <td>0</td>
      <td>2</td>
      <td>59, rue Montcalm</td>
      <td>NaN</td>
      <td>1 (11) 500 555-0130</td>
      <td>05-Jun-07</td>
      <td>2-5 Miles</td>
      <td>28</td>
      <td>True</td>
      <td>433</td>
      <td>6</td>
      <td>12909.67</td>
      <td>VIP</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-04823755-567b-4188-887e-c78a45192f93')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-04823755-567b-4188-887e-c78a45192f93 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-04823755-567b-4188-887e-c78a45192f93');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-65d66b62-7c62-4769-a8ea-06e39d943601">
  <button class="colab-df-quickchart" onclick="quickchart('df-65d66b62-7c62-4769-a8ea-06e39d943601')"
            title="Suggest charts"
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

  <script>
    async function quickchart(key) {
      const quickchartButtonEl =
        document.querySelector('#' + key + ' button');
      quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
      quickchartButtonEl.classList.add('colab-df-spinner');
      try {
        const charts = await google.colab.kernel.invokeFunction(
            'suggestCharts', [key], {});
      } catch (error) {
        console.error('Error during call to suggestCharts:', error);
      }
      quickchartButtonEl.classList.remove('colab-df-spinner');
      quickchartButtonEl.classList.add('colab-df-quickchart-complete');
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-65d66b62-7c62-4769-a8ea-06e39d943601 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>

  <div id="id_29830098-b25a-488e-b5a7-95e310e0a96a">
    <style>
      .colab-df-generate {
        background-color: #E8F0FE;
        border: none;
        border-radius: 50%;
        cursor: pointer;
        display: none;
        fill: #1967D2;
        height: 32px;
        padding: 0 0 0 0;
        width: 32px;
      }

      .colab-df-generate:hover {
        background-color: #E2EBFA;
        box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
        fill: #174EA6;
      }

      [theme=dark] .colab-df-generate {
        background-color: #3B4455;
        fill: #D2E3FC;
      }

      [theme=dark] .colab-df-generate:hover {
        background-color: #434B5C;
        box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
        filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
        fill: #FFFFFF;
      }
    </style>
    <button class="colab-df-generate" onclick="generateWithVariable('df_top_customers')"
            title="Generate code using this dataframe."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M7,19H8.4L18.45,9,17,7.55,7,17.6ZM5,21V16.75L18.45,3.32a2,2,0,0,1,2.83,0l1.4,1.43a1.91,1.91,0,0,1,.58,1.4,1.91,1.91,0,0,1-.58,1.4L9.25,21ZM18.45,9,17,7.55Zm-12,3A5.31,5.31,0,0,0,4.9,8.1,5.31,5.31,0,0,0,1,6.5,5.31,5.31,0,0,0,4.9,4.9,5.31,5.31,0,0,0,6.5,1,5.31,5.31,0,0,0,8.1,4.9,5.31,5.31,0,0,0,12,6.5,5.46,5.46,0,0,0,6.5,12Z"/>
  </svg>
    </button>
    <script>
      (() => {
      const buttonEl =
        document.querySelector('#id_29830098-b25a-488e-b5a7-95e310e0a96a button.colab-df-generate');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      buttonEl.onclick = () => {
        google.colab.notebook.generateWithVariable('df_top_customers');
      }
      })();
    </script>
  </div>

    </div>
  </div>
```
:::
:::

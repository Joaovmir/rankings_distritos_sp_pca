# Rankings dos Distritos de São Paulo com PCA 🏙️📊

[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)

Este repositório apresenta uma análise dos distritos da cidade de São Paulo utilizando **Análise de Componentes Principais (PCA)**, com o objetivo de criar **rankings multicritério** baseados em indicadores sociais, econômicos, demográficos e urbanos. O projeto também explora visualizações e clusters dos distritos, facilitando a interpretação e a tomada de decisão para políticas públicas, estudos e investimentos.

---

## 🌟 Motivação

A cidade de São Paulo é composta por dezenas de distritos com realidades diversas. Políticas públicas, investimentos e projetos sociais exigem uma visão integrada e comparativa desses territórios. Utilizar técnicas estatísticas como PCA permite:

- **Resumir informações complexas** (vários indicadores) em poucos fatores compreensíveis.
- **Identificar padrões e agrupamentos** de distritos semelhantes.
- **Ranquear os distritos** conforme os principais componentes, proporcionando uma análise objetiva e visual dos dados.

---

## 🎯 Objetivos do Projeto

- Aplicar **PCA** para redução de dimensionalidade em dados de distritos de SP.
- Criar um **ranking dos distritos** com base nos componentes principais.
- Explorar **clusters** de distritos com características semelhantes.
- Gerar **visualizações** para apoiar a análise e comunicação dos resultados.
- Disponibilizar um **notebook interativo** para replicação ou adaptação da análise.

---

## 🗂️ Etapas do Projeto

1. **Coleta e pré-processamento** dos dados dos distritos (arquivo `distritos_sp.csv`)
2. **Análise exploratória** e limpeza dos dados (verificação de valores faltantes, padronização)
3. **Aplicação do PCA** para extrair os principais componentes
4. **Rankeamento** dos distritos com base nos scores dos componentes principais
5. **Visualização dos distritos** no espaço dos componentes e identificação de clusters (opcional: uso de K-means)
6. **Interpretação dos componentes**: quais indicadores mais pesam em cada componente?
7. **Discussão dos resultados** e sugestões de uso para políticas públicas ou estudos acadêmicos

---

## 📚 Tecnologias Utilizadas

- [Python 3.8+](https://www.python.org/)
- [Pandas](https://pandas.pydata.org/)
- [NumPy](https://numpy.org/)
- [Scikit-learn](https://scikit-learn.org/)
- [Matplotlib](https://matplotlib.org/)
- [Seaborn](https://seaborn.pydata.org/)

---

## ⚡ Como Rodar o Projeto

### 1. Clone o repositório

```bash
git clone https://github.com/Joaovmir/rankings_distritos_sp_pca.git
cd rankings_distritos_sp_pca
````

### 2. Instale as dependências

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
```

### 3. Estrutura dos Dados

A pasta `dados/` deve conter:

* `distritos_sp.csv`
  Base de dados dos distritos, com indicadores quantitativos (ex: população, renda média, índice de violência, acesso a serviços, etc.)

### 4. Execute o notebook

Abra o arquivo `pca_rankings_distritos_sp.ipynb` em seu ambiente Jupyter, Colab ou VS Code.

---

## 💡 Exemplos de Análises e Resultados

### Leitura e Pré-processamento

```python
import pandas as pd

distritos = pd.read_csv('dados/distritos_sp.csv')
print(distritos.info())
print(distritos.describe())
```

### Aplicação do PCA e Ranking

```python
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA

# Seleção de colunas numéricas e padronização
indicadores = distritos.select_dtypes(include='number')
scaler = StandardScaler()
dados_norm = scaler.fit_transform(indicadores)

# PCA
pca = PCA(n_components=2)
componentes = pca.fit_transform(dados_norm)

# Ranking (componente principal 1)
distritos['Ranking_PCA1'] = componentes[:, 0]
distritos.sort_values('Ranking_PCA1', ascending=False, inplace=True)
print(distritos[['Nome_Distrito', 'Ranking_PCA1']].head())
```

### Visualização dos Distritos nos Componentes

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(10,6))
plt.scatter(componentes[:, 0], componentes[:, 1])
for i, nome in enumerate(distritos['Nome_Distrito']):
    plt.annotate(nome, (componentes[i, 0], componentes[i, 1]), fontsize=8)
plt.xlabel('Componente Principal 1')
plt.ylabel('Componente Principal 2')
plt.title('Distritos de SP no Espaço dos Componentes Principais')
plt.grid(True)
plt.show()
```

---

## 📁 Estrutura do Projeto

```
rankings_distritos_sp_pca/
├── pca_rankings_distritos_sp.ipynb
├── dados/
│   └── distritos_sp.csv
├── README.md
```


> **Obs:** Este projeto pode ser expandido com mais indicadores, comparação entre diferentes anos ou aplicação a outros municípios.


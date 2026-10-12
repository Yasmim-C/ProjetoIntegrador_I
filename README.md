# Projeto Integrador — Ciência de Dados aplicada ao Agronegócio

Projeto acadêmico desenvolvido na **Faculdade de Tecnologia de Catanduva — FATEC**, no **Curso Superior de Tecnologia em Ciências de Dados para o Agronegócio**, na disciplina **Projeto Integrador**.

O repositório reúne as análises em Python que apoiam o desenvolvimento do projeto e do artigo acadêmico. O trabalho atual explora dados de cana-de-açúcar, com foco no ATR (Açúcar Total Recuperável), representado pela variável `atr_kg_ton`.

## Integrantes do projeto e do artigo

- Beatriz dos Santos Lio
- Bruno Bentivoglio Cezare
- Camilla Nogueira Faria Piovani
- Élio Rossi Neto
- Leonardo Almeida Santos Brito
- Yasmim Freitas de Camargo

**Professora orientadora:** Profª Dra. Fernanda Pereira Guidotti Carneiro.

## Objetivo

Explorar dados agrícolas e preparar uma base para o estudo e a previsão do ATR da cana-de-açúcar, considerando características da soqueira, variedade, textura do solo, número de corte e safra. As análises buscam apoiar a compreensão das relações entre essas variáveis e o indicador de qualidade da matéria-prima.

## Desenvolvimento atual

O notebook [Interdisciplinar_CYBEL.ipynb](notebooks/Interdisciplinar_CYBEL.ipynb) contém:

- Importação de um arquivo CSV pelo Google Colab.
- Inspeção da estrutura, dos tipos de dados, dos valores ausentes e dos registros duplicados.
- Estatísticas descritivas e levantamento de talhões e área cadastrada.
- Seleção das variáveis de entrada e do ATR como variável alvo.
- Preparação de conjuntos de treino e teste com separação por safra.
- Conversão de variedade e textura do solo em códigos numéricos.
- Cálculos iniciais de médias de vigor da soqueira e ATR.

O projeto está em desenvolvimento. O notebook ainda não apresenta um modelo preditivo treinado nem métricas de avaliação. As pastas de dados e resultados estão reservadas para as próximas etapas; a base CSV precisa ser fornecida para executar a análise.

## Tecnologias

| Tecnologia | Finalidade |
| --- | --- |
| Python | Desenvolvimento das análises e processamento dos dados. |
| Pandas | Importação, organização e análise de dados tabulares; utilizado no notebook atual. |
| NumPy | Operações numéricas; incluído nas dependências. |
| Matplotlib | Construção de gráficos; incluído nas dependências. |
| OpenPyXL | Suporte a arquivos Excel; incluído nas dependências. |
| Google Colab / notebooks Jupyter | Organização e execução dos códigos em células. O notebook atual utiliza recursos do Colab. |
| Streamlit | Possível interface para apresentação das análises; incluído nas dependências, com uso ainda em definição. |

As dependências e suas versões estão registradas em [requirements.txt](requirements.txt).

## Estrutura do projeto

```text
ProjetoIntegrador_I/
├── dados brutos/                       # Dados de origem
├── dados tratados/                     # Dados após tratamento
├── img/                                # Imagens da documentação
├── notebooks/
│   └── Interdisciplinar_CYBEL.ipynb      # Análise e preparação dos dados
├── resultados/                         # Resultados finais das análises
├── LICENSE                             # Licença MIT
├── README.md                           # Documentação do projeto
└── requirements.txt                    # Dependências Python
```

## Configuração do ambiente local

Abra o PowerShell na pasta do projeto e crie o ambiente virtual:

```powershell
py -m venv .venv
```

Ative o ambiente:

```powershell
.\.venv\Scripts\Activate.ps1
```

Caso o PowerShell bloqueie a ativação, ajuste a política apenas para a sessão atual e tente novamente:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
.\.venv\Scripts\Activate.ps1
```

Com o ambiente ativo, o terminal exibirá `(.venv)`:

![Exemplo do ambiente virtual ativo](img/venv_.png)

Instale as dependências:

```powershell
python -m pip install -r requirements.txt
```

Para encerrar o ambiente virtual:

```powershell
deactivate
```

## Execução do notebook

1. Abra o Google Colab e importe `notebooks/Interdisciplinar_CYBEL.ipynb`.
2. Execute a primeira célula e selecione a base CSV quando solicitado.
3. Execute as demais células na ordem em que aparecem.

A leitura atual utiliza separador `,`, decimal `,` e codificação `utf-8-sig`. A base deve conter as colunas utilizadas nas análises, incluindo `talhao`, `area_ha`, `falhas_soqueira_pct`, `vigor_soqueira_pct`, `variedade`, `textura_solo`, `numero_corte`, `safra` e `atr_kg_ton`.

Para executar localmente, será necessário configurar um ambiente de notebooks e adaptar a primeira célula: `google.colab.files.upload()` é específico do Colab e deve ser substituído pela leitura de um arquivo local com `pandas.read_csv()`.

## Licença

O código deste repositório está disponibilizado sob a [licença MIT](LICENSE).

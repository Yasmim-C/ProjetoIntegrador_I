# Tema Projeto

# Objetivo
-------------------------------------------------------------------------------
# Tecnologias Utilizadas

```powershell
* PYTHON # Lingaguem utilizada no desenvolvimento do projeto
* PANDAS # Para carregar, organizar, limpar e analisar dados em tabelas
* NUMPY # Realizar cálculos numéricos e operações com vetores e matrizez
* MATPLOTLIB # Criação e personalização de gráficos
* STREAMLIT(Ainda decidindo) # Cria aplicações Web e dashboards com o Pyhton
* Seaborn  # Para criar gráficos estatísticos
* Jupyter Notebook # Organizar e executar os códigos em células, combinando textos, gráficos e análises.
```
-------------------------------------------------------------------------------
# Estrutura do Projeto

```powershell
Projeto Integrador/
│
├── /dados brutos    # Vão ficar os dados brutos do projeto                  
├── /dados tratados  # Dados já feito o processo de ETL
├── /notebooks       # Onde serão realizadas as análises e insights com os dados
├──/resultados       # Onde irão ficar os resultados finais do projeto
├── README.md        # Documentação 
└── requirements.txt # Dependências do projeto
```

# Configurando o ambiente de execução
-------------------------------------------------------------------------------
Para criar o ambiente de execução execute o comando abaixo, e será criada uma pasta ".venv" no projeto.

```powershell
py -m venv .venv
```

No Windows, caso o PowerShell bloqueie a ativação do ambiente virtual, execute os comandos abaixo, na ordem indicada, para ajustar temporariamente a política de execução e ativar o ambiente:

```powershell
(Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned) ; (& c:"Caminho de onde esta seu projeto\.venv\Scripts\Activate.ps1)
```

Após a execução do comando deverá ficar com esse (.venv):

![Como fica com o ambiente em execução](img/venv_.png)

A configuração do ambiente está feita.

-------------------------------------------------------------------------------
## Instalar as bibliotecas que serão utilizadas.

Utilize o comando abaixo para instalar todas as bibliotecas necessárias, sem precisar instalar uma a uma.
```poweshell
python - m pip install -r  requirements.txt
```

Caso alguma nova biblioteca seja necessária, realize a instalação dela atráves do "pip install" e para adicionar ela aos requirements, execute esse comando

```powershell
pip freeze > requirements.txt
```

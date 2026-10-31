# Projeto Integrador I — Solo, soqueira e ATR da cana-de-açúcar

Repositório do artigo “Análise da influência das características do solo e da saúde da soqueira no ATR da cana-de-açúcar”, desenvolvido em 2026 no Curso Superior de Tecnologia em Ciência de Dados para o Agronegócio da FATEC Catanduva.

## Objetivo e escopo

Analisar a influência dos atributos do solo e da saúde da soqueira no ATR (Açúcar Total Recuperável, em kg/t de cana) e avaliar sua estimativa antes da colheita, apoiando o planejamento da produção e da receita do produtor.

O artigo propõe uma pesquisa aplicada e quantitativa, exploratória, descritiva e preditiva, em estudo de caso em Marapoama-SP, região de Catanduva, com dados fornecidos pela Associação dos Fornecedores de Cana da Região de Catanduva (AFCRC). A unidade analítica prevista é uma linha por talhão e safra.

## Metodologia prevista

O estudo adota o CRISP-DM para organizar entendimento do negócio e dos dados, preparação, modelagem, avaliação e implantação, conforme o avanço do projeto.

- **Dados:** laudos de solo, registros de soqueira e manejo e boletins de ATR; precipitação como variável complementar, se disponível.
- **Preparação:** limpeza, padronização de unidades e identificação dos talhões, análise de ausências e inconsistências e integração por talhão e safra.
- **Análise e modelo:** estatística descritiva, correlações de Pearson/Spearman e regressão linear simples para estimar o ATR a partir de uma única variável explicativa, ainda a definir. Os demais atributos podem ser explorados sem integrar simultaneamente esse modelo.
- **Avaliação:** treino/teste na proporção 80/20 proposta no artigo e métricas R², MAE e RMSE. A divisão em treino/teste e as métricas MAE e RMSE ainda precisam ser implementadas, com uma estratégia de separação que considere a ordem temporal dos dados. O R² atual é calculado na própria amostra de ajuste.

## Estado atual e dados

O [notebook](notebooks/CYBEL.ipynb) contém células de texto que contextualizam cada etapa e implementa:

- Leitura e conferência dos CSVs, incluindo dimensões, colunas e valores ausentes.
- Preparação das tabelas anuais: médias do solo por propriedade, talhão e ano, seguidas de médias anuais; somas e médias ponderadas pela tonelagem para os indicadores da cana.
- Correlações de Pearson calculadas com laços, gráficos de barras e matriz de correlação.
- Conferência descritiva do Brix e de sua correlação com o ATR na tabela original de cana, sem a agregação anual.
- Gráficos de dispersão do ATR em relação à acidez potencial, ao fósforo, ao potássio e ao pH do solo, com identificação dos pontos pelo ano.
- Cinco ajustes de regressão linear simples, um para cada atributo: pH do solo, acidez potencial, fósforo, potássio e argila. O NumPy ajusta as retas por mínimos quadrados (`np.polyfit`), e cada gráfico apresenta a tendência, o R² e o número de observações; a equação é impressa na saída.

Já há regressões ajustadas, mas ainda não há avaliação em dados de teste. O R² apresentado descreve o ajuste nos mesmos dados utilizados para calcular a reta. Não há divisão em treino/teste, cálculo de MAE/RMSE ou correlação de Spearman implementados. Cada regressão utiliza apenas um atributo; não há modelo com todos os atributos simultaneamente.

A integração atual é por ano civil, extraído das datas de solo e do fim do período da cana, e difere da unidade por talhão e safra prevista no artigo. Embora alguns rótulos dos gráficos usem “safras”, os pontos representam anos civis.

As fontes disponíveis ainda não formam a base por talhão e safra exigida: faltam registros de soqueira/manejo e ATR correspondente por talhão. O ATR agregado não deve ser repetido em cada amostra de solo para criar exemplos de treinamento.

Os dados originais ficam locais, fora do versionamento. A base fictícia também não é distribuída no repositório. Antes da integração, será necessário harmonizar nomes e unidades: o artigo denomina o alvo `atr`, enquanto o notebook atual usa `ATR`.

```text
dados brutos/     # Fontes originais locais, excluídas do Git
dados tratados/   # CSVs de solo e cana utilizados pelo notebook
notebooks/       # Notebook com contextualização, código e saídas
img/             # Imagens da documentação
resultados/      # Resultados locais, excluídos do Git
```

## Resultados exploratórios

Os gráficos abaixo foram gerados pelo notebook com as bases locais. O pareamento anual abrange 2020 a 2025, com seis observações; as variáveis de textura têm somente três anos válidos. As correlações não demonstram causalidade nem desempenho de um modelo preditivo.

Atributos do solo e ATR. As barras apresentam a correlação de Pearson e o número de anos válidos (`n`) para cada atributo.

![Correlação dos atributos do solo com o ATR](img/correlacao_solo_atr.png)

Indicadores da cana e ATR. PC, Pol e Brix apresentam associações positivas elevadas nesta amostra. São indicadores ligados à qualidade e ao cálculo do ATR; essas associações não comprovam previsão antes da colheita.

![Correlação dos indicadores da cana com o ATR](img/correlacao_cana_atr.png)

Matriz de correlação. Resume as associações entre as variáveis selecionadas, permitindo observar também relações entre possíveis entradas do modelo. Cada par utiliza os anos com valores disponíveis.

![Matriz de correlação de Pearson](img/matriz_correlacao_pearson.png)

Dispersões e regressões. As novas visualizações estão nas saídas do [notebook](notebooks/CYBEL.ipynb). Os gráficos de dispersão mostram os pares anuais disponíveis e a correlação de Pearson. Os gráficos de regressão acrescentam a reta ajustada, sua equação e o R² na própria amostra. O ajuste exige pelo menos três observações; a regressão com argila utiliza somente os três anos com dados de textura. Esses resultados ainda não validam uma estimativa de ATR em anos futuros.

Os resumos são unidos apenas pelo ano, sem validar correspondência entre propriedades. Portanto, estes resultados são preliminares e precisam dessa conferência antes de interpretações agronômicas.

## Resultados e discussão

O pareamento dos dados de solo e de cana resultou em seis observações anuais, de 2020 a 2025. O ano de 2026 ficou fora dessa comparação por não haver registros de solo correspondentes. A unidade efetivamente analisada foi o ano civil, e não uma safra delimitada por calendário agrícola. A média aritmética dos seis valores anuais de ATR foi de 134,32 kg/t de cana, atribuindo o mesmo peso a cada ano. O ATR aumentou de 138,4 kg/t em 2020 para 143,7 kg/t em 2022, seguido de reduções sucessivas até atingir 122,7 kg/t em 2025.

Entre os cinco atributos selecionados para as regressões simples, o pH do solo apresentou forte associação linear negativa com o ATR (r = −0,906). A reta ajustada teve inclinação de −26,10, correspondendo a uma diferença estimada de −26,10 kg/t de ATR para cada unidade adicional de pH, dentro do intervalo observado. A acidez potencial apresentou forte associação positiva (r = 0,868), com inclinação de 2,24 kg/t de ATR por unidade do atributo registrada na base. Essas relações descrevem a variação conjunta das médias anuais e não demonstram que alterações no pH ou na acidez tenham causado mudanças no ATR. Tampouco fundamentam recomendações de manejo para aumentar a acidez ou reduzir o pH.

As associações do fósforo (r = −0,098) e do potássio (r = −0,278) com o ATR foram fracas na amostra analisada. Suas regressões apresentaram inclinações de −0,19 e −2,95 kg/t de ATR por unidade do respectivo atributo. A magnitude dessas inclinações depende das unidades e escalas das variáveis e, por isso, não permite comparar diretamente sua importância. Para a argila, a correlação foi positiva (r = 0,599), com inclinação de 0,06 kg/t por unidade registrada na base. Esse ajuste utilizou **apenas três observações anuais**, o que restringe sua interpretação e reforça a necessidade de conferir os registros de textura antes de conclusões agronômicas.

Os indicadores da cana Pol (r = 0,997), PC (r = 0,998) e Brix (r = 0,982) apresentaram correlações positivas elevadas com o ATR na tabela anual pareada. Como estão relacionados à qualidade tecnológica da cana e ao cálculo do ATR, essas associações não constituem evidências independentes de capacidade preditiva antes da colheita. A disponibilidade desses indicadores no momento em que se pretende estimar o ATR também precisa ser considerada em uma futura modelagem.

Os gráficos de dispersão permitiram identificar os anos e examinar visualmente a direção das associações. As retas de regressão sintetizaram essas tendências, mas foram ajustadas com somente seis pontos — ou três, no caso da argila — e podem ser fortemente influenciadas por observações individuais. O R² foi calculado nos mesmos dados utilizados para ajustar cada reta; portanto, descreve o ajuste na própria amostra e não representa desempenho em anos novos. Não foram realizados divisão em treino/teste, cálculo de MAE/RMSE ou testes de significância estatística.

A agregação anual também limita a interpretação: as médias não representam a variabilidade entre talhões, e a associação observada entre anos não pode ser automaticamente atribuída a cada talhão. Além disso, o pareamento foi realizado somente pelo ano, sem validação automática da correspondência entre propriedades. Informações de manejo, clima e saúde da soqueira não foram incorporadas a esses ajustes, de modo que sua participação nas variações do ATR permanece sem avaliação.

## Conclusões

A análise identificou associações entre o ATR e atributos médios anuais do solo no período de 2020 a 2025. Entre os cinco atributos escolhidos para regressão, pH e acidez potencial apresentaram as associações lineares mais fortes, com direções negativa e positiva, respectivamente. Fósforo e potássio apresentaram associações fracas, enquanto a análise de argila ficou limitada a três anos com dados disponíveis. Essa comparação se refere ao conjunto selecionado para regressão, e não a todos os atributos de solo explorados no notebook.

Os resultados contribuem para descrever os padrões observados na base estudada e formular novas hipóteses. Entretanto, o número reduzido de observações, a agregação anual e a ausência de avaliação em dados independentes impedem concluir que os atributos do solo causaram as variações do ATR ou que as regressões estejam validadas para previsão antes da colheita. A influência da saúde da soqueira, prevista no objetivo do projeto, permanece uma etapa a investigar quando houver dados adequados.

Para avançar, propõe-se conferir a consistência e as unidades dos registros de textura, validar a correspondência entre propriedades e, conforme a disponibilidade das fontes, integrar solo e cana por **talhão e safra**. A ampliação da série histórica e a inclusão de informações de manejo, clima e saúde da soqueira podem apoiar uma análise mais completa. Uma futura avaliação preditiva deverá respeitar a ordem temporal dos dados e utilizar observações independentes, evitando atribuir ao solo efeitos que a análise atual não permite distinguir.

## Execução no VS Code

Instale as extensões **Python** e **Jupyter**, abra a pasta do projeto e execute no terminal PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Abra `notebooks/CYBEL.ipynb` e selecione o kernel `.venv`. A primeira célula lê os CSVs da pasta `dados tratados`. O notebook espera arquivos identificados como `DADOS_SOLO`, `Cana.csv` e, opcionalmente, `ART.csv`, com as colunas utilizadas nas células seguintes.

Use **Run All / Executar Tudo** para executar todas as células em ordem, ou **Shift+Enter** para avançar uma célula por vez. Os CSVs utilizados estão disponíveis na pasta `dados tratados` do repositório; os arquivos de `dados brutos` permanecem locais.

**Dependências do ambiente:** `requirements.txt` contém as bibliotecas diretamente utilizadas e o kernel necessário para executar o notebook no VS Code:

| Ferramenta | Uso no projeto |
| --- | --- |
| Pandas | Leitura dos CSVs, preparação das tabelas, datas e conferências estatísticas. |
| NumPy | Ajuste das regressões lineares com `polyfit` e ordenação dos pontos com `argsort`. |
| Matplotlib | Gráficos de barras, matriz de correlação, dispersões e retas de regressão. |
| ipykernel | Execução do notebook no kernel Python do ambiente `.venv`. |

As versões registradas correspondem ao ambiente utilizado na execução atual. As dependências internas dessas bibliotecas são instaladas automaticamente pelo pip. `pathlib` e `io` fazem parte da biblioteca padrão do Python e não exigem instalação separada.

**Organização do trabalho:** Git/GitHub para versionamento, Trello para tarefas e Overleaf para redação do artigo.

## Equipe

Beatriz dos Santos Lio; Bruno Bentivoglio Cezare; Camilla Nogueira Faria Piovani; Élio Rossi Neto; Leonardo Almeida Santos Brito; Yasmim Freitas de Camargo.

**Orientadora:** Profª Dra. Fernanda Pereira Guidotti Carneiro.

Código sob [licença MIT](LICENSE).

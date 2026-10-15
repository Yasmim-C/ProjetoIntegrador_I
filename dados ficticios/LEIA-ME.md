# Base fictícia para demonstração

Os 26 CSVs desta pasta contêm dados sintéticos. Nomes de propriedades, identificadores, preços, análises de solo e produção foram gerados artificialmente e não representam resultados reais.

Os arquivos usam separador `;`, ponto decimal e codificação UTF-8 com BOM. A organização mantém três grupos: análises de solo por propriedade e ano, preços mensais de ATR e produção de cana.

São 413 registros de solo, 150 registros mensais de preços e 21 linhas de produção. As linhas de produção representam sete períodos apresentados em três níveis (`Fazenda`, `Total (Fornecedor)` e `Total (Geral)`); escolha apenas um nível antes de somar.

Esta base serve para demonstração e testes de processamento. Não comprova desempenho preditivo em dados reais e não contém todas as variáveis exigidas pelo modelo originalmente proposto no notebook. O ATR da produção está agregado por período, sem correspondência individual por talhão.

Os dados reais ficam na pasta local `dados brutos/`, excluída do versionamento pelo `.gitignore`.

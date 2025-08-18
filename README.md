# Challenge-Telecom-X

🔹 1. Introdução

Relatório tem como objetivo analisar os dados da empresa TelecomX após um processo de ETL (Extração, Transformação e Carga). O foco principal é entender os padrões de cancelamento de clientes (churn) e como variáveis contratuais, demográficas e de serviços influenciam esse comportamento.

🔹 2. Pipeline ETL

Os dados foram extraídos de um arquivo JSON fornecido pela empresa. Transformação Normalização de colunas aninhadas. Tradução e padronização de valores (Yes/No → Sim/Não). Conversão de variáveis numéricas (Meses_Permanencia, Cobranca_Mensal, Cobranca_Total). Criação da variável binária Cancelou (1 = cancelou, 0 = não cancelou). Carga Dados finais armazenados em .csv e .parquet para uso futuro.

<img width="580" height="455" alt="image" src="https://github.com/user-attachments/assets/f696546b-6604-4398-83fc-849fb2fe7776" />


Aproximadamente 26% dos clientes cancelaram e 74% permaneceram.


<img width="580" height="455" alt="image" src="https://github.com/user-attachments/assets/eb00e59b-ef74-43a0-a1c2-3f4e1fbe7190" />


Clientes com contrato Mês a mês apresentam muito mais cancelamentos.

Contratos de 1 ano ou 2 anos têm churn muito menor, sugerindo maior fidelização.


<img width="571" height="455" alt="image" src="https://github.com/user-attachments/assets/f3e7ee10-6603-42a7-8b8f-c65e14a166a2" />


Clientes que pagam menos por mês cancelam com maior frequência.

Sugere que usuários de planos básicos estão menos satisfeitos ou menos engajados.


<img width="1389" height="1989" alt="image" src="https://github.com/user-attachments/assets/50c82f85-9864-427a-92bc-16189cdd0952" />


Clientes sem serviços adicionais (backup, suporte, segurança) cancelam mais.

Quanto mais serviços extras contratados, menor a probabilidade de churn.


<img width="580" height="456" alt="image" src="https://github.com/user-attachments/assets/1917ea37-267b-40ec-a141-b56e1cfc8792" />


Muitos cancelamentos ocorrem nos primeiros meses de contrato.

Após longos períodos (acima de 2 anos), a taxa de churn cai bastante.


<img width="641" height="435" alt="image" src="https://github.com/user-attachments/assets/6dd9ee5b-4a22-42e6-87a4-d32652f3b041" />


Cobranca_Total tem forte correlação positiva com Meses_Permanencia.

Clientes que ficam mais tempo, naturalmente acumulam mais cobranças.

Resumo:

Quem cancelou ficou em média 1 ano ou menos.

Quem não cancelou costuma permanecer por mais tempo e gerar maior receita.

🔹 5. Conclusões e Recomendações

Planos Mês a Mês têm altíssima taxa de churn → incentivar upgrades para planos anuais.

Clientes com menos serviços contratados cancelam mais → oferecer pacotes de serviços extras pode aumentar retenção.

Primeiros meses críticos → importante criar campanhas de onboarding e suporte ao cliente logo no início.

Planos de baixo valor têm maior churn → sugerir planos de maior valor agregado com benefícios extras pode reduzir cancelamento.

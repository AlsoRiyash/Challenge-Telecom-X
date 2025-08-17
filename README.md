# Challenge-Telecom-X

🔹 1. Introdução

O presente relatório tem como objetivo analisar os dados da empresa TelecomX após um processo de ETL (Extração, Transformação e Carga). O foco principal é entender os padrões de cancelamento de clientes (churn) e como variáveis contratuais, demográficas e de serviços influenciam esse comportamento.

🔹 2. Pipeline ETL

Extração Os dados foram extraídos de um arquivo JSON fornecido pela empresa. Transformação Normalização de colunas aninhadas. Tradução e padronização de valores (Yes/No → Sim/Não). Conversão de variáveis numéricas (Meses_Permanencia, Cobranca_Mensal, Cobranca_Total). Criação da variável binária Cancelou (1 = cancelou, 0 = não cancelou). Carga Dados finais armazenados em .csv e .parquet para uso futuro.


[ ]
churn_counts = df["Cancelou"].value_counts()

sns.barplot(x=churn_counts.index, y=churn_counts.values, palette=["#66c2a5", "#fc8d62"])
plt.xticks([0,1], ["Não cancelou", "Cancelou"])
plt.ylabel("Quantidade de clientes")
plt.title("Distribuição de Cancelamento de Clientes")
plt.show()

(churn_counts / churn_counts.sum()).map("{:.1%}".format)

Aproximadamente 26% dos clientes cancelaram e 74% permaneceram.


[ ]
sns.countplot(data=df, x="Contrato", hue="Cancelou", palette="pastel")
plt.title("Churn por Tipo de Contrato")
plt.xlabel("Tipo de Contrato")
plt.ylabel("Clientes")
plt.legend(title="Cancelou", labels=["Não", "Sim"])
plt.show()

Clientes com contrato Mês a mês apresentam muito mais cancelamentos.

Contratos de 1 ano ou 2 anos têm churn muito menor, sugerindo maior fidelização.


[ ]
sns.boxplot(data=df, x="Cancelou", y="Cobranca_Mensal", palette=["#8da0cb", "#e78ac3"])
plt.xticks([0,1], ["Não cancelou", "Cancelou"])
plt.ylabel("Cobrança Mensal (R$)")
plt.title("Cobrança Mensal x Cancelamento")
plt.show()

Clientes que pagam menos por mês cancelam com maior frequência.

Sugere que usuários de planos básicos estão menos satisfeitos ou menos engajados.


[ ]
servicos = ["Fatura_Eletronica","Telefone","Internet",
            "Seguranca_Online","Backup_Online","Protecao_Dispositivo",
            "Suporte_Tecnico","Streaming_TV","Streaming_Filmes"]

fig, axes = plt.subplots(5, 2, figsize=(14,20))
axes = axes.flatten()

for i, serv in enumerate(servicos):
    sns.countplot(data=df, x=serv, hue="Cancelou", ax=axes[i], palette="Set2")
    axes[i].set_title(f"Churn x {serv}")
    axes[i].legend(title="Cancelou", labels=["Não","Sim"])

plt.tight_layout()
plt.show()

Clientes sem serviços adicionais (backup, suporte, segurança) cancelam mais.

Quanto mais serviços extras contratados, menor a probabilidade de churn.


[ ]
sns.histplot(data=df, x="Meses_Permanencia", hue="Cancelou", multiple="stack", bins=30, palette="coolwarm")
plt.title("Tempo de Permanência x Cancelamento")
plt.xlabel("Meses de permanência")
plt.ylabel("Clientes")
plt.show()

Muitos cancelamentos ocorrem nos primeiros meses de contrato.

Após longos períodos (acima de 2 anos), a taxa de churn cai bastante.


[ ]
num_cols = ["Meses_Permanencia", "Cobranca_Mensal", "Cobranca_Total"]
corr = df[num_cols].corr()

sns.heatmap(corr, annot=True, cmap="coolwarm")
plt.title("Matriz de Correlação")
plt.show()

Cobranca_Total tem forte correlação positiva com Meses_Permanencia.

Clientes que ficam mais tempo, naturalmente acumulam mais cobranças.


[ ]
df.groupby("Cancelou")[["Meses_Permanencia","Cobranca_Mensal","Cobranca_Total"]].median()

Resumo:

Quem cancelou ficou em média 1 ano ou menos.

Quem não cancelou costuma permanecer por mais tempo e gerar maior receita.

🔹 5. Conclusões e Recomendações

Planos Mês a Mês têm altíssima taxa de churn → incentivar upgrades para planos anuais.

Clientes com menos serviços contratados cancelam mais → oferecer pacotes de serviços extras pode aumentar retenção.

Primeiros meses críticos → importante criar campanhas de onboarding e suporte ao cliente logo no início.

Planos de baixo valor têm maior churn → sugerir planos de maior valor agregado com benefícios extras pode reduzir cancelamento.

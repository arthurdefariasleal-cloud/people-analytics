# people-analytics
Como transformar dados de perfil e comportamento em decisões melhores de contratação e retenção

# Estrutura do Projeto

```bash
people-analytics-performance/
│
├── data/
│   └── raw/
│       └── base_original.xlsx
│
├── analysis/
│   └── analises.xlsx
│
└── assets/images/
    ├── grafico1.png
    ├── grafico2.png
    ├── grafico3.png
    ├── grafico4.png
    ├── grafico5.png
    ├── grafico6.png
    ├── grafico7.png
    └── grafico8.png
```
    
# Entendimento do Negócio
## Objetivo
A empresa de Contact Center está passando por um desafio: a alta rotatividade motivada por baixo desempenho dos seus colaboradores nos primeiros meses pós-contratação. Isto acaba promovendo um ciclo contínuo de novas contratações e, por consequência, novos custos com treinamentos e reposições. 

O objetivo deste projeto é criar um modelo para identificar, ainda no processo seletivo, quais perfis têm maior chance de apresentar boa performance após 6 meses de contratação.

## Problema de Negócio
Atualmente, o processo seletivo da empresa estar:
* Priorizando volume em vez de qualidade
* Baseado em critérios subjetivos
* Sem uso estruturado de dados históricos

Isso faz com que parte significativa das contratações resulte em baixa performance após 6 meses. Conseguindo aumentar a taxa de boa performance, mesmo que em poucos pontos percentuais, o impacto financeiro e operacional pode ser significativo para a empresa.

## Premissas Adotadas
1. A performance considerada é a registrada após 6 meses da contratação.
2. Correlação estatística pode ser utilizada como instrumento de apoio à decisão (sem assumir causalidade automática).
3. A variáveis que ferem a ética e a LGPD serão desconsideradas.
4. A Política de Contratação da empresa não sofrerá nenhuma mudança significativa durante o projeto.

## Hipóteses de Negócio
Antes da análise, levantei hipóteses com base na lógica:

Fato (Medida): Turnover por performance  
Dimensão (Atributos do colaborador)

**Escolaridade**

1. O turnover por performance é maior entre colaboradores com menor nível de escolaridade.
2. Escolaridade é o principal preditor de boa performance.

**Experiência prévia em Contact Center**

3. Colaboradores sem experiência prévia são mais suscetíveis a turnover por performance.

**Nível de Inglês**

4. Turnover é maior entre colaboradores com inglês básico ou intermediário.

**Área de atuação anterior**

5. A área onde o colaborador atuou por mais tempo influencia sua performance.

**Perfil comportalmental (Sinceridade)**

6. Sinceridade não é fator preditivo de boa performance.

**Nível de tensão no trabalho**

7. Colaboradores que relatam alta tensão apresentam maior turnover por performance.

**Tempo de deslocamento casa-empresa**

8. Tempo de trajeto impacta diretamente a performance.


# Entendimento dos Dados
## Descrição da Base
A base contém 7.240 colaboradores, contratados ao longo de diferentes períodos, com informações disponíveis no momento da contratação e o resultado de performance após 6 meses.

<img width="1225" height="292" alt="image" src="https://github.com/user-attachments/assets/f32acca4-ebf8-4d64-b303-269f498d77f6" />

## Análise Exploratória (EDA)
O objetivo desta etapa é observar padrões nas variáveis e garantir que a base esteja apta para a etapa de modelagem.
<br><br>

<img width="1654" height="634" alt="image" src="https://github.com/user-attachments/assets/4ca588e9-5711-49c4-8bee-5bca5359fa82" />
<br><br>

Insights:
* A taxa de baixa performance (44%) indica ineficiência na Política de Contratação atual.
* A empresa contrata grande volume de perfis com menor qualificação formal.
* O quadro apresenta uma alta proporção de colaboradores sem experiência.
* A variável de tempo de deslocamento não está sendo bem capturada.

# Preparação dos Dados
## Seleção das Variáveis
Por se tratar de um conjunto com poucas variáveis, optei por manter praticamente todas elas na minha análise, com exceção da variável “P06: Você possui dependentes?”. 

Essa remoção foi baseada em dois critérios:  
1. Etica e privacidade;
2. Baixa relevância para o objetivo de negócio.

## Limpeza e Formatação dos Dados
Após a análise exploratória e a seleção das variáveis, realizei a etapa de limpeza da base. 

**Tratamento de valores ausentes**  
A categoria “Sem resposta” foi mantida nas análises para medir a proporção de não respondentes e avaliar impacto estatístico dessa ausência de informação.

**Limpeza e consistência da base**  
Foram removidos espaços à esquerda em todas as variáveis, além de verificada a existência de duplicatas e caracteres inconsistentes.

**Padronização da variável P01 (Experiência Prévia)**  
A categoria “A empresa é o meu primeiro emprego” foi reclassificada como “Não”, pois analiticamente se equivalem.

# Modelo / Insights
O objetivo desta etapa é identificar quais variáveis possuem maior poder explicativo sobre o risco de turnover e quantificar a probabilidade de ocorrência.

## Escolha da Técnica Estatística
Para medir o quanto cada variável contribui para a boa performance, utilizei duas técnicas estatísticas: **Information Value (IV)** e o **Teste-Z de duas populações**.

A primeira foi utilizada como ponto de partida para medir o grau de influência de cada variável no contexto do negócio, e a segunda para validar estatisticamente se as diferenças entre as categorias são relevantes.

Referência de interpretação:

<div align="center">
  <img src="https://github.com/user-attachments/assets/718221d3-20dc-4f31-974d-1fa7afa35973" width="400">
</div>

## Aplicação de IV
Para iniciar o modelo, apliquei IV em cada variável selecionada, medidndo o quanto cada uma delas contribui para a previsão de boa performance. Resultados abaixo:

<br>
<div align="center">
<img width="801" height="292" alt="image" src="https://github.com/user-attachments/assets/02ce3a14-dc2e-4322-b8ad-9b1f346568b5" />
</div>

<br><br>
Os resultados mostram que todas as variáveis são interpretadas como “Fracas” ou “Irrelevantes”.

Desta forma, decidi desconsiderar as variáveis “Irrelevantes” e aprofundar a análise nas variáveis “Fracas” que, apesar de fracas, ainda apresentam algum grau de relevância para a predição.

Essas variáveis, quando combinadas, apresentam maior relevância do que quando consideradas individualmente.

### 1. P01: Experiência em Contact Center

<img width="1338" height="170" alt="image" src="https://github.com/user-attachments/assets/3dd6ef62-fef1-47e0-a151-f92b669141c8" />

**Insights:**  
* Candidatos inexperientes apresentam uma taxa de boa performance ligeiramente acima dos experientes (60% x 53%).
* Possível explicação: quem nunca trabalhou na área chega mais aberto à treinamentos e à cultura da empresa.
* Experiência prévia não garante melhor desempenho e não deve ser critério eliminatório no processo seletivo.

### 2. P02: Atuação Anterior (somente candidatos com experiência prévia)

<img width="1337" height="355" alt="image" src="https://github.com/user-attachments/assets/026e15c9-ee26-485b-929e-01d9d1ae7203" />

**Insights:**  
* Mais da metade dos candidatos experientes vem de apenas dois setores (Atendimento Recepctivo - 41% e Backoffice - 13%).
* Quase todos os setor apresentam desempenho parecido (entre 48-60%).
* Alguns setores apresentam taxa de boa performance bem acima ou bem abaixo da média, mas com amostras pouco representativas. Suporte Técnico, por exemplo, tem 73% de taxa de boa performance, porém representa uma amostra de apenas 26 colaboradores (1% do total). Já o setor de Retenção, com 39% de taxa de boa performance, representa apenas 3% do total.
* Backoffice (60%) merece mais atenção na hora do recrutamento.
* Suporte Técnico pode ser um perfil de risco com apenas 48% e uma amostra minimamente representativa.

### 3. P07: “É bom trabalho com meus colegas de trabalho"

<img width="1339" height="244" alt="image" src="https://github.com/user-attachments/assets/20ce279f-a6bf-4843-9148-8d9d42ddd064" />

**Insights:**  
* Colaboradores que discordam que é bom trabalhar com os colegas (níveis 1 e 2) apresentam as menores taxas de boa performance (36% e 46%), bem abaixo da média geral (56%).
* Os que concordam totalmente (nível 5) apresentam 59% de boa performance, acima da média e com a maior representatividade da base (46%).
* Os resultados apresentam um padrão comportamental consistente.

## Aplicação do Teste-Z de 2 populações
Como os resultados da aplicação de IV indicaram baixo poder de influência, decidi aplicar o Teste Z de 2 populações para validar com mais rigor se as diferenças de boas performances observadas entre os grupos são realmente relevantes.

**1. P01: Experiência em Contact Center**  

<img width="666" height="504" alt="image" src="https://github.com/user-attachments/assets/33e763fb-b3ca-40e4-af92-16d740866f44" />

Como p-valor = 0% é menor que o nível de significância de 5%, concluo que existem evidências estatísticas suficientes para rejeitar H0. 

Desta forma, considero H1: **A proporção de Boa Performe de colaboradores experientes é menor do que a de inexperientes**.

**2. P07: “É bom trabalho com meus colegas de trabalho”**  
Para essa variável, as respostas foram unificadas em “Concordo” (4+5) e “Discordo” (1+2), desconsiderando as categorias “Sem resposta” e “Indiferente” da análise.

<img width="669" height="503" alt="image" src="https://github.com/user-attachments/assets/3bcce4a5-292c-45b9-a4f3-70eb4550d9e2" />

De forma semelhante, com p-valor = 0,2% é menor que 5%, posso rejeitar H0 e considerar H1: **A proporção de Boa Performance de colaboradores que discordam é menor do que a dos que concordam**.

**Conclusão:**  
Os resultados obtidos a partir do Teste-Z mostram que há evidências estatísticas para considerar que as diferenças entre as categorias de ambas as variáveis, em relação a taxa de Boa Performance, são relevantes. 

Portanto, mesmo com IVs fracos, podemos afirmar que elas contribuem na performance do colaborador após 6 meses de contratação.

## Verificação das Hipóteses de Negócio

**1. O turnover por performance de colaboradores com menor nível de escolaridade é maior do que entre colaboradores com maior nível de escolaridade.**  
Hipótese estatisticamente fraca. Menor escolaridade apresenta menor taxa de boa performance (54 x 62-64%), mas o IV é muito baixo (0,015)

**2. Nível de escolaridade é o maior preditor de boa performance de um candidato.**  
Hipótese refutada. Escolaridade não é o maior preditor e possui baixo poder explicativo (IV = 0,015)

**3. Candidatos que não possuem nenhuma experiência prévia em Contact Center estão mais suscetíveis à turnover por performance do que os que possuem.**  
Hipótese refutada. Candidatos sem experiência performam melhor (60x53%)

**4. O turnover por performance de colaboradores com nível básico ou intermediário de inglês é maior do que entre colaboradores com nível avançado ou fluente.**  
Hipótese estatisticamente fraca. Há leve melhora com o aumento do nível de inglês, mas IV é irrelevante (0,005)

**5. A área de atendimento em que o candidato atuou por mais tempo tem forte poder de influência na sua performance.**  
Hipótese refutada. "Atuação Anterior" tem IV = 0,030, indicando influência fraca na performance.

**6. A sinceridade do candidato que diz o que pensa não é um fator preditivo para prever boa performance.**  
Hipótese confirmada. “Sinceridade” apresenta IV = 0,008 e taxas muito próximas da média (56%), logo não é fator preditivo relevante.

**7. O turnover por performance de colaboradores que relatam trabalhar sob alta tensão é maior do que entre os que relatam menor nível de tensão.**  
Hipótese refutada. Quem relata alta tensão não apresenta maior baixa performance (48–56% boa performance) e IV = 0,003.

**8. O tempo gasto pelo colaborador no trajeto da sua residência para a empresa impacta diretamente na sua performance.**  
Estatisticamente fraca. Há leve piora acima de 2h (45%), mas IV = 0,012 indica impacto muito baixo.

# Análises
Após aplicar as análises estatísticas, é possível apontar:

**1. Experiência prévia não garante melhor performance**  
Contrariando o senso comum, candidatos sem experiência em Contact Center apresentaram melhor performance (60% x 53%). 
Apesar do IV ser baixo, foi um dos maiores encontrados e o Teste Z confirmou diferença estatística. 
Isso sugere que perfis “crus” podem se adaptar melhor à cultura e aos treinamentos da empresa.

**2. Postura colaborativa tem relação com performance**  
Entre as variáveis comportamentais, “gostar de trabalhar com os colegas” foi a única com sinal relevante.
Quem concorda com essa afirmação teve 57% de boa performance, enquanto quem discorda apresentou 39%.
Postura colaborativa deve ser considerada no processo seletivo.

**3. Entre experientes, priorizar Backoffice**  
Candidatos vindos de Backoffice apresentaram 60% de boa performance, acima da média dos experientes (53%).
Esse perfil pode ser priorizado dentro do grupo com experiência prévia.

**4. Suporte Técnico com Vendas (atenção futura)**  
Apresentou alta performance (73%), porém com amostra muito pequena (1%).
Não recomenda mudança imediata, apenas monitoramento no longo prazo.

**5. Retenção (atenção futura)**  
Mostrou baixa performance (39%), mas também com baixa representatividade (3%).
Requer acompanhamento antes de qualquer decisão prática.

# Política de Contratação Recomendada
**1. Não exigir experiência prévia como critério eliminatório.**  
Candidatos inexperientes na área não devem ser preteridos em nenhuma etapa do processo seletivo. Esta recomendação reduz um viés de pré-conceito.

**2. Candidatos com perfil colaborativo e de boa relação com os colegas devem ser priorizados.**  
Para isso, o RH deve-se adotar perguntas que aprofundem mais o tema. Por exemplo:
** Como você costuma lidar com colegas que pensam diferente de você?
** Conte sobre a sua melhor experiência de trabalho em grupo.
** Você costuma dividir problemas do dia-a-dia com os seus colegas de trabalho?
** Qual a sua postura perante um conflito entre seus colegas de trabalho?

**3. Priorizar o setor de Backoffice entre os candidatos com experiência prévia em Contact Center.**  
Mesmo que a experiência prévia do candidato em Contact Center não seja um critério eliminatório, quando um candidato a tiver, seu setor de atuação pode significar informações adicionais relevantes.

**4. Retirar do processo seletivo a pergunta sobre dependentes.**    
Além de não acrescentar valor preditivo no contexto do negócio, a pergunta também fere conceitos éticos, pois o candidato fornece informações pessoais que não têm relevância para as suas habilidades profissionais.

**5. Reavaliar perguntas sobre “Gostar de fazer as coisas do próprio jeito”, “Gostar de dizer o que pensa”, “Medo de criticar lideranças” e “Situações de autocontrole”.**  
A análise mostrou que essas perguntas são irrelevantes para prever performance. Contudo, é preciso avaliar se elas são importantes para avaliação de outros contextos. Neste caso, cabe ao RH reavaliar a necessidade de mantê-las ou não.




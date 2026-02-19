# people-analytics
Como transformar dados de perfil e comportamento em decisões melhores de contratação e retenção

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
Antes da análise, levantei hipóteses com base na lógica de **Fato (Medida) + Dimensão (Detalhes)**

**Fato + Dimensão: Colaborador - Atributo: Escolaridade**    
(1) O turnover por performance de colaboradores com menor nível de escolaridade é maior do que entre colaboradores com maior nível de escolaridade.  
(2) Nível de escolaridade é o maior preditivo de boa performance de um candidato.

**Fato + Dimensão: Colaborador - Atributo: Experiência prévia em Contact Center**  
(3) Candidatos que não possuem nenhuma experiência prévia em Contact Center estão mais suscetíveis à turnover por performance do que os que possuem.

**Fato + Dimensão: Colaborador - Atributo: Nível de Inglês**  
(4) O turnover por performance de colaboradores com nível básico ou intermediário de inglês é maior do que entre colaboradores com nível avançado ou fluente.

**Fato + Dimensão: Colaborador - Atributo: Área de atuação anterior**  
(5) A área de atendimento em que o candidato atuou por mais tempo tem forte poder de influência na sua performance.

**Fato + Dimensão: Colaborador - Atributo: Sinceridade (perfil comportamental)**  
(6) A sinceridade do candidato que diz o que pensa não é um fator preditivo para prever boa performance.

**Fato + Dimensão: Colaborador - Atributo: Nível de tensão no trabalho**  
(7) O turnover por performance de colaboradores que relatam trabalhar sob alta tensão é maior do que entre os que relatam menor nível de tensão.

**Fato + Dimensão: Colaborador - Atributo: Tempo de deslocamento**  
(8) O tempo gasto pelo colaborador no trajeto da sua residência para a empresa impacta diretamente na sua performance.

# Entendimento dos Dados
## Descrição da Base
A base contém 7.240 colaboradores, contratados ao longo de diferentes períodos, com informações disponíveis no momento da contratação e o resultado de performance após 6 meses.

<img width="1225" height="292" alt="image" src="https://github.com/user-attachments/assets/f32acca4-ebf8-4d64-b303-269f498d77f6" />

## Análise Exploratória (EDA)
Nesta etapa, o objetivo é entender como as variáveis se comportam, observar padrões e garantir que a base está apta para a etapa de modelagem.







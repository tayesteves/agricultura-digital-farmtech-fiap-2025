FIAP - Faculdade de Informática e Administração Paulista

## Fase 2 - Campo da inovação - Uma plantação de códigos
## Atividade Cap 1 - Um mapa do tesouro

## Integrantes 
  João, RM 565999
  Vinicius, RM 566269
  Endrew, RM 563646
  Tayná, RM 562491

## Sumário
- [Contexto](#contexto)
- [Objetivos do Projeto](#objetivos-do-projeto)
- [Entidades e Atributos](#entidades-e-atributos)
- [Relacionamentos dentro do sistema](#relacionamentos-dentro-do-sistema)
- [Geolocalização](#geolocalização)
- [Arquivos incluídos](#arquivos-incluídos)

## Agricultura Digital - FarmTech Solutions
Este repositório apresenta o projeto de modelagem de banco de dados relacional para um sistema de agricultura digital inteligente, desenvolvido como parte da disciplina de Banco de Dados da FIAP – 2025.

## Contexto
A FarmTech Solutions está investindo em tecnologia para transformar a forma como os produtores rurais cuidam de suas lavouras. Sensores são instalados nas plantações para monitorar dados como umidade, pH do solo e nutrientes. Essas informações são enviadas para um sistema que registra, analisa e gera insights para:

  1. Aplicar água e nutrientes na medida certa;
  2. Fazer previsões de necessidades futuras;
  3. Monitorar a saúde do solo;
  4. Aumentar a produtividade;
  5. Reduzir desperdícios e otimizar recursos;
  6. Identificar padrões de desempenho das plantações ao longo do tempo,
  7. Facilitar auditorias técnicas com rastreabilidade de quem executou cada ação. 

## Objetivos do Projeto
  1. Armazenar informações detalhadas sobre sensores, plantações e aplicações;
  2. Rastrear ações feitas no campo por usuários responsáveis;
  3. Gerar histórico de análises e decisões técnicas;
  4. Representar os relacionamentos entre os dados de forma estruturada;
  5. Permitir expansão futura com dados geográficos e novas funcionalidades;
  7. Permitir análises preditivas para antecipar necessidades da lavoura;
  8. Oferecer suporte à tomada de decisão por meio de relatórios estruturados.

## Entidades e Atributos
1. Entidade: plantacao
Representa cada plantação monitorada.
  Seus atributos:
    plantacao_ID: identificador único da plantação (PK)
    cultura_tipo: tipo de cultura plantada (ex: milho, soja)
    localizacao_fazenda: descrição textual do local
    area_m2: área da plantação em metros quadrados
    latitude / longitude: localização geográfica da plantação

2. Entidade: sensores
Sensores utilizados no campo.
  Seus atributos:
    sensor_ID: identificador do sensor (PK)
    sensor_tipo: nome ou modelo do sensor
    sensor_modelo: modelo ou código de série
    unidade_medida_sensor: unidade utilizada na medição (ex: %, pH)
    tipo_sensor_ID: chave estrangeira que aponta para a entidade tipo_sensor (FK)

3. Entidade: tipo_sensor
Armazena os tipos de sensores disponíveis.
  Seus atributos: 
    tipo_sensor_ID: identificador (PK)
    nome_tipo_sensor: nome (ex: S1, S2, S3)
    descricao: descrição do tipo de sensor (ex: "umidade do solo")

4. Entidade: leitura_sensor
Registra as leituras feitas pelos sensores.
   Seus atributos:
    leitura_ID: identificador da leitura (PK)
    sensor_ID: sensor responsável pela leitura (FK)
    plantacao_ID: plantação onde foi feita a leitura (FK)
    data_hora: data e hora da leitura
    valor: valor registrado (numérico)

5. Entidade: uso_agua
Aplicações de água na plantação.
  Seus atributos:
    aplicacao_ID: identificador (PK)
    plantacao_ID: qual plantação recebeu água (FK)
    data_hora: data e hora da aplicação
    quantidade_emitros: quantidade de água aplicada em litros

6. Entidade: uso_nutrientes
Aplicações de nutrientes do tipo NPK.
  Seus atributos:
    aplicacao_ID: identificador (PK)
    plantacao_ID: plantação onde foi feita a aplicação (FK)
    data_hora: data e hora da aplicação
    fosforo_quantidade: quantidade de fósforo (P) aplicada
    potassio_quantidade: quantidade de potássio (K) aplicada

7. Entidade: analise_notempo
Sugestões de ajuste feitas a partir de análises dos dados.
  Seus atributos: 
    analise_ID: identificador (PK)
    plantacao_ID: plantação analisada (FK)
    data_analise: data da análise
    tipo_analise: tipo de análise realizada
    sugestao_de_ajuste: recomendação gerada (texto)
    usuario_usuario_ID: usuário que registrou a análise (FK)

8. Entidade: sensor_manutencao
Registros de manutenção dos sensores.
  Seus atributos:
    manutencao_ID: identificador (PK)
    sensor_ID: sensor que passou por manutenção (FK)
    data_manutencao: data da manutenção
    descricao: o que foi feito
    responsabilidade_tecnica: responsável
    usuario_usuario_ID: técnico ou usuário responsável (FK)

9. Entidade: sensor_plantacao
Tabela intermediária para relacionamento N:N entre sensores e plantações.
  Seus atributos:
    sensor_ID: identificador do sensor (PK + FK)
    plantacao_ID: identificador da plantação (PK + FK)
    data_associacao: data em que o sensor foi instalado na plantação

10. Entidade: usuario
Usuários do sistema (técnicos, agrônomos, operadores).
  Seus atributos: 
    usuario_ID: identificador (PK)
    usuario_nome: nome completo
    email: contato
    cargo: função no sistema (ex: analista, técnico, operador)

## Relacionamentos dentro do sistema
  1:N
    plantacao → leitura_sensor, uso_agua, uso_nutrientes, analise_notempo, sensor_plantacao
    sensores → leitura_sensor, sensor_plantacao, sensor_manutencao
    tipo_sensor → sensores
    usuario → analise_notempo, sensor_manutencao

  N:N
    plantacao ↔ sensores (via sensor_plantacao)

## Geolocalização 
A entidade plantacao foi aprimorada com os campos latitude e longitude para permitir visualizações em mapas e facilitar tomadas de decisão baseadas em localização.

## Arquivos incluídos
agricultura-digital-FIAP-2025-TAYNAESTEVES.dmd: arquivo original criado no Oracle SQL Developer Data Modeler
der-agricultura-digital-fiap-2025-taynaesteves.png: imagem final do DER
README.md: este documento com explicações detalhadas do MER

- [📄 Ver DER (.png)](./der-agricultura-digital-fiap-2025-taynaesteves.png)
- [📁 Baixar modelo .dmd](./agricultura-digital-FIAP-2025-TAYNAESTEVES.dmd)

```markdown
# Checklist de Descoberta de Requisitos para Microserviços
**(Spring Boot + Kafka + Domain-Driven Design)**

---

# 1. Contexto de Negócio

## Problema
- Que problema de negócio estamos a resolver?
- Porque é que este serviço é necessário?
- O que acontece atualmente se este serviço não existir?
- Quem são os stakeholders?
- Quem solicitou esta funcionalidade?
- Qual é o resultado de negócio esperado?
- Como será medido o sucesso?
- Que KPIs deverão melhorar?

## Âmbito
- O que está incluído no âmbito?
- O que está explicitamente fora do âmbito?
- Existem funcionalidades futuras que devemos antecipar?
- Este serviço vem substituir outro já existente?

---

# 2. Descoberta do Domínio (DDD)

## Bounded Context
- A que **Bounded Context** pertence este serviço?
- Existe sobreposição com outro **Bounded Context**?
- Que equipa é responsável por este domínio?

## Modelo de Domínio
- Quais são as principais entidades?
- Quais são os Value Objects?
- Que agregados existem?
- Quais são os Aggregate Roots?
- Que invariantes nunca podem ser violadas?
- Que conceitos pertencem ao negócio e quais são apenas técnicos?

## Linguagem Ubíqua
- Que terminologia utiliza o negócio?
- Existem termos frequentemente mal interpretados pelos programadores?
- Existem sinónimos que devemos evitar?

---

# 3. Processo de Negócio

## Fluxo Principal
- Descreva o fluxo normal do processo.
- O que desencadeia o processo?
- Qual é o resultado final esperado?

## Fluxos Alternativos
- Que variações existem?
- Existem passos opcionais?

## Fluxos de Erro
- O que pode correr mal?
- Como deve o negócio reagir?
- Em que situações é necessária intervenção manual?

---

# 4. Responsabilidades do Serviço

- Qual é a responsabilidade deste serviço?
- O que este serviço não deve fazer?
- Que serviço é responsável por esta capacidade de negócio?
- Este serviço deve orquestrar ou apenas executar?
- Existe outro serviço que já desempenhe parte desta responsabilidade?

---

# 5. Propriedade dos Dados

- Que dados pertencem a este serviço?
- Que dados são apenas de leitura?
- Que dados são provenientes de outros serviços?
- Outro serviço pode alterar estes dados?
- Estes dados são mantidos em cache?
- Durante quanto tempo são considerados válidos?

---

# 6. Ciclo de Vida dos Objetos

Para cada entidade:

- Como é criada?
- Como é atualizada?
- Pode ser eliminada?
- Pode ser restaurada?
- Pode expirar?
- Pode ser arquivada?
- Quem pode executar cada ação?
- Que estados pode assumir?
- Que transições de estado são inválidas?

---

# 7. Regras de Negócio

- Quais são as regras obrigatórias?
- Quais são configuráveis?
- Quais mudam com maior frequência?
- Quem é responsável por cada regra?
- Existem exceções às regras?
- Em que circunstâncias?

---

# 8. Validações

- Que validações são efetuadas antes do processamento?
- Que validações são efetuadas depois do processamento?
- Quais são validações de negócio?
- Quais são validações técnicas?
- Existem validações assíncronas?
- O que acontece quando uma validação falha?

---

# 9. Requisitos da API

## Endpoints

- Que operações são necessárias?
- Que parâmetros são obrigatórios?
- Qual o resultado esperado?

## Contratos

- REST?
- gRPC?
- GraphQL?

## Versionamento

- Como são geridas alterações incompatíveis?
- Como são suportados clientes antigos?
- Que campos são opcionais?
- Que campos poderão desaparecer no futuro?

---

# 10. Arquitetura Event-Driven (Kafka)

## Produtores

- Que eventos são publicados?
- Porque são publicados?
- Em que momento são publicados?

## Consumidores

- Que eventos são consumidos?
- O que desencadeia o processamento?
- O que acontece se o mesmo evento chegar duas vezes?

## Modelação dos Eventos

- O evento representa um facto ou um comando?
- Que ação de negócio representa?
- Os consumidores devem reagir imediatamente?

## Tópicos

- Em que tópico será publicado?
- Qual é a chave de partição?
- Porque foi escolhida essa chave?
- A ordem dos eventos é importante?
- A ordem é importante apenas por chave ou globalmente?

## Fiabilidade

- É aceitável receber eventos duplicados?
- Como é garantida a idempotência?
- O que acontece se o Kafka estiver indisponível?
- O que acontece se a publicação falhar?
- Devem existir tentativas automáticas?
- Quantas tentativas?
- Quando deve uma mensagem ser enviada para uma Dead Letter Queue (DLQ)?
- Como são tratadas mensagens inválidas (poison messages)?
- Durante quanto tempo devem os eventos ser mantidos?

---

# 11. Transações e Consistência

- A consistência eventual é aceitável?
- Existe necessidade de uma transação distribuída?
- Será necessário implementar um Saga?
- Como são tratadas ações de compensação?
- O que acontece se uma etapa falhar depois de outra já ter sido concluída?
- Como deve decorrer a recuperação?

---

# 12. Cenários de Falha

- O que acontece se a base de dados estiver indisponível?
- O que acontece se o Kafka estiver indisponível?
- O que acontece se outro microserviço estiver indisponível?
- O que acontece em caso de timeout?
- O que acontece se o mesmo pedido chegar duas vezes?
- O que acontece se os eventos chegarem fora de ordem?
- O que acontece se o processamento for interrompido a meio?
- A operação pode ser repetida em segurança?

---

# 13. Integrações

- Com que sistemas este serviço se integra?
- Quem é responsável por cada integração?
- A comunicação é síncrona ou assíncrona?
- Existem SLAs definidos?
- Qual é a integração mais frágil?
- Como são comunicadas falhas de integração?

---

# 14. Desempenho

- Quantos pedidos por segundo são esperados?
- Quantas mensagens Kafka por segundo são esperadas?
- Qual é o volume de tráfego em pico?
- Qual é o volume médio?
- Qual é a latência máxima aceitável?
- Qual é o tempo máximo de resposta?
- Qual é o tempo esperado de processamento?
- Qual é o débito (throughput) esperado?

---

# 15. Escalabilidade

- O que acontece se o tráfego aumentar 10 vezes?
- Qual será o primeiro componente a tornar-se um gargalo?
- O processamento pode ser paralelo?
- O serviço pode escalar horizontalmente?
- Existem restrições de ordenação que impeçam a escalabilidade?

---

# 16. Segurança

- Quem pode invocar este serviço?
- Como é feita a autenticação?
- Como é feita a autorização?
- Que perfis de utilizador existem?
- Que dados são sensíveis?
- Os dados devem ser cifrados?
- É necessário manter auditoria?
- Existem requisitos legais ou regulamentares?

---

# 17. Monitorização e Observabilidade

- Que métricas devem ser monitorizadas?
- Que informação deve ser registada em logs?
- Que traces devem existir?
- Que alertas devem ser configurados?
- Como identificar uma falha de negócio?
- Como identificar uma falha técnica?
- Como é verificada a saúde do serviço?

---

# 18. Configuração

- Que parâmetros devem ser configuráveis?
- Que parâmetros obrigam a novo deployment?
- A configuração pode ser alterada em tempo de execução?
- São necessárias feature flags?

---

# 19. Tempo e Agendamento

- Os fusos horários são relevantes?
- Existem horários de funcionamento?
- Existem prazos a cumprir?
- Existem tarefas agendadas?
- Existem tentativas automáticas agendadas?
- A mudança da hora (Daylight Saving Time) tem impacto?

---

# 20. Concorrência

- Vários utilizadores podem alterar os mesmos dados em simultâneo?
- Que operações devem ser serializadas?
- Como são resolvidos conflitos?
- É necessário optimistic locking?
- É necessário pessimistic locking?

---

# 21. Qualidade dos Dados

- Que campos são obrigatórios?
- Que campos são opcionais?
- Podem existir registos duplicados?
- Como é efetuada a limpeza de dados?
- O que acontece quando os dados são inválidos?

---

# 22. Migração

- É necessária migração de dados existentes?
- Como serão mapeados os identificadores antigos?
- É necessário efetuar backfill?
- Durante quanto tempo coexistirão os sistemas antigos?

---

# 23. Relatórios

- Existem relatórios que dependem destes dados?
- Que relatórios consomem esta informação?
- É necessário manter histórico?
- Durante quanto tempo deve o histórico ser conservado?

---

# 24. Testes

- Quais são os critérios de aceitação?
- Que cenários têm obrigatoriamente de funcionar?
- Que casos limite devem ser testados?
- Que cenários de falha devem ser simulados?
- Que integrações requerem Contract Testing?

---

# 25. Deployment e Operação

- Como será efetuado o deployment?
- É necessário deployment sem indisponibilidade?
- Qual é a estratégia de rollback?
- Qual é o RTO (Recovery Time Objective)?
- Qual é o RPO (Recovery Point Objective)?
- Existem requisitos de Disaster Recovery?

---

# 26. Governação

- Quem é responsável por este serviço?
- Quem aprova alterações à API?
- Quem aprova alterações ao esquema de dados?
- Quem fica de prevenção (on-call)?
- Quem é responsável pelos incidentes em produção?

---

# 27. Revisão da Arquitetura

- Porque é necessário criar um novo microserviço em vez de reutilizar um existente?
- Porque foi escolhida comunicação síncrona?
- Porque foi escolhida comunicação assíncrona?
- Porque é que este serviço é responsável por estes dados?
- Que compromissos arquiteturais (trade-offs) estão a ser assumidos?
- Que pressupostos estamos a fazer?
- Que restrições existem?
- Que dívida técnica estamos dispostos a aceitar?

---

# 28. Perguntas Finais

- Que pressupostos estamos a fazer?
- O que mais o preocupa nesta funcionalidade?
- Que caso extremo considera mais arriscado?
- O que surpreenderia negativamente os utilizadores?
- O que poderia fazer este projeto falhar?
- Que pergunta deveria ter feito e não fiz?
- Que regra de negócio é mais fácil esquecer?
- Se implementarmos exatamente o que discutimos hoje, o que continuará a faltar?
```

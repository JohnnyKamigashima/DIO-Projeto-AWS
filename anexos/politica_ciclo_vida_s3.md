# Política de Ciclo de Vida de Dados — Amazon S3

Empresa: Abstergo Industries
Escopo: dados armazenados no Amazon S3 (documentos regulatórios, laudos, resultados de pesquisa, backups e mídias)
Objetivo: reduzir custo de armazenamento mantendo a disponibilidade e a conformidade regulatória exigida no setor farmacêutico, movendo automaticamente os dados para camadas mais baratas conforme o padrão de acesso diminui.

## Regras de transição por classe de armazenamento

| Fase | Idade do objeto | Classe de destino | Justificativa |
|---|---|---|---|
| 1 | 0–29 dias | S3 Standard | Dados recém-criados, com alta probabilidade de acesso frequente (ex.: laudos em análise, documentos em revisão) |
| 2 | A partir de 30 dias | S3 Intelligent-Tiering | Move automaticamente entre camadas frequente/infrequente conforme o padrão de acesso real, sem necessidade de regras manuais adicionais |
| 3 | A partir de 180 dias sem acesso | S3 Glacier Flexible Retrieval | Dados históricos com baixa probabilidade de consulta, mas que ainda podem ser solicitados (recuperação em minutos a horas) |
| 4 | A partir de 365 dias sem acesso | S3 Glacier Deep Archive | Dados de arquivamento de longo prazo (ex.: registros regulatórios antigos), com menor custo de armazenamento e recuperação em até 12 horas |

## Retenção e exclusão

- Objetos sujeitos a exigências regulatórias (documentação de Boas Práticas de Fabricação, registros de lote, laudos analíticos) não devem ser excluídos automaticamente; a expiração deve seguir o prazo definido pela área de Compliance/Regulatório da empresa, conforme legislação aplicável (ex.: ANVISA, BPF/GMP), a ser confirmado formalmente com essa área antes da implementação.
- Dados não regulatórios (rascunhos, arquivos temporários, logs de aplicação) podem ter expiração automática configurada, sugerida em 90 dias após a última modificação, salvo indicação em contrário.
- Versionamento deve ser habilitado nos buckets com dados críticos, com regra de expiração de versões não-atuais após 90 dias, para evitar acúmulo de custo com versões antigas.

## Multipart uploads incompletos

- Uploads multipart não finalizados devem ser automaticamente excluídos após 7 dias, evitando cobrança por partes de arquivo órfãs.

## Monitoramento

- Revisão trimestral das regras de ciclo de vida e dos relatórios de custo do S3 (via AWS Cost Explorer / S3 Storage Lens) para validar se os padrões de acesso reais continuam alinhados às regras definidas.
- Ajustes nas regras devem ser aprovados pela equipe de infraestrutura em conjunto com Compliance, quando envolverem dados regulatórios.

## Observação

Os prazos acima são uma proposta inicial de dimensionamento técnico. Prazos de retenção mínima de documentos regulatórios do setor farmacêutico devem ser validados e formalizados com a área jurídica/regulatória da Abstergo Industries antes da configuração definitiva das regras de expiração no S3.

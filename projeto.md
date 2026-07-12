# RELATÓRIO DE IMPLEMENTAÇÃO DE SERVIÇOS AWS

Data: 12/07/2026 Empresa: Abstergo Industries Responsável: Johnny Kamigashima

## Introdução

Este relatório apresenta o processo de implementação de ferramentas na empresa Abstergo Industries, realizado por Johnny Kamigashima. O objetivo do projeto foi elencar 3 serviços AWS, com a finalidade de realizar diminuição de custos imediatos, no contexto da migração da infraestrutura da empresa (do setor farmacêutico) para a nuvem, com foco em escalabilidade e redução de custos.

## Descrição do Projeto

O projeto de implementação de ferramentas foi dividido em 3 etapas, cada uma com seus objetivos específicos. A seguir, serão descritas as etapas do projeto:

Etapa 1:

- Amazon EC2 Auto Scaling
- Escalabilidade e otimização de custos de computação
- Os sistemas da Abstergo (como o portal de pedidos e as aplicações internas de pesquisa) sofrem picos de demanda em horários e épocas específicas (ex.: fechamento de lotes de produção, campanhas sazonais). Com o Auto Scaling, o número de instâncias EC2 é ajustado automaticamente conforme a demanda, evitando pagar por capacidade ociosa fora dos picos e garantindo disponibilidade quando o uso cresce, sem necessidade de dimensionar a infraestrutura para o pior cenário o tempo todo.

Etapa 2:

- AWS Lambda
- Computação sem servidor com cobrança por uso
- Processos pontuais e orientados a eventos, como validação de laudos, geração de relatórios regulatórios e integrações entre sistemas internos, passam a rodar em funções Lambda. Como o serviço cobra apenas pelo tempo de execução (sem servidores ociosos para manter), a empresa reduz custos operacionais nesses fluxos e ainda ganha escalabilidade automática para lidar com variações de volume de processamento.

Etapa 3:

- Amazon S3 (com classes de armazenamento, incluindo Intelligent-Tiering e Glacier)
- Armazenamento de dados escalável e de baixo custo
- Dados da Abstergo com diferentes padrões de acesso — documentos regulatórios, resultados de pesquisa, backups e mídias — passam a ser armazenados no S3. Com o Intelligent-Tiering e as classes Glacier, arquivos pouco acessados (como registros históricos exigidos por compliance farmacêutico) migram automaticamente para camadas mais baratas, reduzindo custo de armazenamento sem perder a escalabilidade praticamente ilimitada do serviço.



## Conclusão

A implementação de ferramentas na empresa *Abstergo Industries tem como esperado redução dos custos de infraestrutura via cobrança por uso e eliminação de capacidade ociosa, maior escalabilidade para absorver picos de demanda sem intervenção manual, e maior resiliência operacional*, o que aumentará a eficiência e a produtividade da empresa. Recomenda-se a continuidade da utilização das ferramentas implementadas e a busca por novas tecnologias que possam melhorar ainda mais os processos da empresa.

## Anexos

Diagrama de arquitetura da migração

*Diagrama de arquitetura da migração: usuários acessam a aplicação via Internet Gateway e Elastic Load Balancing, que distribui o tráfego entre instâncias EC2 gerenciadas por um Auto Scaling Group em múltiplas zonas de disponibilidade.* 

*Eventos e chamadas de API acionam funções AWS Lambda para processamento sem servidor. Tanto as instâncias EC2 quanto as funções Lambda gravam dados no Amazon S3, cuja política de ciclo de vida move automaticamente dados pouco acessados para as camadas Intelligent-Tiering e Glacier, reduzindo custo de armazenamento.*



Planilha de estimativa de custos: [estimativa_custos_aws.xlsx](anexos/estimativa_custos_aws.xlsx)

Política de ciclo de vida de dados no S3: [politica_ciclo_vida_s3.md](anexos/politica_ciclo_vida_s3.md)

Assinatura do Responsável pelo Projeto:

Johnny Kamigashima
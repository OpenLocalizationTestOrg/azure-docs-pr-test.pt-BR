Armazenamento é restrito por espaço em disco ou por um limite rígido na Olá *número máximo* de índices ou documentos, o que ocorrer primeiro.

| Recurso | Grátis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Contrato de nível de serviço (SLA) |Não <sup>1</sup> |Sim |Sim |Sim |Sim |Sim |
| Armazenamento por partição |50 MB |2 GB |25 GB |100 GB |200 GB |200 GB |
| Partições por serviço |N/D |1 |12 |12 |12 |3 <sup>2</sup> |
| Tamanho da partição |N/D |2 GB |25 GB |100 GB |200 GB |200 GB |
| Réplicas |N/D |3 |12 |12 |12 |12 |
| Índices máximos |3 |5 |50 |200 |200 |1000 por partição ou 3000 por serviço |
| Indexadores máximos |3 |5 |50 |200 |200 |Não há suporte do indexador |
| Máximo de fontes de dados |3 |5 |50 |200 |200 |Não há suporte do indexador |
| Máximo de documentos |10.000 |1 milhão |15 milhões por partição ou 180 milhões por serviço |60 milhões por partição ou 720 milhões por serviço |120 milhões por partição ou 1,4 bilhão por serviço |1 milhão por serviço, 200 milhões por partição |
| Estimativa de QPS (Consultas por segundo) |N/D |~3 por réplica |~15 por réplica |~60 por réplica |~60 por réplica |>60 por réplica |

<sup>1</sup> Os recursos de camada gratuita e de versão prévia não vêm com SLAs (contratos de nível de serviço). Para todas as camadas faturáveis, os SLAs entram em vigor quando você provisiona redundância suficiente para o serviço. Duas ou mais réplicas são necessárias para o SLA de consulta (leitura). Três ou mais réplicas são necessárias para consulta e indexação do SLA (leitura-gravação). número de saudação de partições não é uma consideração de SLA. 

<sup>2</sup> S3 HD tem um limite rígido de 3 partições, que é inferior ao limite da partição Olá para S3. limite inferior de partição Olá é imposto porque a contagem de índice de saudação do HD S3 é significativamente maior. Considerando que existem limites de serviço para ambos os recursos de computação (processamento e armazenamento) e conteúdo (índices e documentos), Olá conteúdo limite for atingido primeiro.

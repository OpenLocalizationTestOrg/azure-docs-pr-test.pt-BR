Olá, a tabela a seguir descreve cada uma das principais cotas de hello, limites, padrões e limitações no Agendador do Azure.

| Recurso | Descrição de limite |
| --- | --- |
| **Tamanho do trabalho** |O tamanho máximo do trabalho é 16K. Se um PUT ou PATCH resultarem em um trabalho maior do que esses limites, é retornado um código de status 400 Solicitação incorreta. |
| **Tamanho da solicitação de URL** |Tamanho máximo da URL de solicitação de saudação é 2048 caracteres. |
| **Tamanho do cabeçalho de agregação** |O tamanho máximo do cabeçalho agregação é de 4096 caracteres. |
| **Contagem de cabeçalho** |A contagem máxima do cabeçalho é de 50 cabeçalhos. |
| **Tamanho do corpo** |O tamanho máximo do corpo é de 8192 caracteres. |
| **Intervalo de recorrência** |O período máximo de recorrência é de 18 meses. |
| **Tempo de toostart de tempo** |"Hora toostart horário" o máximo é 18 meses. |
| **Histórico de trabalho** |O corpo de resposta máximo armazenado no histórico de trabalho é de 2048 bytes. |
| **Frequência** |cota de frequência máxima saudação padrão é 1 hora em uma coleção de trabalhos livre e 1 minuto em uma coleção de trabalhos padrão. frequência máxima de saudação é configurável em um menor do que o máximo de saudação do trabalho coleção toobe. Todos os trabalhos na coleção de trabalhos de saudação são valor limitado Olá definido na coleção de trabalho hello. Se você tentar toocreate um trabalho com uma frequência superior a frequência máxima Olá na coleção de trabalhos de saudação solicitação falhará com um código de status 409 Conflito. |
| **Trabalhos** |Olá cota máxima padrão é 5 trabalhos em uma coleção de trabalhos livre e 50 trabalhos em uma coleção de trabalhos padrão. número máximo de saudação de trabalhos é configurável em uma coleção de trabalhos. Todos os trabalhos na coleção de trabalhos de saudação são valor limitado Olá definido na coleção de trabalho hello. Se você tentar toocreate mais trabalhos do que a cota máxima de trabalhos de saudação e solicitação de saudação falhará com um código de status 409 Conflito. |
| **Coleções de trabalho** |O número máximo de coleções de trabalho por assinatura é de 200,000. |
| **Retenção de histórico de trabalho** |Histórico do trabalho é retido para o too2 meses ou backup toohello última execuções de 1000. |
| **Retenção de trabalhos concluídos e com falha** |Os trabalhos concluídos e com falha são armazenados por 60 dias. |
| **Tempo limite** |Há um tempo limite da solicitação (não configurável) estático de 60 segundos para ações de HTTP. Para operações mais demoradas em execução, execute protocolos assíncronos de HTTP; Por exemplo, retorne um 202 imediatamente, mas continuar trabalhando no plano de fundo de saudação. |


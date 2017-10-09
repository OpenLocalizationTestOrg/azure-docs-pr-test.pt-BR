## <a name="what-is-queue-storage"></a>O que é armazenamento de fila?
Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.

Usos comuns de Armazenamento de filas incluem:

* Criando uma lista de pendências de trabalho tooprocess assincronamente
* Transmissão de mensagens de uma função de trabalho do Azure de tooan de função web do Azure

## <a name="queue-service-concepts"></a>Conceitos do Serviço da Fila
Olá serviço fila contém Olá componentes a seguir:

![Fila1](./media/storage-queue-concepts-include/queue1.png)

* **Formato de URL:** filas são acessadas usando Olá formato de URL a seguir:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Olá URL a seguir aborda uma fila no diagrama de saudação:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../articles/storage/common/storage-scalability-targets.md) para obter detalhes sobre a capacidade da conta de armazenamento.
* **Fila:** uma fila contém um conjunto de mensagens. Todas as mensagens devem estar em uma fila. Observe que nome de fila Olá deve ser todas minúscula. Para saber mais sobre filas de nomenclatura, confira [Nomenclatura de filas e metadados](https://msdn.microsoft.com/library/azure/dd179349.aspx).
* **Mensagem:** A mensagem, em qualquer formato de backup too64 KB. tempo máximo de saudação que uma mensagem pode permanecer na fila de saudação é 7 dias.


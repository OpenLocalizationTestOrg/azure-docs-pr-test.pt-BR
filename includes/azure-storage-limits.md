| Recurso | Limite padrão |
| --- | --- |
| Número máximo de contas de armazenamento por assinatura |200<sup>1</sup> |
| Capacidade máxima da conta de armazenamento |500 TB<sup>2</sup> |
| Número máximo de contêineres de blob, blobs, compartilhamentos de arquivo, tabelas, filas, entidades ou mensagens por conta de armazenamento |Sem limite |
| Tamanho máximo de um único contêiner de blob, tabela ou fila |O mesmo da capacidade máxima da conta de armazenamento |
| Número máximo de blocos em um blob de blocos ou de acréscimo |50.000 |
| Tamanho máximo de um bloco em um blob de blocos |100 MB |
| Tamanho máximo de um blob de blocos |50.000 x 100 MB (aprox. 4,75 TB) |
| Tamanho máximo de um bloco em um blob de acréscimo |4 MB |
| Tamanho máximo de um blob de acréscimo |50.000 x 4 MB (aproximadamente 195 GB) |
| Tamanho máximo de um blob de páginas |8 TB |
| Tamanho máximo de uma entidade de tabela |1 MB |
| Número máximo de propriedades em uma entidade de tabela |252 |
| Tamanho máximo de uma mensagem em uma fila |64 KB |
| Tamanho máximo de um compartilhamento de arquivo |5 TB |
| Tamanho máximo de um arquivo em um compartilhamento de arquivos |1 TB |
| Número máximo de arquivos em um compartilhamento de arquivo |Somente o limite é de capacidade total de 5 TB de Olá Olá do compartilhamento de arquivos |
| IOPS máximo por compartilhamento |1000 |
| Número máximo de arquivos em um compartilhamento de arquivo |Somente o limite é de capacidade total de 5 TB de Olá Olá do compartilhamento de arquivos |
| Número máximo de políticas de acesso armazenada por contêiner, compartilhamento de arquivos, tabela ou fila |5 |
| Taxa Máxima de Solicitação por conta de armazenamento |BLOBs: solicitações 20.000 por segundo<sup>2</sup> para blobs de qualquer tamanho válido (limitado somente por limites de entrada/saída da conta Olá) <br />Arquivos: 1000 IOPS (de 8 KB) por compartilhamento de arquivos <br />Filas: 20.000 mensagens por segundo (supondo que o tamanho de mensagem seja de 1 KB)<br />Tabelas: 20.000 transações por segundo (supondo que tamanho de entidade seja de 1 KB) |
| Taxa de transferência de destino para blob único |Backup too60 MB por segundo ou backup too500 solicitações por segundo |
| Taxa de transferência de destino para fila única (mensagens de 1 KB) |As mensagens de too2000 por segundo |
| Meta de taxa de transferência para partição de tabela única (entidades de 1 KB) |Backup too2000 entidades por segundo |
| Taxa de transferência de destino para compartilhamento de arquivo único |Too60 MB por segundo |
| Entrada máxima<sup>3</sup> por conta de armazenamento (Regiões dos EUA) |10 Gbps se o GRS/ZRS<sup>4</sup> estiver habilitado, 20 Gbps para o LRS<sup>2</sup> |
| Saída máxima<sup>3</sup> por conta de armazenamento (Regiões dos EUA) |20 Gbps se o RA-GRS/GRS/ZRS<sup>4</sup> estiver habilitado, 30 Gbps para o LRS<sup>2</sup> |
| Entrada máxima<sup>3</sup> por conta de armazenamento (Regiões fora dos EUA) |5 Gbps se o GRS/ZRS<sup>4</sup> estiver habilitado, 10 Gbps para o LRS<sup>2</sup> |
| Saída máxima<sup>3</sup> por conta de armazenamento (Regiões fora dos EUA) |10 Gbps se o RA-GRS/GRS/ZRS<sup>4</sup> estiver habilitado, 15 Gbps para o LRS<sup>2</sup> |

<sup>1</sup>Isso inclui contas de armazenamento Standard e Premium. Se você precisar de mais de 200 contas de armazenamento, faça uma solicitação por meio do [Suporte do Azure](https://azure.microsoft.com/support/faq/). equipe de armazenamento do Azure Olá examine seu caso de negócios e pode aprovar as contas de armazenamento too250. 

<sup>2</sup> tooget toogrow anterior de contas de armazenamento padrão Olá anunciados limites de taxa de capacidade, a entrada/saída e a solicitação, verifique uma solicitação por meio de [suporte do Azure](https://azure.microsoft.com/support/faq/). equipe de armazenamento do Azure Olá examine solicitação hello e Aprovar limites maiores caso a caso.

<sup>3</sup>*entrada* refere-se a dados tooall (solicitações) sendo enviados tooa conta de armazenamento. *Saída* refere-se tooall dados (respostas) sendo recebidos de uma conta de armazenamento.  

<sup>4</sup>As opções de replicação do Armazenamento do Azure incluem:
* **RA-GRS**: armazenamento com redundância geográfica com acesso de leitura. Se RA-GRS estiver habilitada, destinos de saída para o local secundário hello serão toothose idêntico para o local primário hello.
* **GRS**: armazenamento com redundância geográfica. 
* **ZRS**: armazenamento com redundância de zona. Disponível apenas para blobs de blocos. 
* **LRS**: armazenamento com redundância local. 



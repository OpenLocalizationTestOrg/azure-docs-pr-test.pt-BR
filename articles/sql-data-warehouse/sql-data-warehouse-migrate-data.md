---
title: aaaMigrate tooSQL seus dados do Data Warehouse | Microsoft Docs
description: "Dicas para migrar sua tooAzure de dados SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Migrar seus dados
Os dados podem ser movidos de diferentes origens no SQL Data Warehouse com uma variedade de ferramentas.  Cópia de ADF, SSIS e todos os bcp pode ser usado tooachieve essa meta. No entanto, como Olá quantidade de dados aumenta, deve pensar dividindo o processo de migração de dados de saudação em etapas. Isso lhe dá a você Olá oportunidade toooptimize cada etapa para desempenho e resiliência tooensure uma migração de dados sem problemas.

Primeiro, este artigo descreve os cenários de migração simples de saudação de cópia do ADF, SSIS e bcp. Em seguida, procure um pouco mais em como migração Olá pode ser otimizada.

## <a name="azure-data-factory-adf-copy"></a>Cópia do ADF (Azure Data Factory)
A [Cópia do ADF][ADF Copy] faz parte do [Azure Data Factory][Azure Data Factory]. Você pode usar a cópia ADF tooexport tooflat arquivos de dados do que reside no armazenamento local, arquivos simples tooremote mantidos no armazenamento de BLOBs do Azure ou diretamente no SQL Data Warehouse.

Se seus dados começam em arquivos simples, você precisará primeiro tootransfer-tooAzure blob de armazenamento antes de iniciar um carregamento no SQL Data Warehouse. Quando dados saudação for transferidos para o armazenamento de BLOBs do Azure, você pode escolher toouse [cópia ADF] [ ADF Copy] toopush dados de saudação novamente no SQL Data Warehouse.

PolyBase também fornece uma opção de alto desempenho para carregar dados de saudação. No entanto, isso significa usar duas ferramentas em vez de uma. Se você precisa obter um melhor desempenho hello, usa o PolyBase. Se você quiser uma experiência única ferramenta (e dados de saudação não são grandes) ADF é sua resposta.


> 
> 

Principal sobre toohello após o artigo para alguns ótimo [exemplos ADF][ADF samples].

## <a name="integration-services"></a>Serviços de integração
O SSIS (SQL Server Integration Services) é uma ferramenta de ETL (Extração, Transformação e Carregamento) avançada e flexível que oferece suporte a fluxos de trabalho complexos, transformação de dados e várias opções de carregamento de dados. Usar o SSIS toosimply transferência dados tooAzure ou como parte de uma migração mais ampla.

> [!NOTE]
> O SSIS pode exportar tooUTF-8 sem Olá marca de ordem de bytes no arquivo hello. tooconfigure isso primeiro você deve usar Olá derivado coluna componente tooconvert Olá dados de caracteres hello dados fluxo toouse Olá 65001 UTF-8 página de código. Quando colunas Olá tem sido convertidas, escreva Olá dados toohello arquivo simples destino adaptador garantindo que 65001 também foi selecionada como a página de código Olá para o arquivo hello.
> 
> 

SSIS tooSQL Data Warehouse conecta-se exatamente como ele se conectaria tooa implantação de SQL Server. No entanto, as conexões precisará toobe usando um Gerenciador de conexão ADO.NET. Você também deve ter cuidado tooconfigure hello "Usar o inserção em massa quando disponível" taxa de transferência de toomaximize de configuração. Consulte toohello [adaptador de destino ADO.NET] [ ADO.NET destination adapter] artigo toolearn mais sobre essa propriedade

> [!NOTE]
> Não há suporte para a conexão tooAzure SQL Data Warehouse usando OLEDB.
> 
> 

Além disso, sempre há possibilidade de saudação que um pacote pode falhar devido a problemas de rede ou toothrottling. Design de pacotes para que eles possam ser retomados no ponto de saudação de falha, sem refazer o trabalho concluído antes de falha de saudação.

Para obter mais informações, consulte Olá [documentação SSIS][SSIS documentation].

## <a name="bcp"></a>bcp
O bcp é um utilitário de linha de comando desenvolvido para importação e exportação de dados de arquivo simples. Algumas transformações podem ocorrer durante a exportação de dados. transformações de tooperform simples usam uma consulta tooselect e transform dados de hello. Uma vez exportado, arquivos simples hello, em seguida, podem ser carregados diretamente no banco de dados do SQL Data Warehouse Olá Olá destino.

> [!NOTE]
> Geralmente é Olá de tooencapsulate uma boa ideia exportar transformações usadas durante a dados em uma exibição no sistema de origem de saudação. Isso garante que lógica Olá é retida e o processo de saudação é repetido.
> 
> 

As vantagens do bcp são:

* Simplicidade. comandos de BCP são toobuild simple e executar
* Processo de carregamento reinicializável. Uma vez exportado Olá carga pode ser executado várias vezes

As limitações do bcp são:

* O bcp funciona somente com arquivo simples tabulados. Ele não funciona com arquivos xml ou JSON, por exemplo
* Recursos de transformação de dados são toohello limitado somente estágio de exportação e são simples de natureza
* BCP não foi adaptada toobe robusto ao carregar dados sobre Olá da internet. Qualquer instabilidade de rede pode causar um erro de carregamento.
* BCP depende do esquema Olá presente na carga de toohello anterior de banco de dados de destino Olá

Para obter mais informações, consulte [usar dados do bcp tooload no SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Otimizando a migração de dados
Um processo de migração de dados SQLDW pode ser dividido efetivamente em três etapas distintas:

1. Exportação dos dados de origem
2. Transferência de dados tooAzure
3. Carregar no banco de dados do hello destino SQLDW

Cada etapa pode ser otimizado individualmente toocreate um processo de migração robusta, reinicializável e resiliente que maximiza o desempenho em cada etapa.

## <a name="optimizing-data-load"></a>Otimizando o carregamento de dados
Olhando na ordem inversa para um momento; dados de tooload de maneira mais rápidos de saudação são por meio do PolyBase. Otimização para um processo de carregamento do PolyBase exige pré-requisitos de Olá etapas anteriores é melhor toounderstand isso inicial. Eles são:

1. Codificação dos arquivos de dados
2. Formatação dos arquivos de dados
3. Localização dos arquivos de dados

### <a name="encoding"></a>Codificação
O PolyBase requer toobe de arquivos de dados UTF-8 ou UTF-16FE. 



### <a name="format-of-data-files"></a>Formatação dos arquivos de dados
O PolyBase exige um terminador de linha fixo de \n ou uma nova linha. Os arquivos de dados devem estar de acordo com toothis padrão. Não existem restrições quanto a terminadores de coluna ou de cadeia de caracteres.

Você terá toodefine todas as colunas no arquivo hello como parte da tabela externa no PolyBase. Certifique-se de que todas as colunas exportadas são necessárias e que tipos de saudação em conformidade com padrões toohello necessário.

Consulte novamente toohello [migrar seu esquema] artigo para obter detalhes sobre os tipos de dados com suporte.

### <a name="location-of-data-files"></a>Localização dos arquivos de dados
SQL Data Warehouse usa dados do armazenamento de BLOBs do Azure tooload exclusivamente. Consequentemente, dados saudação devem foram primeiro transferidos no armazenamento de blob.

## <a name="optimizing-data-transfer"></a>Otimizando a transferência de dados
Uma das partes de hello mais lentos de migração de dados é a transferência de saudação de saudação tooAzure de dados. Não só a largura de banda da rede pode ser um problema; a confiabilidade também pode atrapalhar seriamente o progresso. Por padrão tooAzure migração de dados é Olá internet assim Olá possibilidades de erros de transferência ocorrendo razoavelmente provavelmente. No entanto, esses erros podem exigir dados toobe enviada novamente no todo ou em parte.

Felizmente, você tem várias velocidade de saudação tooimprove opções e resiliência desse processo:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
Convém usar tooconsider [ExpressRoute] [ ExpressRoute] toospeed transferência hello. [Rota expressa] [ ExpressRoute] fornece a você com um tooAzure estabelecida conexão privada para a conexão de saudação não passa pelo Olá internet pública. Essa não é uma etapa obrigatória. No entanto, isso melhorará taxa de transferência ao enviar dados tooAzure de um local ou instalação de colocalização.

benefícios do uso de Olá [ExpressRoute] [ ExpressRoute] são:

1. Maior confiabilidade
2. Rede mais rápida
3. Menor latência da rede
4. Mais segurança de rede

[Rota expressa] [ ExpressRoute] é benéfico para diversos cenários; Olá não apenas a migração.

Interessado? Para obter mais informações e preços, visite Olá [documentação de rota expressa][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Serviço de Importação e Exportação do Azure
Hello Azure serviço de importação e exportação é um processo de transferência de dados grandes (GB + +) toomassive (TB + +) para transferências de dados no Azure. Ela envolve a gravar sua toodisks de dados e enviá-los tooan data center do Azure. conteúdo do disco Hello será carregado em Blobs de armazenamento do Azure em seu nome.

Uma visão geral do processo de exportação de importação de saudação é o seguinte:

1. Configurar um contêiner de armazenamento de BLOBs do Azure tooreceive Olá dados
2. Exportar seu armazenamento de dados toolocal
3. Copiar Olá dados too3.5 polegadas SATA II ou III unidades de disco rígido usando Olá [ferramenta de importação/exportação do Azure]
4. Criar um trabalho de importação usando hello importação do Azure e o serviço de exportação fornecer arquivos de diário Olá produzidos pelo Olá [ferramenta de importação/exportação do Azure]
5. Enviar os discos de saudação seu indicado data center do Azure
6. Seus dados são transferidos tooyour contêiner de armazenamento de BLOBs do Azure
7. Carregar dados de saudação em SQLDW usando PolyBase

### <a name="azcopyazcopy-utility"></a>Utilitário [AZCopy][AZCopy]
Olá [AZCopy][AZCopy] utilitário é uma excelente ferramenta para obter os dados transferidos para Blobs de armazenamento do Azure. Ele foi projetado para pequenos (MB + +) toovery grande (GB + +) transferências de dados. [AZCopy] também foi projetado tooprovide bom throughput resiliente quando a transferência de dados tooAzure e, portanto é uma ótima opção para a etapa de transferência de dados de saudação. Uma vez transferidos, você pode carregar dados hello usando PolyBase no SQL Data Warehouse. Também é possível incorporar o AZCopy aos seus pacotes do SSIS usando uma tarefa “Executar Processo”.

toouse AZCopy primeiro será necessário toodownload e instalá-lo. Uma [versão de produção][production version] e uma [versão prévia][preview version] estão disponíveis.

tooupload um arquivo do sistema de arquivos, que você precisará de um comando como Olá um abaixo:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Exemplo do resumo de um processo de alto nível:

1. Configurar um blob de armazenamento do Azure contêiner tooreceive Olá dados
2. Exportar seu armazenamento de dados toolocal
3. AZCopy seus dados no contêiner de armazenamento de BLOBs do Azure Olá
4. Saudação de carregar dados no SQL Data Warehouse usando PolyBase

Documentação completa disponível: [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Otimizando a exportação de dados
Além disso tooensuring que exportação hello está de acordo com requisitos de toohello dispostos pelo PolyBase você também pode pesquisar toooptimize exportação de Olá Olá tooimprove saudação do processo de dados ainda mais.



### <a name="data-compression"></a>Compactação de dados
O PolyBase pode ler dados compactados em gzip. Se você é capaz de toocompress que toogzip dos arquivos de dados, em seguida, você minimizará a quantidade de saudação de dados sendo enviados pela rede hello.

### <a name="multiple-files"></a>Vários arquivos
Dividir tabelas grandes em vários arquivos de Ajuda não só a tooimprove exportar velocidade, como também ajuda com reinicialização de transferência e Olá a capacidade de gerenciamento geral de dados Olá uma vez no armazenamento de BLOBs do Azure hello. Um dos Olá há muitos recursos de PolyBase é que ele lerá todos os arquivos de saudação dentro de uma pasta e tratá-lo como uma tabela. Portanto, é um arquivos de saudação tooisolate boa ideia para cada tabela em sua própria pasta.

O PolyBase também oferece suporte a um recurso conhecido como "passagem de pasta recursiva". Você pode usar esse recurso toofurther melhorar a organização de saudação do seu tooimprove dados exportados o gerenciamento de dados.

toolearn mais sobre o carregamento de dados com o PolyBase, consulte [Use tooload dados no SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre migração, consulte [migrar tooSQL sua solução do Data Warehouse][Migrate your solution tooSQL Data Warehouse].
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx

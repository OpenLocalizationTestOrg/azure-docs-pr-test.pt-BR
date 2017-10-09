---
title: "aaaUsing importação/exportação do Azure tootransfer dados tooand do armazenamento de blob | Microsoft Docs"
description: "Saiba como toocreate importar e exportar trabalhos no portal do Azure para transferir dados tooand do armazenamento de blob de saudação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Usar o hello importação/exportação do Microsoft Azure serviço tootransfer dados tooblob armazenamento
Olá serviço de importação/exportação do Azure permite que você toosecurely transferem grandes quantidades de armazenamento de blob tooAzure dados por envio unidades de disco rígido tooan data center do Azure. Você também pode usar esses dados de tootransfer do serviço de unidades de disco de toohard de armazenamento de BLOBs do Azure e enviar tooyour no site local. Esse serviço é adequado em situações onde você deseja tootransfer vários terabytes (TB) de tooor de dados do Azure, mas carregar ou baixar pela rede Olá inviável devido toolimited largura de banda ou alto custo de rede.

serviço de saudação requer que unidades de disco rígido deve ser criptografada para a segurança dos seus dados Olá pelo BitLocker. serviço Olá dá suporte a ambos os Olá clássico e o Azure Resource Manager armazenamento contas (camada padrão e moderada) presentes em todas as regiões de saudação do público do Azure. Você deve enviar tooone de discos rígidos locais Olá suportada especificado neste artigo.

Neste artigo, você aprenderá mais sobre o serviço de importação/exportação do Azure hello e como tooship unidades copiar tooand seus dados de armazenamento de BLOBs do Azure.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>Quando devo usar serviço de importação/exportação do Azure Olá?
Considere usar o serviço de importação/exportação do Azure ao carregar ou baixar os dados pela rede Olá está muito lenta ou a obtenção de largura de banda de rede adicionais é caro.

Você pode usar esse serviço em cenários como:

* Migrando dados na nuvem toohello: mover grandes quantidades de dados tooAzure rápida e econômica.
* A distribuição de conteúdo: enviar dados tooyour rapidamente sites de clientes.
* Backup: Faz backups do seu toostore de dados local no armazenamento de BLOBs do Azure.
* Recuperação de dados: recuperar grande quantidade de dados armazenados no armazenamento de blob e que ele seja entregue tooyour no local.

## <a name="prerequisites"></a>Pré-requisitos
Nesta seção listamos Olá pré-requisitos necessários toouse esse serviço. Examine-os cuidadosamente antes de enviar suas unidades.

### <a name="storage-account"></a>Conta de armazenamento
Você deve ter uma assinatura do Azure existente e um ou mais contas toouse Olá importação/exportação do serviço de armazenamento. Cada trabalho pode ser usado tootransfer tooor de dados de apenas uma conta de armazenamento. Em outras palavras, um único trabalho de importação/exportação não pode estender-se por várias contas de armazenamento. Para obter informações sobre como criar uma nova conta de armazenamento, consulte [como uma conta de armazenamento do tooCreate](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Tipos de blob
Você pode usar dados do serviço de importação/exportação do Azure toocopy muito**bloco** blobs ou **página** blobs. Por outro lado, você pode exportar apenas os blobs de **Bloco**, blobs de **Página** ou blobs de **Acréscimo** do armazenamento do Azure usando esse serviço.

### <a name="job"></a>Trabalho
processo de saudação do toobegin de importação tooor exportando do armazenamento de Blob, primeiro crie um trabalho. que pode ser um trabalho de importação ou um trabalho de exportação:

* Crie um trabalho de importação quando você deseja que os dados de tootransfer tiver tooblobs local em sua conta de armazenamento do Azure.
* Criar um trabalho de exportação que tootransfer dados atualmente armazenados como blobs em suas unidades de toohard de conta de armazenamento que são fornecidos tooyou.s quando você cria um trabalho, notificar Olá importação/exportação do serviço que você enviará um ou mais rígida unidades tooan do Azure Centro de dados.

* Para um trabalho de importação, você enviará discos rígidos contendo seus dados.
* Para um trabalho de exportação, você enviará discos rígidos vazios.
* Você pode enviar a unidades de disco rígido too10 por trabalho.

Você pode criar uma importação ou exportar trabalho usando Olá portal do Azure ou hello [API de REST de importação/exportação do armazenamento do Azure](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Ferramenta WAImportExport
a primeira etapa Olá na criação de um **importar** trabalho é tooprepare as unidades que serão enviadas para importação. tooprepare suas unidades, você deve conectar servidor local tooa e execução hello ferramenta WAImportExport no servidor de local de saudação. Essa ferramenta WAImportExport facilita copiar sua unidade de toohello de dados, criptografando dados Olá na unidade de saudação com BitLocker e gerando arquivos de diário de unidade de saudação.

arquivos de diário Olá armazenam informações básicas sobre o seu trabalho e a unidade, como o número de série da unidade e o nome de conta de armazenamento. Este arquivo de diário não é armazenado na unidade de saudação. Ele é usado durante a criação do trabalho de importação. Confira posteriormente neste artigo detalhes do passo a passo sobre a criação de trabalho.

ferramenta de WAImportExport Olá só é compatível com o sistema de operacional do Windows de 64 bits. Consulte Olá [sistema operacional](#operating-system) seção para versões específicas do sistema operacional com suporte.

Baixar a versão mais recente Olá de saudação [ferramenta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Para obter mais detalhes sobre como usar o hello ferramenta WAImportExport, consulte Olá [usando Olá ferramenta WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Versão anterior:** você pode [baixar WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versão do hello ferramenta e consulte muito[guia de uso WAImportExpot V1](storage-import-export-tool-how-to-v1.md). WAImportExpot V1 versão da ferramenta Olá dá suporte para **Preparando discos quando os dados já é previamente gravados disco toohello**. Também será necessário toouse WAImportExpot V1 ferramenta se Olá única chave disponível é a chave de SAS.

>

### <a name="hard-disk-drives"></a>Unidades de disco rígido
Somente 2,5 polegadas SSD ou 2,5" ou 3,5" SATA II ou III HDD de interno têm suporte para uso com o serviço de importação/exportação do hello. Um único trabalho de importação/exportação pode ter um máximo de 10 HDD/SSDs e cada HDD/SSD individual pode ter qualquer tamanho. Grande número de unidades que pode ser disseminado por vários trabalhos, e não há nenhum limite no número de saudação de trabalhos que podem ser criadas. 

Para trabalhos de importação, somente Olá primeiro volume de dados na unidade hello será processado. o volume de dados Olá deve ser formatado com NTFS.

> [!IMPORTANT]
> As unidades de disco rígido externas que vêm com um adaptador USB interno não são suportadas por esse serviço. Além disso, o disco hello dentro de saudação de maiusculas e minúsculas de um disco rígido externo não pode ser usado; Não envie HDDs externos.
> 
> 

Abaixo está que uma lista de adaptadores USB externas usada toocopy dados toointernal HDDs. Anker 68UPSATAA - 02BU Anker BU 68UPSHHDS Startech SATADOCK22UE Orico 6628SUS3-C-BK (série 6628) Estação dock da unidade de disco rígido externa SATA BlacX Hot Swap Thermaltake (USB 2.0 e eSATA)

### <a name="encryption"></a>Criptografia
dados de saudação na unidade Olá devem ser criptografados usando a criptografia de unidade de disco BitLocker. Isso protegerá os dados enquanto eles estiverem em trânsito.

Para trabalhos de importação, há dois criptografia de saudação do tooperform maneiras. Olá primeiro modo é a opção de saudação de toospecify ao usar o arquivo CSV de conjunto de dados ao executar a ferramenta WAImportExport de saudação durante a preparação de unidade. Hello segunda maneira é a criptografia de BitLocker tooenable manualmente na unidade de saudação e especificar chave de criptografia de saudação em Olá driveset CSV ao executar a linha de comando WAImportExport ferramenta durante a preparação de unidade.

Para trabalhos de exportação, depois que os dados forem copiados toohello unidades, serviço Olá criptografará unidade hello usando o BitLocker antes da entrega tooyou voltar. chave de criptografia Hello será fornecida tooyou via Olá portal do Azure.  

### <a name="operating-system"></a>Sistema operacional
Você pode usar uma saudação 64-bit sistemas operacionais tooprepare Olá no disco rígido usando Olá ferramenta WAImportExport antes do envio de saudação unidade tooAzure a seguir:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Todos esses sistemas operacionais dão suporte à Criptografia de Unidade de Disco BitLocker.

### <a name="locations"></a>Locais
Olá serviço de importação/exportação do Azure dá suporte à cópia tooand de dados de todas as contas de armazenamento do Azure públicos. Você pode enviar unidades de disco rígido tooone de saudação locais a seguir. Se sua conta de armazenamento está em um local do Azure público que não é especificado aqui, um local alternativo de remessa será fornecido quando você estiver criando Olá trabalho usando Olá portal do Azure ou Olá API de REST de importação/exportação.

Locais de envio com suporte:

* Leste dos EUA
* Oeste dos EUA
* Leste dos EUA 2
* Oeste dos EUA 2
* Centro dos EUA
* Centro-Norte dos EUA
* Centro-Sul dos Estados Unidos
* Centro-Oeste dos EUA
* Norte da Europa
* Europa Ocidental
* Ásia Oriental
* Sudeste Asiático
* Leste da Austrália
* Sudeste da Austrália
* Oeste do Japão
* Leste do Japão
* Índia Central
* Sul da Índia
* Índia Ocidental
* Canadá Central
* Leste do Canadá
* Sul do Brasil
* Coreia Central
* Gov. dos EUA – Virgínia
* Gov do Iowa nos EUA
* DoD do Leste dos EUA
* DoD Central dos EUA
* Leste da China
* Norte da China
* Sul do Reino Unido

### <a name="shipping"></a>Remessa
**Envio de unidades toohello Datacenter:**

Ao criar um trabalho de importação ou exportação, você receberá que um endereço de envio de uma saudação suporte locais tooship suas unidades. Olá endereço de remessa fornecido dependerá de local de saudação de sua conta de armazenamento, mas pode não ser Olá mesmo como o local de conta de armazenamento.

Você pode usar as operadoras móveis como FedEx, DHL, no-break ou Olá serviço Postal tooship seu toohello unidades endereço de entrega.

**Unidades de envio do Centro de dados hello:**

Ao criar um trabalho de importação ou exportação, forneça um endereço de retorno para Microsoft toouse quando envio unidades de saudação fazer depois que o trabalho seja concluído. Verifique se que você fornecer um endereço de retorno válido tooavoid atrasos no processamento.

Você pode usar uma operadora de sua escolha no disco rígido de saudação de remessa do pedido tooforward. operadora Olá deve ter o controle apropriado no grupo de toomaintain ordens de custódia. Você também deve fornecer uma operadora FedEx ou DHL válida toobe número de conta usada pela Microsoft para envio Olá unidades novamente. Um número de conta FedEx é necessário para enviar as unidades da saudação dos EUA e locais na Europa. Um número de conta DHL é necessário para enviar de volta as unidades de locais na Ásia e na Austrália. Você poderá criar uma conta da carrier [FedEx](http://www.fedex.com/us/oadr/) (para os EUA e a Europa) ou [DHL](http://www.dhl.com/) (Ásia e Austrália) se não tiver uma. Se você já tiver um número de conta da transportadora, verifique se ele é válido.

No envio de pacotes, você deve seguir os termos Olá [termos de serviço do Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Observe que a mídia física de saudação que são fornecidos pode precisar fronteiras internacionais toocross. Você é responsável por garantir que a mídia física e os dados são importados e/ou exportados de acordo com as leis aplicáveis Olá. Antes do envio de mídia física hello, verifique com seu tooverify supervisores seus dados e mídia legalmente podem ser fornecido toohello identificado Datacenter. Isso ajudará tooensure atingir Microsoft de maneira oportuna. Por exemplo, qualquer pacote que será entre fronteiras internacionais precisa de um toobe fatura comercial acompanhado de pacote de saudação (exceto se Cruzando bordas dentro da União Europeia). Você pode imprimir uma cópia preenchida da fatura comercial de saudação do site da operadora. Alguns exemplos de fatura comercial são a [Fatura comercial da DHL](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) e a [Fatura comercial da FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Certifique-se de que a Microsoft não foi indicada como exportador de saudação.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>Como funciona a saudação serviço de importação/exportação do Azure?
Você pode transferir dados entre o site local e o armazenamento de BLOBs do Azure usando o serviço de importação/exportação do Azure Olá Criando trabalhos e envio de unidades de disco rígido tooan data center do Azure. Cada unidade de disco rígido que você enviar estará associada a um único trabalho. Cada trabalho é associado uma única conta de armazenamento. Saudação de revisão [seção pré-requisitos](#pre-requisites) cuidadosamente toolearn sobre especificações Olá esse tipos de blob do serviço, como suporte para tipos de disco, locais e envio.

Nesta seção, vamos descrevem em uma saudação de nível alto passos para importar e exportar trabalhos. Olá posteriormente [início rápido da seção](#quick-start), fornecem instruções passo a passo toocreate uma importação e trabalho de exportação.

### <a name="inside-an-import-job"></a>Dentro de um trabalho de importação
Em um nível alto, um trabalho de importação envolve Olá etapas a seguir:

* Determinar Olá toobe de dados importado e Olá o número de unidades que será necessário.
* Identificar o local de blob de destino Olá para seus dados no armazenamento de Blob.
* Use Olá ferramenta WAImportExport toocopy tooone seus dados ou mais unidades de disco rígido e criptografá-los com o BitLocker.
* Criar um trabalho de importação na sua conta de armazenamento de destino usando o portal do Azure de saudação ou Olá API de REST de importação/exportação. Se usar Olá portal do Azure, carregar arquivos de diário de unidade hello.
* Forneça o endereço de retorno hello e toobe número de conta da operadora usada para envio Olá unidades back tooyou.
* Unidades de disco rígido de Olá de remessa toohello endereço fornecido durante a criação do trabalho de envio.
* Atualizar entrega Olá número em detalhes do trabalho de importação de saudação de controle e enviar o trabalho de importação de saudação.
* Unidades são recebidas e processadas no hello data center do Azure.
* Unidades são enviadas usando o transporte conta toohello endereço do remetente fornecido no trabalho de importação de saudação.
  
    ![Figura 1: Importar o fluxo de trabalho](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Dentro de um trabalho de exportação
Em um nível alto, um trabalho de exportação envolve Olá etapas a seguir:

* Determine Olá dados toobe exportado e Olá o número de unidades que será necessário.
* Identificar os blobs de origem hello ou caminhos do contêiner de seus dados no armazenamento de Blob.
* Criar um trabalho de exportação na conta de armazenamento usando o portal do Azure de saudação ou Olá API de REST de importação/exportação.
* Especifique Olá blobs de origem ou o trabalho de exportação de caminhos do contêiner de seus dados em hello.
* Forneça Olá retorno endereço e operadora número da conta para toobe usada para envio Olá unidades back tooyou.
* Unidades de disco rígido de Olá de remessa toohello endereço fornecido durante a criação do trabalho de envio.
* Atualizar entrega Olá número em detalhes do trabalho de exportação de saudação de controle e enviar o trabalho de exportação de saudação.
* Olá unidades são recebidas e processadas no hello data center do Azure.
* Olá unidades estão criptografadas com BitLocker; chaves de saudação estão disponíveis via Olá portal do Azure.  
* unidades de saudação são enviadas usando o transporte conta toohello endereço do remetente fornecido no trabalho de importação de saudação.
  
    ![Figura 2: Exportar o fluxo de trabalho](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Exibir o status do trabalho e da unidade
Você pode acompanhar o status de saudação de importação ou trabalhos de exportação de saudação portal do Azure. Clique em Olá **importação/exportação** guia. Na página hello, será exibida uma lista de seus trabalhos.

![Exibir o estado do trabalho](./media/storage-import-export-service/jobstate.png)

Você verá um Olá status dependendo de onde a unidade está no processo de saudação do trabalho a seguir.

| Status do Trabalho | Descrição |
|:--- |:--- |
| Criando | Depois que um trabalho é criado, seu estado é definido tooCreating. Enquanto o trabalho de saudação está em Olá criando estado, hello serviço de importação/exportação supõe Olá unidades não foram enviadas toohello Datacenter. Um trabalho pode permanecer no estado de criação de Olá para backup tootwo semanas, após o qual ele é excluído automaticamente pelo serviço de saudação. |
| Remessa | Depois que você enviar seu pacote, você deve atualizar Olá informações no portal do Azure de saudação do controle.  Isso tornará o trabalho Olá em "Envio". trabalho de saudação permanecerá no estado de envio Olá para backup tootwo semanas. 
| Recebido | Depois que todas as unidades tiverem sido recebidas no data center de hello, estado do trabalho Olá será definido toohello recebidos. |
| Transferindo | Quando pelo menos uma unidade tiver iniciado o processamento, o estado do trabalho Olá será definido toohello transferir. Consulte os estados da unidade Olá seção abaixo para obter informações detalhadas. |
| Empacotamento | Depois que todas as unidades tiverem concluído o processamento, Olá trabalho será colocado no estado de empacotamento Olá até Olá unidades tooyou back fornecido. |
| Concluído | Depois que todas as unidades foram enviadas toohello back cliente, se Olá trabalho foi concluído sem erros, em seguida, Olá trabalho será definido toohello estado concluído. trabalho Hello será excluído automaticamente depois de 90 dias no hello estado concluído. |
| Fechado | Depois que todas as unidades foram enviadas toohello back cliente, se houve erros durante o processamento de saudação do trabalho de saudação, em seguida, Olá trabalho será definido estado fechado toohello. trabalho Hello será excluído automaticamente após 90 dias em um estado fechado hello. |

Olá tabela a seguir descreve Olá ciclo de vida de uma unidade individual, como ela passa por um trabalho de importação ou exportação. estado atual de saudação de cada unidade em um trabalho agora está visível da saudação portal do Azure.
Olá tabela a seguir descreve cada estado de cada unidade em um trabalho pode passar.

| Estado da unidade | Descrição |
|:--- |:--- |
| Especificado | Para um trabalho de importação, quando o trabalho de saudação é criado da saudação portal do Azure, saudação inicial para uma unidade é Olá especificado estado. Para um trabalho de exportação, desde que nenhuma unidade foi especificada quando o trabalho de saudação é criado, saudação inicial de unidade é Olá recebidos estado. |
| Recebido | unidade Olá faz a transição de estado recebido de toohello quando o operador do serviço de importação/exportação Olá processou unidades Olá recebidas do hello envio da empresa para um trabalho de importação. Para um trabalho de exportação, saudação inicial de unidade é Olá recebidos estado. |
| Nunca recebido | unidade de saudação moverá toohello NeverReceived estado quando chega do pacote de saudação para um trabalho, mas pacote hello não contém a unidade de saudação. Uma unidade também pode mover esse estado se foram duas semanas desde que o serviço de saudação recebeu informações de envio de saudação, mas o pacote hello ainda não tiver chegado no data center de saudação. |
| Transferindo | Uma unidade moverá toohello transferindo estado quando o serviço Olá começa tootransfer dados Olá unidade tooWindows armazenamento do Azure. |
| Concluído | Uma unidade moverá toohello estado concluído quando o serviço de saudação tiver transferido com êxito todos os dados de saudação sem erros.
| Concluído mais informações | Uma unidade moverá toohello CompletedMoreInfo estado quando o serviço Olá encontrou alguns problemas ao copiar dados de ou unidade de toohello. informações de saudação podem incluir erros, avisos ou mensagens informativas sobre substituição de blobs.
| Enviado de volta | unidade de saudação moverá toohello ShippedBack estado quando ela foi enviada do endereço do remetente de toohello Olá data center de volta. |

Esta imagem de saudação portal do Azure exibe o estado de unidade de saudação de um trabalho de exemplo:

![Exibir estado da unidade](./media/storage-import-export-service/drivestate.png)

Olá tabela a seguir descreve Olá estados de falha de unidade e Olá ações executadas para cada estado.

| Estado da unidade | Evento | Resolução/Próxima etapa |
|:--- |:--- |:--- |
| Nunca recebido | Uma unidade que está marcada como NeverReceived (porque ela não foi recebida como parte da remessa do trabalho Olá) chega em outra remessa. | equipe de operações de saudação moverá Olá unidade toohello estado recebido. |
| N/D | Uma unidade que não faz parte de qualquer trabalho chega no data center de saudação como parte de outro trabalho. | unidade de saudação será marcada como uma unidade adicional e será retornada toohello cliente quando Olá trabalho associado com o pacote original Olá estiver concluído. |

### <a name="time-tooprocess-job"></a>Trabalho de tempo de tooprocess
Olá quantidade de tempo-tooprocess varia de acordo com um trabalho de importação/exportação com diferentes fatores, como a hora de envio, tipo de trabalho, digite e tamanho de Olá dados sendo copiados e Olá tamanho dos discos Olá fornecido. Olá serviço de importação/exportação não tem um SLA, mas depois de discos Olá recebidos serviço Olá se esforça toocomplete Olá cópia em 7 dias too10. Você pode usar o andamento do trabalho Olá API REST tootrack hello mais de perto. Olá operação listar trabalhos que fornece uma indicação do andamento da cópia é um parâmetro de conclusão percentual. Contato toous se você precisar de um toocomplete de estimativa de um trabalho de importação/exportação crítico de tempo.

### <a name="pricing"></a>Preços
**Taxa de manuseio de unidade**

Há uma taxa de manuseio de unidade para cada unidade processada como parte do trabalho de importação ou exportação. Veja detalhes de saudação sobre Olá [preços de importação/exportação do Azure](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Custos de envio**

Quando você enviar unidades tooAzure, você paga Olá transportadora de toohello custo de remessa. Quando a Microsoft retorna Olá unidades tooyou, Olá custo de remessa será cobrado toohello conta da transportadora que é fornecido no momento da saudação de criação de trabalho.

**Custos de transação**

Não há nenhum custo de transação ao importar dados para o armazenamento de blobs. encargos de saída padrão de saudação são aplicáveis quando dados são exportados do armazenamento de blob. Para obter mais detalhes sobre os custos da transação, consulte [Preços de transferência de dados.](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Início rápido
Nesta seção, fornecemos instruções passo a passo para criar um trabalho de importação e exportação. Verifique se você atende a todos os Olá [pré-requisitos](#pre-requisites) antes de continuar.

> [!IMPORTANT]
> serviço Olá dá suporte a uma conta de armazenamento padrão por importar ou exportar trabalho e não oferece suporte a contas de armazenamento premium. 
> 
> 
## <a name="create-an-import-job"></a>Criar um trabalho de importação
Crie uma importação trabalho toocopy dados tooyour conta de armazenamento do Azure do disco rígido pelo envio de uma ou mais unidades que contêm dados toohello especificado Datacenter. trabalho de importação Hello transmite os detalhes sobre unidades de disco rígido, toobe dados copiados, conta de armazenamento de destino e o serviço de importação/exportação do Azure toohello informações de envio. A criação de um trabalho de importação é um processo de três etapas. Primeiro, prepare suas unidades usando a ferramenta WAImportExport de saudação. Em seguida, envie um trabalho de importação usando Olá portal do Azure. Em terceiro lugar, envie Olá unidades toohello endereço fornecido durante a saudação de criação e atualização de trabalho enviando informações em seus detalhes do trabalho de envio.   

### <a name="prepare-your-drives"></a>Preparar suas unidades
Olá primeira etapa ao importar dados usando o serviço de importação/exportação do Azure Olá é tooprepare suas unidades usando a ferramenta WAImportExport de saudação. Siga as etapas de saudação abaixo tooprepare suas unidades.

1. Identifica Olá toobe de dados importado. Isso pode ser diretórios e arquivos autônomos no servidor local hello ou um compartilhamento de rede.  
2. Determine o número de saudação de unidades que você precisará dependendo do tamanho total dos dados de saudação. Adquira unidades de disco rígido SATA II ou III de número Olá necessário de 2,5 polegadas SSD ou 2,5" ou 3,5".
3. Identifica a conta de armazenamento de destino hello, contêiner, diretórios virtuais e blobs.
4.  Determine os diretórios hello e/ou arquivos independentes que serão copiados tooeach do disco rígido.
5.  Crie hello arquivos CSV para o conjunto de dados e driveset.
    
    **Arquivo CSV do conjunto de dados**
    
    Veja abaixo um exemplo de arquivo CSV de conjunto de dados:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    Olá, o exemplo acima, 100M_1.csv.txt será copiado toohello raiz do contêiner Olá denominado "containername". Se o nome de contêiner de hello "containername" não existe, um será criado. Todos os arquivos e pastas em 50M_original será toocontainername recursivamente copiado. A estrutura de pastas será mantida.

    Saiba mais sobre [Preparando Olá conjunto de dados CSV arquivo](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Lembre-se de**: por padrão, os dados hello serão importados como Blobs de blocos. Você pode usar dados de valor do campo tooimport BlobType hello como os Blobs de página. Por exemplo, se você estiver importando arquivos VHD que serão montados como discos em uma VM do Azure, deverá importá-los como Blobs de Página.

    **Arquivo CSV driveset**

    valor Olá Olá driveset sinalizador é um arquivo CSV que contém a lista de saudação discos toowhich Olá de letras de unidade são mapeados para que Olá ferramenta toocorrectly selecione lista de saudação de discos toobe preparado. 

    Abaixo está o exemplo hello do arquivo CSV de driveset:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    Olá, o exemplo acima, presume-se que dois discos anexados e volumes NTFS básicos com letra de volume G:\ e H:\ foram criados. Olá ferramenta Formatar e criptografar o disco Olá que hospeda H:\ e não formatar ou criptografar o disco Olá volume G:\ de hospedagem.

    Saiba mais sobre [Preparando o arquivo CSV Olá driveset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Saudação de uso [ferramenta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy tooone seus dados ou mais discos rígidos.
7.  Você pode especificar "Criptografar" no campo de criptografia de drivset CSV tooenable de disco BitLocker na unidade de disco rígido hello. Como alternativa, pode também habilitar a criptografia BitLocker manualmente na unidade de disco rígido hello e especificar "AlreadyEncrypted" e fornecer chave Olá Olá driveset CSV durante a execução da ferramenta de saudação.

8. Não modifique dados Olá Olá com discos rígidos ou arquivo de diário Olá depois de concluir a preparação do disco.

> [!IMPORTANT]
> Cada unidade de disco rígido preparada resultará em um arquivo de diário. Quando você estiver criando um trabalho de importação hello usando Olá portal do Azure, você deve carregar todos os arquivos de diário de saudação de unidades de saudação que fazem parte do trabalho de importação. Unidades sem arquivos de diário não serão processadas.
> 
>

A seguir são comandos hello e exemplos para preparar a unidade de disco rígido hello usando ferramenta WAImportExport.

A ferramenta WAImportExport comando PrepImport para Olá primeiro copiar diretórios toocopy de sessão e/ou arquivos com uma nova sessão de cópia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Exemplo de importação 1**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

Em ordem muito**adicionar mais unidades**, um pode criar um novo arquivo driveset e execute o comando hello como abaixo. Para cópia subsequentes sessões toohello diferentes unidades de disco que foi especificado no arquivo. csv de InitialDriveset, especifique um novo arquivo CSV driveset e fornecê-la como um parâmetro toohello "AdditionalDriveSet". Saudação de uso **mesmo arquivo de diário** nome e fornecer um **nova ID de sessão**. formato de saudação do arquivo CSV AdditionalDriveset é igual ao formato InitialDriveSet.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Exemplo de importação 2**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

Em ordem tooadd dados adicionais toohello driveset mesmo, a ferramenta WAImportExport PrepImport comando pode ser chamada para cópia subsequentes sessões toocopy adicionais/diretório de arquivos: de cópia subsequentes sessões toohello mesmo disco rígido unidades especificada no . InitialDriveset CSV especificar Olá **mesmo arquivo de diário** nomear e fornecer um **nova ID de sessão**; não há nenhuma chave de conta de armazenamento do necessidade tooprovide Olá.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Exemplo de importação 3**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Veja mais detalhes sobre como usar a ferramenta WAImportExport Olá [Preparando discos rígidos para importação](storage-import-export-tool-preparing-hard-drives-import.md).

Além disso, consulte toohello [unidades de disco rígido de tooprepare do fluxo de trabalho para um trabalho de importação de exemplo](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) para obter mais instruções passo a passo.  

### <a name="create-hello-import-job"></a>Criar trabalho de importação de saudação
1. Depois de preparar a unidade, navegar tooyour conta de armazenamento Olá portal do Azure e exibir hello painel. Em **Visão Rápida**, clique em **Criar um Trabalho de Importação**. Examine as etapas de saudação e selecione Olá tooindicate de caixa de seleção que você preparou sua unidade e se você tem o arquivo de diário de unidade de saudação disponível.
2. Na etapa 1, fornece informações de contato Olá pessoa responsável por esse trabalho de importação e um endereço de retorno válido. Se você quiser toosave dados de log detalhado para o trabalho de importação hello, verificar opção Olá muito**Olá de Salvar log detalhado no meu contêiner de blob 'waimportexport'**.
3. Na etapa 2, carregar arquivos de diário de unidade Olá obtido durante a etapa de preparação de unidade hello. Você precisará de um arquivo de tooupload para cada unidade que você preparou.
   
   ![Criar o trabalho de importação - Etapa 3](./media/storage-import-export-service/import-job-03.png)
4. Na etapa 3, insira um nome descritivo para o trabalho de importação de saudação. Observe que nome hello inserido pode conter apenas letras minúsculas, números, hifens e sublinhados e deve começar com uma letra e não pode conter espaços. Você usará o nome hello escolhido tootrack seus trabalhos enquanto eles estão em andamento e depois que eles forem concluídos.
   
   Em seguida, selecione sua região do data center na lista de saudação. Olá região do data center indica dados saudação center e endereço toowhich, você deve enviar seu pacote. Consulte as perguntas Frequentes Olá abaixo para obter mais informações.
5. Na etapa 4, selecione a operadora de retorno na lista de saudação e insira seu número de conta da operadora. A Microsoft usará essa conta tooship Olá unidades back tooyou depois que o trabalho de importação for concluído.
   
   Se você tiver o número de controle, selecione a operadora de entrega da lista de saudação e insira o número de controle.
   
   Se você não tem um controle de número ainda, escolha **fornecerei minhas informações de envio para este trabalho de importação após ter enviado meu pacote**, em seguida, concluir o processo de importação de saudação.
6. tooenter o número de controle depois de ter enviado o pacote, retornar toohello **importação/exportação** página para sua conta de armazenamento Olá portal do Azure, selecione o trabalho na lista de saudação e escolha **informações de envio**. Navegar pelo Assistente de saudação e insira o número de controle na etapa 2.
   
    Se Olá número de controle não for atualizada dentro de duas semanas de criação de trabalho hello, trabalho Olá expirará.
   
    Se o trabalho hello está em estado de criação, envio ou transferir de Olá, você também pode atualizar seu número de conta da operadora na etapa 2 do Assistente de saudação. Depois que o trabalho de saudação está em estado de empacotamento de Olá, você não pode atualizar seu número de conta da operadora para esse trabalho.
7. Você pode acompanhar o andamento do trabalho no painel do portal hello. Veja o que significa que cada estado do trabalho na seção anterior Olá por [exibindo o status do trabalho](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Criar um trabalho de exportação
Crie uma saudação de toonotify de trabalho de exportação serviço de importação/exportação que você enviará um ou mais discos vazios toohello Datacenter para que os dados podem ser exportados de suas unidades de toohello de conta de armazenamento e unidades de saudação enviados tooyou.

### <a name="prepare-your-drives"></a>Preparar suas unidades
As pré-verificações a seguir são recomendadas para preparar suas unidades para um trabalho de exportação:

1. Verifique o número de saudação de discos necessário usando o comando de PreviewExport da ferramenta do hello WAImportExport. Para obter mais informações, consulte [Visualizando o uso da unidade para um trabalho de exportação](https://msdn.microsoft.com/library/azure/dn722414.aspx). Ajuda a visualizar o uso da unidade para blobs Olá selecionados, com base no tamanho Olá Olá unidades que serão toouse.
2. Verifique se você pode leitura/gravação toohello disco rígido que será enviado para o trabalho de exportação hello.

### <a name="create-hello-export-job"></a>Criar trabalho de exportação de saudação
1. toocreate um trabalho de exportação, navegue tooyour conta de armazenamento Olá portal do Azure e exibir hello painel. Em **rápidos**, clique em **criar um trabalho de exportação** e prossiga com o Assistente de saudação.
2. Na etapa 2, fornece informações de contato Olá pessoa responsável por este trabalho de exportação. Se você quiser toosave dados de log detalhado para o trabalho de exportação hello, verificar opção Olá muito**Olá de Salvar log detalhado no meu contêiner de blob 'waimportexport'**.
3. Na etapa 3, especifique quais blob de dados que você deseja tooexport da sua conta de armazenamento tooyour espaço em branco da unidade ou unidades. Você pode escolher tooexport todos os dados de blob na conta de armazenamento hello, ou você pode especificar que os blobs ou conjuntos de tooexport de blobs.
   
   toospecify tooexport um blob, use Olá **igual a** seletor e especificar o blob toohello caminho relativo do hello, começando com o nome do contêiner de saudação. Use *$root* toospecify contêiner de raiz de saudação.
   
   toospecify todos os blobs começando com um prefixo, use Olá **começa com** seletor e especifique o prefixo hello, começando com uma barra '/'. prefixo de saudação pode ser o prefixo de saudação do nome do contêiner Olá, nome de recipiente completo hello ou nome de recipiente completo Olá seguido por prefixo de saudação do nome de blob de saudação.
   
   Olá, a tabela a seguir mostra exemplos de caminhos de blob válidos:
   
   | Seletor | Caminho do Blob | Descrição |
   | --- | --- | --- |
   | Começa com |/ |Exporta todos os blobs na conta de armazenamento Olá |
   | Começa com |/$root/ |Exporta todos os blobs no contêiner raiz de saudação |
   | Começa com |/book |Exporta todos os blobs em qualquer contêiner que comece com o prefixo **book** |
   | Começa com |/music/ |Exporta todos os blobs no contêiner **music** |
   | Começa com |/music/love |Exporta todos os blobs no contêiner **music** que comecem com o prefixo **love** |
   | Igual muito|$root/logo.bmp |Blob de exportações **logo.bmp** no contêiner raiz de saudação |
   | Igual muito|videos/story.mp4 |Exporta o blob **story.mp4** no contêiner **videos** |
   
   Forneça caminhos de blob de saudação em formatos válidos tooavoid erros durante o processamento, conforme mostrado nesta captura de tela.
   
   ![Criar o trabalho de exportação - Etapa 3](./media/storage-import-export-service/export-job-03.png)
4. Na etapa 4, digite um nome descritivo para o trabalho de exportação de saudação. nome de saudação pode conter apenas letras minúsculas, números, hifens e sublinhados e deve começar com uma letra e não pode conter espaços.
   
   Olá região do data center indicará Olá data center toowhich deve enviar seu pacote. Consulte as perguntas Frequentes Olá abaixo para obter mais informações.
5. Na etapa 5, selecione a operadora de retorno na lista de saudação e insira seu número de conta da operadora. A Microsoft usará essa conta tooship suas unidades fazer tooyou depois que o trabalho de exportação for concluído.
   
   Se você tiver o número de controle, selecione a operadora de entrega da lista de saudação e insira o número de controle.
   
   Se você não tem um controle de número ainda, escolha **fornecerei minhas informações de envio para este trabalho de exportação após ter enviado meu pacote**, conclua o processo de exportação hello.
6. tooenter o número de controle depois de ter enviado o pacote, retornar toohello **importação/exportação** página para sua conta de armazenamento Olá portal do Azure, selecione o trabalho na lista de saudação e escolha **informações de envio**. Navegar pelo Assistente de saudação e insira o número de controle na etapa 2.
   
    Se Olá número de controle não for atualizada dentro de duas semanas de criação de trabalho hello, trabalho Olá expirará.
   
    Se o trabalho hello está em estado de criação, envio ou transferir de Olá, você também pode atualizar seu número de conta da operadora na etapa 2 do Assistente de saudação. Depois que o trabalho de saudação está em estado de empacotamento de Olá, você não pode atualizar seu número de conta da operadora para esse trabalho.
   
   > [!NOTE]
   > Se Olá blob toobe exportado está em uso no tempo de saudação de cópia de unidade toohard, serviço de importação/exportação do Azure terá um instantâneo de Olá blob e cópia Olá instantâneos.
   > 
   > 
7. Você pode acompanhar o andamento do trabalho no painel de saudação do hello portal do Azure. Veja o que significa que cada estado do trabalho na seção anterior Olá em "exibindo o status do trabalho".
8. Depois de receber Olá unidades com os dados exportados, você pode exibir e copiar chaves do BitLocker Olá geradas pelo serviço Olá para unidade de disco. Navegue tooyour conta de armazenamento no portal do Azure de saudação e guia de importação/exportação do Olá. Selecione o trabalho de exportação da lista de saudação e botão Exibir chaves de saudação. chaves do BitLocker Olá aparecem como mostrado abaixo:
   
   ![Exibir chaves do BitLocker para um trabalho de exportação](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Vá por meio da seção de perguntas Frequentes de saudação abaixo conforme ele abrange as perguntas mais comuns hello, os clientes encontram ao usar este serviço.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

**Armazenamento de arquivo do Azure usando o serviço de importação/exportação do Azure de saudação pode copiar?**

Não, Olá serviço de importação/exportação do Azure suporta apenas Blobs de blocos e Blobs de página. Não há suporte para todos os outros tipos de armazenamento, incluindo o armazenamento de Arquivos do Azure, o Armazenamento de Tabelas e o Armazenamento de Filas.

**Serviço de importação/exportação do Azure hello está disponível para assinaturas de CSP?**

Não, o serviço de Importação/Exportação do Azure não dá suporte a assinaturas de CSP.

**Pode ignorar a etapa de preparação de unidade do Olá para um trabalho de importação ou me preparar uma unidade sem copiar?**

Qualquer unidade que você deseja tooship de importação de dados deve estar preparada usando hello Azure WAImportExport ferramenta. Você deve usar a unidade de toohello Olá WAImportExport ferramenta toocopy dados.

**É necessário tooperform qualquer preparação do disco durante a criação de um trabalho de exportação?**

Não, mas algumas pré-verificações são recomendadas. Verifique o número de saudação de discos necessário usando o comando de PreviewExport da ferramenta do hello WAImportExport. Para obter mais informações, consulte [Visualizando o uso da unidade para um trabalho de exportação](https://msdn.microsoft.com/library/azure/dn722414.aspx). Ajuda a visualizar o uso da unidade para blobs Olá selecionados, com base no tamanho Olá Olá unidades que serão toouse. Também verifique se é possível ler e gravação toohello disco rígido que será enviado para Olá trabalho de exportação.

**O que acontece se enviar uma unidade de disco rígido que não está de acordo com toohello acidentalmente requisitos com suporte?**

Olá data center do Azure retornará unidade Olá que não está de acordo com tooyou de requisitos de toohello com suporte. Se apenas algumas das unidades de saudação no pacote de saudação atende aos requisitos de suporte de Olá, essas unidades serão processadas e unidades de saudação que não atendem aos requisitos de saudação retornará tooyou.

**Posso cancelar meu trabalho?**

Você pode cancelar um trabalho quando seu status for Criando ou Enviando.

**Quanto tempo pode exibir status de saudação de trabalhos concluídos em Olá portal do Azure?**

Você pode exibir o status de saudação dos trabalhos concluídos para backup too90 dias. Os trabalhos concluídos serão excluídos após 90 dias.

**Se eu quiser tooimport ou exportar mais de 10 unidades, o que devo fazer?**

Uma importação ou trabalho de exportação pode fazer referência apenas 10 unidades em um único trabalho para o serviço de importação/exportação de saudação. Se você quiser tooship mais de 10 unidades, você pode criar vários trabalhos. Unidades que estão associadas a saudação mesmo trabalho deve ser enviado juntos em Olá mesmo pacote.
A Microsoft oferece orientações e assistência quando a capacidade dos dados se estender por vários trabalhos de importação de disco. Entre em contato com bulkimport@microsoft.com para saber mais

**Olá unidades de saudação do formato de serviço antes de retorná-los?**

Não. Todas as unidades são criptografadas com o BitLocker.

**Pode adquirir unidades para os trabalhos de importação/exportação da Microsoft?**

Não. Você precisará tooship suas próprias unidades tanto para importar e exportar trabalhos.

**Como fazer para acessar dados importados por este serviço**

dados de saudação em sua conta de armazenamento do Azure podem ser acessados via Olá Portal do Azure ou usando uma ferramenta autônoma chamado Gerenciador de armazenamento. https://docs.microsoft.com/pt-br/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Após a conclusão do trabalho de importação hello, o que meu dados como ficará na conta de armazenamento Olá? A hierarquia de diretório será preservada?**

Ao preparar um disco rígido para um trabalho de importação, o destino de saudação é especificado pelo campo de DstBlobPathOrPrefix Olá no conjunto de dados CSV. Este é o contêiner de destino de saudação em toowhich de conta de armazenamento Olá dados do disco rígido Olá são copiados. Nesse contêiner de destino, os diretórios virtuais são criados para pastas de disco rígido hello e blobs são criados para arquivos. 

**Se a unidade de saudação tiver arquivos que já existem na minha conta de armazenamento, serviço Olá substituirá blobs existentes em minha conta de armazenamento?**

Ao preparar a unidade Olá, você pode especificar se os arquivos de destino Olá devem ser substituídos ou ignorados usando o campo de saudação no arquivo CSV de conjunto de dados chamado disposição: < renomear | substituir nenhum | substituir >. Por padrão, Olá serviço será renomear novos arquivos de saudação em vez de substituir os blobs existentes.

**Olá WAImportExport ferramenta é compatível com sistemas operacionais de 32 bits?**
Não. ferramenta de WAImportExport Olá só é compatível com sistemas de operacionais do Windows de 64 bits. Consulte a seção de sistemas operacionais toohello Olá [pré-requisitos](#pre-requisites) para obter uma lista completa de versões com suporte do sistema operacional.

**Devo incluir algo diferente de saudação do disco rígido no meu pacote?**

Envie somente seus discos rígidos. Não inclua itens como cabos de alimentação ou cabos USB.

**É necessário tooship meus discos usando FedEx ou DHL?**

Você pode enviar unidades toohello data center usando qualquer operadora conhecida como FedEx, DHL, no-break ou serviço Postal. No entanto, para envio Olá unidades back tooyou do Centro de dados hello, você deve fornecer um número de conta FedEx em Olá EUA e, ou um número de conta DHL em hello Ásia e regiões Austrália.

**Há restrições quanto ao envio de minha unidade internacionalmente?**

Observe que a mídia física de saudação que são fornecidos pode precisar fronteiras internacionais toocross. Você é responsável por garantir que a mídia física e os dados são importados e/ou exportados de acordo com as leis aplicáveis Olá. Antes do envio de mídia física hello, verifique com seu tooverify supervisores seus dados e mídia legalmente podem ser fornecido toohello identificado Datacenter. Isso ajudará tooensure atingir Microsoft de maneira oportuna.

**Ao criar um trabalho, Olá endereço de entrega é um local diferente do meu local da conta de armazenamento. O que devo fazer?**

Alguns locais de conta de armazenamento são mapeada tooalternate locais de envio. Anteriormente, locais de envio disponível também podem ser temporariamente mapeada tooalternate locais. Sempre verifique Olá endereço de remessa fornecido durante a criação de trabalho antes de enviar suas unidades.

**Ao enviar a unidade, solicita operadora Olá Olá data center contato endereço e número de telefone. O que devo fornecer?**

Olá, número de telefone e o controlador de domínio de endereço é fornecido como parte da criação de trabalho.

**É possível usar caixas de correio do hello importação/exportação do Azure serviço toocopy PST e tooO365 de dados do SharePoint?**

Consulte também[arquivos PST de importação ou tooOffice de dados do SharePoint 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**É possível usar toocopy de serviço de importação/exportação do Azure Olá meu toohello offline de backups Azure Backup Service?**

Consulte também[fluxo de trabalho de Backup Offline no Backup do Azure](../../backup/backup-azure-backup-import-export.md).

**O que é números máximos de saudação de HDD para em uma única remessa?**

Pode ser qualquer número de unidades de disco rígido em uma única remessa e se discos Olá pertencem toomultiple trabalhos recomenda muito um) tem discos Olá rotulados com nomes de trabalho correspondente hello. b) trabalhos de saudação de atualização com um número de controle -1, o sufixo-2 etc.
  
**O que é hello máximo Blob de blocos e o tamanho de Blob de página com suporte pela importação/exportação do disco?**

O tamanho máximo de Blob de Blocos é de aproximadamente 4,768 TB ou 5.000.000 MB.
O tamanho máximo de Blob de Páginas é de 1 TB.

**A Importação/Exportação de Disco dá suporte à criptografia AES 256?**

Serviço de importação/exportação do Azure por padrão criptografa com a criptografia bitlocker AES 128, mas isso pode ser aumentada tooAES 256 criptografando manualmente com o bitlocker antes dos dados são copiados. 

Se estiver usando o [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), veja abaixo um comando de exemplo
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Se usar [ferramenta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) especificar "AlreadyEncrypted" e forneça a chave Olá Olá driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Próximas etapas

* [Configurando a ferramenta WAImportExport de saudação](storage-import-export-tool-how-to.md)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)
* [Exemplo de API REST de importação e exportação do Azure](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)


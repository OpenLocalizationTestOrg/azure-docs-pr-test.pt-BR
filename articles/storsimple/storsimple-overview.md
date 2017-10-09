---
title: "Visão geral da solução aaaStorSimple 8000 series | Microsoft Docs"
description: "Descreve as camadas de StorSimple, dispositivo hello, dispositivo virtual, serviços e gerenciamento de armazenamento e apresenta os principais termos usados no StorSimple."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 7144d218-db21-4495-88fb-e3b24bbe45d1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/10/2017
ms.author: v-sharos@microsoft.com
ms.openlocfilehash: 0891841186dcd4c46f48d13ed829b98fab7bdf67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-a-hybrid-cloud-storage-solution"></a>Série 8000 StorSimple: uma solução de armazenamento em nuvem híbrida
## <a name="overview"></a>Visão geral
Bem-vindo tooMicrosoft StorSimple do Azure, uma solução de armazenamento integrado que gerencia as tarefas de armazenamento entre dispositivos locais e armazenamento em nuvem Microsoft Azure. StorSimple é uma solução de SAN (rede) de área de armazenamento eficiente, econômica e facilmente gerenciável que elimina muitos dos problemas de saudação e gastos associados a proteção de armazenamento e dados corporativos. Usa o dispositivo da série StorSimple 8000 proprietário hello, integra-se com os serviços de nuvem e fornece um conjunto de ferramentas de gerenciamento para uma visualização perfeita de todo o armazenamento corporativo, incluindo o armazenamento em nuvem. (informações de implantação StorSimple Olá publicadas no site do Microsoft Azure Olá se aplica tooStorSimple 8000 series somente para dispositivos. Se você estiver usando um dispositivo da série StorSimple 5000/7000, vá muito[StorSimple ajuda](http://onlinehelp.storsimple.com/).)

StorSimple usa [camadas de armazenamento](#automatic-storage-tiering) toomanage dados armazenados em várias mídias de armazenamento. conjunto de trabalho atual Olá é armazenado no local em unidades de estado sólido (SSDs), os dados que são usados com menos frequência são armazenados em unidades de disco rígido (HDDs) e dados de arquivamento é enviada por push toohello nuvem. Além disso, StorSimple usa eliminação de duplicação e compactação tooreduce Olá quantidade de armazenamento que Olá dados consomem. Para obter mais informações, vá muito[eliminação de duplicação e compactação](#deduplication-and-compression). Para obter definições de outros principais termos e conceitos usados na documentação da série StorSimple 8000 do hello, ir muito[terminologia do StorSimple](#storsimple-terminology) final Olá deste artigo.

Além disso toostorage management, recursos de proteção de dados StorSimple habilitar você toocreate sob demanda e backups agendados e armazená-los localmente ou na saudação de nuvem. Backups são realizados no formulário de saudação de instantâneos incrementais, que significa que eles podem ser criados e restaurados rapidamente. Instantâneos de nuvem podem ser extremamente importantes em cenários de recuperação de desastres pois substituir os sistemas de armazenamento secundária (como o backup em fita) e permitir toorestore dados tooyour datacenter ou tooalternate sites, se necessário.

![ícone de vídeo](./media/storsimple-overview/video_icon.png) Assista o vídeo de saudação para tooMicrosoft uma breve introdução do Azure StorSimple.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/StorSimple-Hybrid-Cloud-Storage-Solution/player]

## <a name="why-use-storsimple"></a>Por que usar StorSimple?
Olá tabela a seguir descreve algumas das principais benefícios do hello fornecidos pelo Microsoft Azure StorSimple.

| Recurso | Benefício |
| --- | --- |
| Integração transparente |Usa recursos de armazenamento de dados de link tooinvisibly de protocolo iSCSI de saudação. Isso garante que os dados armazenados na nuvem hello, no datacenter hello, ou em servidores remotos pareçam toobe armazenado em um único local. |
| Redução nos custos de armazenamento |Aloca local suficiente ou demandas atuais de toomeet de armazenamento em nuvem e amplia o armazenamento em nuvem somente quando necessário. Reduz ainda mais os requisitos de armazenamento e as despesas, eliminando versões redundantes de saudação mesmo dados (eliminação de duplicação) e utilizando compactação. |
| Gerenciamento simplificado do armazenamento |Fornece tooconfigure de ferramentas de administração do sistema e gerenciar dados armazenados localmente, em um servidor remoto e na nuvem de saudação. Além disso, você pode gerenciar o backup e restaurar as funções de um snap-in do Microsoft Management Console (MMC).|
| Aprimoramento da recuperação de desastres e conformidade |Não requer tempo de recuperação estendido. Em vez disso, ele restaura os dados conforme necessário. Isso significa que as operações normais podem continuar com um mínimo de interrupção. Além disso, você pode configurar agendas de backup políticas toospecify e retenção de dados. |
| Mobilidade de dados |Os dados carregados tooMicrosoft serviços podem ser acessados de outros sites para fins de recuperação e migração de nuvem do Azure. Além disso, você pode usar soluções de nuvem do StorSimple tooconfigure StorSimple em máquinas virtuais (VMs) em execução no Microsoft Azure. Olá VMs pode usar dispositivos virtuais tooaccess armazenados dados para fins de teste ou de recuperação. |
| Continuidade dos negócios |Permite toomigrate de usuários de série StorSimple 7000 5000 dispositivo da série seus dados tooa StorSimple 8000. |
| Disponibilidade no hello Portal do Azure Government |StorSimple está disponível no hello Portal do Azure governamental. Para obter mais informações, consulte [implantar seu dispositivo do StorSimple local em Olá governo Portal](storsimple-8000-deployment-walkthrough-gov-u2.md). |
| Disponibilidade e proteção de dados |Olá StorSimple série 8000 oferece suporte a zona redundante armazenamento (ZRS), em adição tooLocally armazenamento redundante (LRS) e armazenamento com redundância geográfica (GRS). Consulte também[este artigo sobre as opções de redundância de armazenamento do Azure](https://azure.microsoft.com/documentation/articles/storage-redundancy/) para obter detalhes ZRS. |
| Suporte para aplicativos críticos |StorSimple permite que identificar volumes adequados como fixado localmente que por sua vez garante que os dados exigidos por aplicativos críticos não sejam toohello em camadas em nuvem. Volumes localmente afixados não são as latências de toocloud assunto ou problemas de conectividade. Para obter mais informações sobre volumes fixados localmente, consulte [usar Olá Gerenciador de dispositivos do StorSimple service toomanage volumes](storsimple-8000-manage-volumes-u2.md). |
| Baixa latência e alto desempenho |Você pode criar soluções de nuvem que tiram proveito da saudação de alto desempenho, recursos de baixa latência de armazenamento premium do Azure. Para obter mais informações sobre dispositivos de nuvem premium do StorSimple, consulte [Implantar e gerenciar um Dispositivo de Nuvem StorSimple no Azure](storsimple-8000-cloud-appliance-u2.md). |


## <a name="storsimple-components"></a>Componentes do StorSimple
Olá solução Microsoft Azure StorSimple inclui Olá componentes a seguir:

* **Dispositivo do Microsoft Azure StorSimple** - uma matriz de armazenamento híbrido local que contém SSDs e HDDs, juntamente com controladores redundantes e recursos de failover automático. controladores de saudação gerenciam o armazenamento hierárquico, colocando atualmente usados (ou dados quentes) no armazenamento local (em Olá dispositivo ou local servidores), ao mover dados usados com menos frequência toohello na nuvem.
* **Solução de nuvem do StorSimple** — também conhecido como Olá dispositivo Virtual StorSimple, esta é uma versão do software do dispositivo StorSimple Olá que replica a arquitetura de saudação e a maioria dos recursos do dispositivo de armazenamento híbrido físico hello. Olá StorSimple Appliance de nuvem é executado em um único nó em uma máquina virtual do Azure. Dispositivos virtuais premium, que aproveitam o armazenamento premium do Azure, estão disponíveis na Atualização 2 e posterior.
* **Serviço de Gerenciador de dispositivos de StorSimple** – uma extensão de saudação portal do Azure que permite a você gerenciar um dispositivo StorSimple ou StorSimple Appliance de nuvem em uma única interface da web. Você pode usar toocreate de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar serviços, exibir e gerenciar dispositivos, exibir alertas, gerenciar volumes, exibir e gerenciar políticas de backup e o catálogo de backup hello.
* **O Windows PowerShell para StorSimple** – uma interface de linha de comando que você pode usar toomanage Olá dispositivo StorSimple. Windows PowerShell para StorSimple possui recursos que permitem a você tooregister seu dispositivo StorSimple, configurar a interface de rede Olá no seu dispositivo, instalar determinados tipos de atualizações, solucionar problemas de seu dispositivo acessando a sessão de suporte de saudação e alterar Olá estado do dispositivo. Você pode acessar o Windows PowerShell para StorSimple conexão console serial do toohello ou usando o Windows PowerShell remotamente.
* **Cmdlets do Azure PowerShell StorSimple** – uma coleção de cmdlets do Windows PowerShell que permitem tooautomate tarefas de nível de serviço e a migração da linha de comando hello. Para obter mais informações sobre Olá cmdlets do Azure PowerShell para StorSimple, vá toohello [referência de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0#azure).
* **Gerenciador de instantâneos StorSimple** – um snap-in do MMC que utiliza grupos de volume e backups consistentes com o aplicativo do toogenerate Olá serviço de cópias de sombra de Volume do Windows. Além disso, você pode usar o clone e Gerenciador de instantâneos StorSimple toocreate agendas de backup ou restaurar volumes.
* **Adaptador StorSimple para SharePoint** – uma ferramenta que estende transparentemente proteção de dados e armazenamento do Microsoft Azure StorSimple tooSharePoint farms de servidores, tornando o armazenamento do StorSimple visível e gerenciável de saudação Central do SharePoint Portal de administração.

diagrama de saudação abaixo fornece uma visão geral da arquitetura do Microsoft Azure StorSimple de saudação e componentes.

![Arquitetura do StorSimple](./media/storsimple-overview/overview-big-picture.png)

Olá seções a seguir descrevem cada um desses componentes em maiores detalhes e explicam como Olá solução organiza dados, aloca armazenamento e facilita o gerenciamento de armazenamento e proteção de dados. Olá última seção fornece definições para alguns termos importantes hello e conceitos relacionados tooStorSimple componentes e o gerenciamento.

## <a name="storsimple-device"></a>Dispositivo StorSimple
dispositivo do Microsoft Azure StorSimple Olá é uma matriz de armazenamento híbrido local que fornece armazenamento primário e iSCSI toodata de acesso armazenado nela. Ele gerencia a comunicação com o armazenamento em nuvem e ajuda a segurança de saudação tooensure e confidencialidade de todos os dados armazenados em Olá solução Microsoft Azure StorSimple.

o dispositivo StorSimple Olá inclui SSDs e HDDs de unidades de disco rígido, bem como suporte para clustering e failover automático. Ele contém um processador compartilhado, armazenamento compartilhado e dois controladores espelhados. Cada controlador fornece o seguinte hello:

* Computador de host de tooa de Conexão
* Backup toosix rede portas tooconnect toohello rede local (LAN)
* Monitoramento de hardware
* Memória de acesso aleatório não volátil (NVRAM), que mantém as informações mesmo que a alimentação seja interrompida
* Suporte a cluster atualizando toomanage atualizações de software em servidores em um cluster de failover para que as atualizações de saudação tenham pouco ou nenhum efeito na disponibilidade de serviço
* Serviço de cluster, que funciona como um cluster de back-end, oferecendo alta disponibilidade e minimizando os efeitos adversos que podem ocorrer se um HDD ou SSD falhar ou ficar offline

Somente um controlador está ativo em qualquer momento no tempo. Se o controlador ativo Olá falhar, Olá segundo controlador torna-se ativo automaticamente.

Para obter mais informações, vá muito[StorSimple componentes de hardware e status](storsimple-8000-monitor-hardware-status.md).

## <a name="storsimple-cloud-appliance"></a>Dispositivo de Nuvem StorSimple
Você pode usar o StorSimple toocreate um aplicativo de nuvem que replica a arquitetura de saudação e os recursos do dispositivo de armazenamento híbrido físico hello. Olá StorSimple Appliance de nuvem (também conhecido como Olá dispositivo Virtual StorSimple) é executado em um único nó em uma máquina virtual do Azure. (Um dispositivo de nuvem só pode ser criado em uma máquina virtual do Azure. Você não pode criá-lo em um servidor local ou em um dispositivo StorSimple.)

Olá nuvem tem Olá recursos a seguir:

* Ele se comporta como um dispositivo físico e pode oferecer um iSCSI em máquinas de toovirtual de interface na nuvem de saudação.
* Você pode criar um número ilimitado de dispositivos de nuvem na nuvem hello e ligá-los e desativar o conforme necessário.
* Ele pode ajudar a simular ambientes locais em cenários de recuperação de desastre, de desenvolvimento ou teste, e pode ajudar na recuperação no nível do item de backups.

Olá StorSimple Appliance de nuvem está disponível em dois modelos: dispositivo Olá 8010 (anteriormente conhecido como modelo Olá 1100) e o dispositivo Olá 8020. dispositivo 8010 Olá tem a capacidade máxima de 30 TB. dispositivo 8020 Hello, que aproveita o armazenamento premium do Azure, tem a capacidade máxima de 64 TB. (Em camadas locais, o armazenamento premium do Azure armazena dados em SSDs, enquanto o armazenamento padrão armazena dados em HDDs.) Observe que você deve ter um armazenamento do Azure premium armazenamento conta toouse premium. Para obter mais informações sobre o armazenamento premium, ir muito[armazenamento Premium: armazenamento de alto desempenho para cargas de trabalho de máquina Virtual do Azure](../storage/common/storage-premium-storage.md).

Para obter mais informações sobre Olá StorSimple Appliance de nuvem, vá muito[implantar e gerenciar um dispositivo de nuvem no Azure StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="storsimple-device-manager-service"></a>Serviço do Gerenciador de Dispositivos StorSimple
Microsoft Azure StorSimple fornece uma interface de usuário baseada na web (serviço de Gerenciador de dispositivos de StorSimple Olá) que permite que você toocentrally gerenciar datacenter e armazenamento em nuvem. Você pode usar Olá Gerenciador de dispositivos do StorSimple service tooperform Olá tarefas a seguir:

* Definir configurações do sistema para dispositivos StorSimple.
* Configurar e gerenciar configurações de segurança para dispositivos StorSimple.
* Configurar credenciais e propriedades de nuvem.
* Configurar e gerenciar volumes em um servidor.
* Configurar grupos de volumes.
* Fazer backup e restaurar dados.
* Monitorar o desempenho.
* Revisar as configurações do sistema e identificar possíveis problemas.

Você pode usar tooperform de serviço do Gerenciador de dispositivos de StorSimple Olá todas as tarefas de administração, exceto aquelas que exigem inatividade, como a configuração inicial e a instalação de atualizações do sistema.

Para obter mais informações, vá muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

## <a name="windows-powershell-for-storsimple"></a>Windows PowerShell para StorSimple
O Windows PowerShell para StorSimple fornece uma interface de linha de comando que você pode usar toocreate e gerenciar o serviço do Microsoft Azure StorSimple hello e configurar e monitorar dispositivos de StorSimple. É uma interface de linha de comando com base no Windows PowerShell que inclui cmdlets dedicados para gerenciar seu dispositivo StorSimple. O Windows PowerShell para StorSimple tem recursos que permitem:

* Registrar um dispositivo.
* Configure a interface de rede de saudação em um dispositivo.
* Instalar determinados tipos de atualizações.
* Solucionar problemas de seu dispositivo acessando a sessão de suporte de saudação.
* Alterar o estado do dispositivo hello.

Você pode acessar o Windows PowerShell para StorSimple em um console serial (em um host do computador conectado diretamente dispositivo toohello) ou remotamente usando o Windows PowerShell remotamente. Observe que alguns Windows PowerShell para tarefas de StorSimple, como o registro de dispositivo inicial, só pode ser feito no console serial hello.

Para obter mais informações, vá muito[usar o Windows PowerShell para StorSimple tooadminister seu dispositivo](storsimple-8000-windows-powershell-administration.md).

## <a name="azure-powershell-storsimple-cmdlets"></a>cmdlets Azure PowerShell StorSimple
Olá StorSimple do Azure PowerShell cmdlets são um conjunto de cmdlets do Windows PowerShell que permitem tooautomate nível de serviço e as tarefas de migração da linha de comando hello. Para obter mais informações sobre Olá cmdlets do Azure PowerShell para StorSimple, vá toohello [referência de cmdlet](/powershell/module/azure/?view=azuresmps-3.7.0).

## <a name="storsimple-snapshot-manager"></a>Gerenciador de instantâneos do StorSimple
Gerenciador de instantâneos StorSimple é um snap-in do Console de gerenciamento Microsoft (MMC) que você pode usar toocreate consistente e point-in-time cópias de backup local e da nuvem. Olá snap-in é executado em um host baseado no Windows Server. Você pode usar o Gerenciador de instantâneos do StorSimple para:

* Configurar, fazer backup e excluir volumes.
* Configurar o volume tooensure grupos que o backup dos dados é consistente com o aplicativo.
* Gerencie políticas de backup para que os dados são feitos em um horário pré-determinado e armazenados em um local designado (localmente ou na nuvem Olá).
* Restaurar volumes e arquivos individuais.

Os backups são capturados como instantâneos, o que registram somente as alterações de saudação desde Olá último instantâneo foi tirado e exigem muito menos espaço de armazenamento que os backups completos. Você pode criar agendas de backup ou fazer backups imediatos, conforme necessário. Além disso, você pode usar políticas de retenção do Gerenciador de instantâneos StorSimple tooestablish que controlam quantas fotos serão salvas. Se você precisar posteriormente toorestore dados de um backup, permite de Gerenciador de instantâneos StorSimple que você selecionar Olá catálogo de locais ou instantâneos de nuvem. 

Se ocorrer um desastre ou se precisar de dados de toorestore por outro motivo, o Gerenciador de instantâneos StorSimple restaurá-lo incrementalmente conforme necessário. Restauração de dados não requer que você desligue todo o sistema Olá enquanto você restaura um arquivo, substituição de equipamentos ou move operações tooanother site.

Para obter mais informações, vá muito[o que é StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

## <a name="storsimple-adapter-for-sharepoint"></a>Adaptador do StorSimple para SharePoint
Microsoft Azure StorSimple inclui Olá adaptador StorSimple para SharePoint, um componente opcional que estende transparentemente farms de servidores de tooSharePoint de recursos de proteção de dados e armazenamento do StorSimple. adaptador de saudação funciona com um provedor de armazenamento de Blob remoto (RBS) e o recurso RBS do SQL Server de hello, permitindo que você toomove BLOBs tooa server backup pelo sistema do Microsoft Azure StorSimple hello. Microsoft Azure StorSimple, em seguida, armazena dados BLOB Olá localmente ou na nuvem hello, com base no uso.

Olá adaptador StorSimple para SharePoint é gerenciado por dentro do portal de Administração Central do SharePoint hello. Consequentemente, gerenciamento do SharePoint permanece centralizado e todo o armazenamento aparece toobe no farm do SharePoint hello.

Para obter mais informações, vá muito[adaptador StorSimple para SharePoint](storsimple-adapter-for-sharepoint.md). 

## <a name="storage-management-technologies"></a>Tecnologias de gerenciamento de armazenamento
Além disso toohello dedicado dispositivo StorSimple, dispositivo virtual e outros componentes, Microsoft Azure StorSimple usa Olá software tecnologias tooprovide acesso rápido toodata e tooreduce o consumo de armazenamento a seguir:

* [Camadas de armazenamento automático](#automatic-storage-tiering) 
* [Provisionamento dinâmico](#thin-provisioning) 
* [Eliminação de duplicação e compactação](#deduplication-and-compression) 

### <a name="automatic-storage-tiering"></a>Camadas de armazenamento automático
Microsoft Azure StorSimple organiza automaticamente os dados em camadas lógicas com base no uso atual, idade e dados de tooother de relação. Dados que estão mais ativas é armazenada localmente, enquanto menos ativos e dados inativos são automaticamente migrados toohello nuvem. Olá diagrama a seguir ilustra essa abordagem de armazenamento.

![Camadas de armazenamento do StorSimple](./media/storsimple-overview/hcs-data-services-storsimple-components-tiers.png)

acesso rápido de tooenable, StorSimple armazena dados muito ativos (dados quentes) em SSDs no dispositivo do StorSimple hello. Ele armazena dados que são usados ocasionalmente (dados quentes) em HDDs no dispositivo hello ou em servidores no datacenter hello. Ele move dados inativos, dados de backup, e os dados mantidos para arquivamento ou nuvem toohello fins de conformidade. 

> [!NOTE]
> Na atualização 2 ou posterior, você pode especificar um volume fixado localmente, caso em que dados saudação permanecem no dispositivo local hello e não hierárquico toohello nuvem. 


O StorSimple ajusta e reorganiza as atribuições de dados e armazenamento conforme os padrões de uso mudam. Por exemplo, algumas informações poderão ficar menos ativas ao longo do tempo. Como ele se torna progressivamente menos ativo, elas são migradas da nuvem toohello tooHDDs SSDs e, em seguida. Se esses mesmos dados ficarem ativos novamente, é o dispositivo de armazenamento toohello back migrados.

processo de camadas de armazenamento Olá ocorre da seguinte maneira:

1. Um administrador do sistema configura uma conta de armazenamento em nuvem do Microsoft Azure.
2. administrador Olá usa Olá serial console e hello Gerenciador de dispositivos do StorSimple serviço (executando Olá portal do Azure) tooconfigure Olá dispositivo e o arquivo de servidor, criar políticas de proteção de volumes e dados. Máquinas locais (como servidores de arquivos) usem dispositivo StorSimple do hello Internet Small Computer System Interface (iSCSI) tooaccess hello.
3. Inicialmente, StorSimple armazena dados na camada SSD rápida de saudação do dispositivo de saudação.
4. Como Olá abordagens capacidade na camada SSD, StorSimple elimina a duplicação e compacta os blocos de dados mais antigos Olá e os move toohello da camada de unidade de disco rígido.
5. Como Olá capacidade de abordagens da camada HDD, StorSimple criptografa os blocos de dados mais antigos hello e envia-os com segurança conta de armazenamento do Microsoft Azure toohello via HTTPS.
6. Microsoft Azure cria várias réplicas de dados de saudação em seu datacenter e em um data center remoto, garantindo que os dados de saudação podem ser recuperados se ocorrer um desastre.
7. Quando o servidor de arquivos Olá solicita dados armazenados na nuvem hello, StorSimple retorna perfeitamente e armazena uma cópia na camada SSD de saudação do dispositivo do StorSimple hello.

#### <a name="how-storsimple-manages-cloud-data"></a>Como o StorSimple gerencia dados de nuvem

StorSimple elimina a duplicação de dados do cliente em todos os instantâneos de saudação e dados primário da saudação (dados gravados por hosts). Enquanto a eliminação de duplicação é excelente eficiência do armazenamento, faz pergunta hello "como está na nuvem hello" complicada. Olá hierárquica de dados primária e dados de instantâneo de saudação se sobrepõem uns com os outros. Um único bloco de dados na nuvem Olá pode ser usado como hierárquica de dados primária e também ser referenciado por vários instantâneos. Cada instantâneo de nuvem garante que uma cópia de todos os dados de point-in-time hello está bloqueada para a nuvem Olá até que esse instantâneo é excluído.

Dados só serão excluídos da nuvem hello quando não houver nenhum dado de toothat referências. Por exemplo, se usarmos um instantâneo de nuvem de todos os dados de saudação no dispositivo do StorSimple hello e, em seguida, excluir alguns dados primários, veremos Olá _dados primários_ drop imediatamente. Olá _da nuvem_ que inclui Olá hierárquica de dados e Olá backups, permanece Olá mesmo. Isso ocorre porque há um instantâneo ainda fazendo referência a dados na nuvem hello. Depois de nuvem Olá instantâneo será excluído (e qualquer outro instantâneo referenciado Olá mesmo dados), descarta o consumo de nuvem. Antes de removermos os dados de nuvem, verificamos se nenhum instantâneo ainda faz referência a esses dados. Esse processo é chamado _coleta de lixo_ e um serviço em segundo plano está em execução no dispositivo de saudação. Remoção de dados de nuvem não é imediata enquanto o serviço de coleta de lixo Olá verifica outras referências toothat dados antes da exclusão de saudação. velocidade de saudação da coleta de lixo depende do número total de saudação de instantâneos e dados de total de saudação. Normalmente, os dados de nuvem Olá são limpos em menos de uma semana.


### <a name="thin-provisioning"></a>Provisionamento dinâmico
O provisionamento dinâmico é uma tecnologia de virtualização na qual o armazenamento disponível aparece recursos físicos tooexceed. Em vez de reservar um armazenamento suficiente antecedência, StorSimple usa tooallocate provisionamento thin suficiente requisitos de espaço atual em toomeet. a natureza elástica Olá de armazenamento em nuvem facilita essa abordagem porque StorSimple pode aumentar ou diminuir a nuvem armazenamento toomeet demandas em constante mudança.

> [!NOTE]
> Os volumes fixados localmente não são provisionados de modo dinâmico. Armazenamento alocado tooa volume de somente local é provisionado em sua totalidade quando Olá volume é criado.


### <a name="deduplication-and-compression"></a>Eliminação de duplicação e compactação
Microsoft Azure StorSimple usa eliminação de duplicação e toofurther de compactação de dados reduzir os requisitos de armazenamento.

Eliminação de duplicação reduz Olá quantidade geral de dados armazenados, eliminando a redundância no conjunto de dados Olá armazenado. Como alterações nas informações, StorSimple ignora dados saudação inalterado e captura Olá somente as alterações. Além disso, o StorSimple reduz a quantidade de saudação dos dados armazenados por identificar e remover informações desnecessárias. 

> [!NOTE]
> Os dados em volumes fixados localmente não têm eliminação de duplicação nem são compactados. No entanto, os backups de volumes fixados localmente têm eliminação de duplicação e são compactados.


## <a name="storsimple-workload-summary"></a>Resumo de carga de trabalho do StorSimple
Um resumo de cargas de trabalho de StorSimple Olá com suporte é tabulado abaixo.

| Cenário | Carga de trabalho | Suportado | Restrições | Versão |
| --- | --- | --- | --- | --- |
| Colaboração |Compartilhamento de arquivos |Sim | |Todas as versões |
| Colaboração |Compartilhamento de arquivos distribuído |Sim | |Todas as versões |
| Colaboração |SharePoint |Sim* |Com suporte somente com volumes afixados localmente |Atualização 2 e posterior |
| Arquivamento |Arquivamento de arquivos simples |Sim | |Todas as versões |
| Virtualização |Máquinas virtuais |Sim* |Com suporte somente com volumes afixados localmente |Atualização 2 e posterior |
| Banco de dados |SQL |Sim* |Com suporte somente com volumes afixados localmente |Atualização 2 e posterior |
| Vigilância em vídeo |Vigilância em vídeo |Sim* |Suporte ao dispositivo StorSimple é dedicado a carga de trabalho de toothis somente |Atualização 2 e posterior |
| Backup |Backup de destino principal |Sim* |Suporte ao dispositivo StorSimple é dedicado a carga de trabalho de toothis somente |Atualização 3 e posterior |
| Backup |Backup de destino secundário |Sim* |Suporte ao dispositivo StorSimple é dedicado a carga de trabalho de toothis somente |Atualização 3 e posterior |

*Sim&#42; – Diretrizes e restrições da solução devem ser aplicadas.*

Olá cargas de trabalho a seguir não é suportado por dispositivos da série StorSimple 8000. Se forem implantadas no StorSimple, essas cargas de trabalho resultarão em uma configuração sem suporte.

* Imagens médicas
* Exchange
* VDI
* Oracle
* SAP
* Big data
* Distribuição de conteúdo
* Inicialização de SCSI

A seguir está uma lista de componentes da infraestrutura Olá StorSimple com suporte.

| Cenário | Carga de trabalho | Suportado | Restrições | Versão |
| --- | --- | --- | --- | --- |
| Geral |Rota Expressa |Sim | |Todas as versões |
| Geral |DataCore FC |Sim* |Suporte com DataCore SANsymphony |Todas as versões |
| Geral |DFSR |Sim* |Com suporte somente com volumes afixados localmente |Todas as versões |
| Geral |Indexação |Sim* |Para volumes em camadas, somente a indexação de metadados tem suporte (sem dados).<br>Para volumes afixados localmente, a indexação completa tem suporte. |Todas as versões |
| Geral |Antivírus |Sim* |Para volumes em camadas, há suporte apenas para verificação ao abrir e fechar.<br> Para volumes afixados localmente, há suporte para verificação completa. |Todas as versões |

*Sim&#42; – Diretrizes e restrições da solução devem ser aplicadas.*

A seguir está uma lista de outros softwares que são usados com soluções de toobuild StorSimple.

| Tipo de carga de trabalho | Software usado com o StorSimple | Versões com suporte|Guia de toosolution de link| 
| --- | --- | --- | --- |
| Destino de backup |Veeam |Veeam v 9 e posterior |[StorSimple como um destino de backup com o Veeam](storsimple-configure-backup-target-veeam.md)|
| Destino de backup |VERITAS Backup Exec |Backup Exec 16 e posterior |[StorSimple como destino de backup com o Backup Exec](storsimple-configure-backup-target-using-backup-exec.md)|
| Destino de backup |Veritas NetBackup |NetBackup 7.7.x e posterior  |[StorSimple como um destino de backup com o NetBackup](storsimple-configure-backuptarget-netbackup.md)|
| Compartilhamento de Arquivos Global <br></br> Colaboração |Talon  |[StorSimple com Talon](https://www.talonstorage.com/products/fast-deployment-azure-storsimple) | |

## <a name="storsimple-terminology"></a>Terminologia do StorSimple
Antes de implantar sua solução do Microsoft Azure StorSimple, recomendamos que você examine a seguir Olá termos e definições.

### <a name="key-terms-and-definitions"></a>Principais termos e definições
| Termo (sigla ou abreviação) | Descrição |
| --- | --- |
| Registro de controle de acesso (ACR) |Um registro associado a um volume em seu dispositivo do Microsoft Azure StorSimple que determina quais hosts podem se conectar a tooit. Olá determinação se baseia em Olá iSCSI IQN (nome qualificado) dos hosts hello (contidos no hello ACR) que estão se conectando tooyour o dispositivo StorSimple. |
| AES-256 |Um algoritmo de criptografia AES (Advanced Standard) 256 bits para criptografar dados enquanto se movimentam tooand da nuvem de saudação. |
| tamanho da unidade de alocação (AUS) |Olá menor quantidade de espaço em disco que pode ser alocada toohold um arquivo em seus sistemas de arquivos do Windows. Se um tamanho de arquivo não é um múltiplo par do tamanho do cluster hello, espaço extra deve ser usado toohold arquivo de saudação (backup toohello próximo múltiplo do tamanho do cluster Olá) resulta em espaço perdido e a fragmentação do disco rígido de saudação. <br>Olá recomendado que AUSTRÁLIA para volumes do StorSimple do Azure é 64 KB porque ela funciona bem com algoritmos de eliminação de duplicação de saudação. |
| camadas de armazenamento automatizado |Movendo automaticamente os dados menos ativos de tooHDDs SSDs e, em seguida, tooa camada na nuvem hello e, em seguida, habilitar o gerenciamento de todo o armazenamento de uma interface de usuário central. |
| catálogo de backup |Uma coleção de backups, geralmente relacionados pelo tipo de aplicativo hello que foi usado. Essa coleção é exibida na folha de catálogo de Backup de saudação do hello serviço do Gerenciador de dispositivos do StorSimple da interface do usuário. |
| arquivo de catálogo de backup |Um arquivo que contém uma lista de instantâneos disponíveis atualmente armazenados no banco de dados de backup saudação do StorSimple Snapshot Manager. |
| política de backup |Uma seleção de volumes, tipo de backup e um agendamento que permite a você toocreate backups em um cronograma predefinido. |
| objetos binários grandes (BLOBs) |Uma coleção de dados binários armazenados como entidade única em um sistema de gerenciamento de banco de dados. BLOBs são normalmente imagens, áudio ou outros objetos de multimídia, embora o código executável binário, às vezes, é armazenado como um BLOB. |
| Protocolo CHAP (Challenge Handshake Authentication Protocol) |Um protocolo usado par de saudação tooauthenticate de uma conexão, com base no ponto de saudação compartilhando uma senha ou segredo. O protocolo CHAP pode ser unidirecional ou mútuo. Com o CHAP unidirecional, o destino de saudação autentica um iniciador. CHAP mútuo requer que o destino Olá autentique o iniciador de saudação e esse iniciador Olá autentica o destino de saudação. |
| clone |Uma cópia duplicada de um volume. |
| Nuvem como camada (CaaT) |Armazenamento na nuvem integrado como uma camada na arquitetura de armazenamento Olá para que todo o armazenamento pareça toobe parte da rede de armazenamento de uma empresa. |
| provedor de serviços de nuvem (CSP) |Um provedor de serviços de computação em nuvem. |
| instantâneo de nuvem |Uma cópia point-in-time de dados de volume que são armazenados na nuvem hello. Um instantâneo de nuvem é equivalente instantâneo tooa replicado em um sistema de armazenamento externo, diferentes. Instantâneos de nuvem são particularmente úteis em cenários de recuperação de desastres. |
| chave de criptografia de armazenamento em nuvem |Uma senha ou uma chave usada pelos StorSimple dispositivo tooaccess Olá criptografado dados enviados pelo seu dispositivo toohello nuvem. |
| atualização com suporte a cluster |Gerenciando atualizações de software em servidores em um cluster de failover para que as atualizações de saudação tenham pouco ou nenhum efeito na disponibilidade do serviço. |
| caminho de dados |Uma coleção de unidades funcionais que realizam operações de processamento de dados inter-relacionadas. |
| desativar |Uma ação permanente quebras Olá conexão entre o dispositivo StorSimple hello e hello associados serviço de nuvem. Instantâneos de nuvem do dispositivo Olá permanecem após esse processo e podem ser clonados ou usados para recuperação de desastres. |
| espelhamento de disco |Unidades de replicação dos volumes de disco lógico em rígidos separados em tempo real tooensure a disponibilidade contínua. |
| espelhamento de disco dinâmico |Replicação de volumes de disco lógico em discos dinâmicos. |
| discos dinâmicos |Um formato de volume de disco que usa Olá toostore do Gerenciador de discos lógicos (LDM) e gerenciar dados em vários discos físicos. Discos dinâmicos pode ser ampliada tooprovide mais espaço livre. |
| Compartimento estendido de vários discos (EBOD) |Um compartimento secundário do dispositivo Microsoft Azure StorSimple que contém discos rígidos adicionais de armazenamento. |
| provisionamento FAT |Um provisionamento de armazenamento convencional no qual armazenamento espaço é alocado com base em necessidades antecipadas (e geralmente está além da necessidade atual Olá). Consulte também *provisionamento dinâmico*. |
| unidade de disco rígido (HDD) |Uma unidade que usa dados de toostore platters rotação. |
| armazenamento em nuvem híbrida |Uma arquitetura de armazenamento que usa os recursos locais e externos, incluindo armazenamento em nuvem. |
| Internet Small Computer System Interface (iSCSI) |Um padrão de rede de armazenamento baseado no protocolo de internet (IP) para vincular equipamentos ou instalações de armazenamento de dados. |
| Iniciador iSCSI |Um componente de software que permite que um computador host executando a rede de armazenamento externo com base em iSCSI do Windows tooconnect tooan. |
| Nome qualificado de iSCSI (IQN) |Um nome exclusivo que identifica um destino ou iniciador iSCSI. |
| destino iSCSI |Um componente de software que fornece subsistemas de disco de iSCSI centralizados em redes de área de armazenamento. |
| arquivamento dinâmico |Uma abordagem de armazenamento em que dados de arquivamento são acessíveis tempo Olá todo (não são armazenadas fora do local em fita, por exemplo). O Microsoft Azure StorSimple usa arquivamento dinâmico. |
| volumes fixado localmente |um volume que reside no dispositivo hello e nunca é hierárquico toohello nuvem. |
| instantâneo local |Uma cópia point-in-time de dados de volume que são armazenados no dispositivo do Microsoft Azure StorSimple hello. |
| Microsoft Azure StorSimple |Uma solução avançada que consiste em um dispositivo de armazenamento do datacenter e o software que permite IT organizações tooleverage armazenamento em nuvem como se fosse o armazenamento do data center. O StorSimple simplifica o gerenciamento e a proteção de dados enquanto reduz os custos. solução de saudação consolida primária armazenamento, arquivamento, backup e recuperação de desastres (DR) por meio de uma integração perfeita com a nuvem de saudação. Combinando o gerenciamento de dados em nuvem e armazenamento SAN em uma plataforma de classe empresarial, os dispositivos StorSimple tornam possível oferecer velocidade, simplicidade e confiabilidade em relação a todas as necessidades relacionadas ao armazenamento. |
| Módulo de energia e resfriamento (PCM) |Componentes de hardware do seu dispositivo StorSimple consiste Olá fontes de alimentação e o ventilador de resfriamento de hello hello, portanto, módulo de energia e refrigeração de nome. compartimento principal de saudação do dispositivo Olá possui dois PCMs de 764W, enquanto Olá compartimento EBOD possui dois PCMs de 580W. |
| compartimento primário |Compartimento principal do seu dispositivo StorSimple que contém os controladores da plataforma de aplicativo hello. |
| objetivo de tempo de recuperação (RTO) |quantidade máxima de saudação de tempo que deve ser dispendido antes que um processo de negócios ou sistema seja totalmente restaurada após um desastre. |
| serial anexado SCSI (SAS) |Tipo de unidade de disco rígido (HDD) |
| chave de criptografia de dados do serviço |Uma chave feitas dispositivo StorSimple novo tooany disponíveis que registra com hello serviço do Gerenciador de dispositivos do StorSimple. dados de configuração de saudação transferidos entre o serviço de Gerenciador de dispositivos de StorSimple hello e dispositivo Olá são criptografados usando uma chave pública e, em seguida, podem ser descriptografados apenas no dispositivo hello usando uma chave privada. Chave de criptografia de dados de serviço permite Olá serviço tooobtain essa chave privada para descriptografia. |
| chave de registro do serviço |Uma chave que ajuda a registrar o dispositivo StorSimple Olá com hello serviço do Gerenciador de dispositivos de StorSimple para que ele apareça no hello portal do Azure para ações de gerenciamento adicionais. |
| Small Computer System Interface (SCSI) |Conjunto de padrões para conectar computadores fisicamente e transmitir dados entre eles. |
| unidade de estado sólido (SSD) |Disco que não contém peças móveis; por exemplo, uma unidade flash. |
| do Azure |Um conjunto de credenciais de acesso vinculadas tooyour conta de armazenamento para um provedor de serviços de nuvem especificada. |
| Adaptador do StorSimple para SharePoint |Um componente do Microsoft Azure StorSimple que estende transparentemente tooSharePoint farms de servidor de proteção de dados e armazenamento do StorSimple. |
| Serviço do Gerenciador de Dispositivos StorSimple |Uma extensão de Olá portal do Azure que permite que você toomanage o local do Azure StorSimple e os dispositivos virtuais. |
| Gerenciador de instantâneos do StorSimple |Snap-in do console de gerenciamento Microsoft (MMC)  para gerenciar operações de backup e restauração no Microsoft Azure StorSimple. |
| fazer backup |Um recurso que permite Olá usuário tootake um backup interativo de um volume. É uma maneira alternativa de fazer um backup manual de um volume como tootaking contrário um backup automatizado por meio de uma política definida. |
| Provisionamento dinâmico |Um método de otimizar a eficiência de saudação com quais Olá espaço de armazenamento disponível é usado em sistemas de armazenamento. No provisionamento dinâmico, o armazenamento de saudação é alocado entre vários usuários com base no hello espaço mínimo exigido por cada usuário em um determinado momento. Veja também *provisionamento estático*. |
| disposição em camadas |Organizar dados em agrupamentos lógicos com base no uso atual, idade e dados de tooother de relação. O StorSimple organiza automaticamente os dados em camadas. |
| volume |Áreas de armazenamento lógico apresentadas na forma de saudação de unidades. Volumes do StorSimple correspondem toohello volumes montados pelo host hello, incluindo os descobertos através do uso de saudação do iSCSI e um dispositivo StorSimple. |
| contêiner de volume |Um grupo de volumes e configurações de saudação que se aplicam a toothem. Todos os volumes em seu dispositivo StorSimple são agrupados em contêineres de volume. Configurações de contêiner de volume incluem contas de armazenamento, configurações de criptografia para dados enviados toocloud com chaves de criptografia associada e largura de banda consumida para operações que envolvem a nuvem de saudação. |
| grupo de volumes |No Gerenciador de instantâneos do StorSimple, um grupo de volumes é uma coleção de volumes configurados toofacilitate do processamento do backup. |
| Serviço de cópias de sombra de volume (VSS) |Um serviço do sistema operacional Windows Server que facilita a consistência do aplicativo, comunicando-se com reconhecimento de VSS aplicativos toocoordinate Olá a criação de instantâneos incrementais. O VSS garante que os aplicativos de saudação estejam temporariamente inativos quando os instantâneos são realizados. |
| Windows PowerShell para StorSimple |Uma interface de linha de comando baseado no Windows PowerShell usado toooperate e gerenciar seu dispositivo StorSimple. Ao mesmo tempo que mantém alguns dos recursos básicos de saudação do Windows PowerShell, essa interface possui cmdlets dedicados que se destinam a gerenciar um dispositivo StorSimple. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre a [Segurança do StorSimple](storsimple-8000-security.md).


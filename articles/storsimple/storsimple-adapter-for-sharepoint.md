---
title: aaaInstall adaptador StorSimple para SharePoint | Microsoft Docs
description: "Descreve como tooinstall e configurar ou remover Olá adaptador StorSimple para SharePoint em um farm de servidores do SharePoint."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 36c20b75-f2e5-4184-a6b5-9c5e618f79b2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: v-sharos
ms.openlocfilehash: 9a7347232fb80156d93212e6382cdd4fab98a2d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-hello-storsimple-adapter-for-sharepoint"></a>Instalar e configurar Olá adaptador StorSimple para SharePoint
## <a name="overview"></a>Visão geral
Olá adaptador StorSimple para SharePoint é um componente que permite a você fornecer armazenamento flexível do Microsoft Azure StorSimple e farms de servidor de tooSharePoint de proteção de dados. Você pode usar o conteúdo de objeto binário grande (BLOB) do hello adaptador toomove de saudação do SQL Server bancos de dados de conteúdo toohello Microsoft Azure StorSimple híbrida nuvem dispositivo de armazenamento.

Olá adaptador StorSimple para SharePoint funciona como um provedor de armazenamento de BLOB remoto (RBS) e usa Olá toostore do recurso de armazenamento de BLOB remoto do SQL Server conteúdo de SharePoint não estruturado (na forma de saudação de BLOBs) em um servidor de arquivos que é apoiado por um dispositivo StorSimple.

> [!NOTE]
> Olá adaptador StorSimple para SharePoint dá suporte ao armazenamento de BLOB do SharePoint Server 2010 remoto (RBS). Ele não dá suporte a EBS (External BLOB Storage) do SharePoint Server 2010.


* Olá toodownload adaptador StorSimple para SharePoint, vá muito[adaptador StorSimple para SharePoint] [ 1] em Olá Microsoft Download Center.
* Para obter informações sobre como planejar para RBS e RBS limitações, vá muito[decidir toouse RBS no SharePoint 2013] [ 2] ou [planejar para RBS (SharePoint Server 2010)] [3].

Hello restante esta visão geral descreve resumidamente a função hello de saudação do adaptador StorSimple para SharePoint e hello capacidade do SharePoint e limites de desempenho que você deve estar atento antes de instalar e configurar o adaptador de saudação. Depois de examinar essas informações, vá muito[do adaptador StorSimple para SharePoint](#storsimple-adapter-for-sharepoint-installation) toobegin configurar adaptador hello.

### <a name="storsimple-adapter-for-sharepoint-benefits"></a>Benefícios do Adaptador StorSimple para SharePoint
Em um site do SharePoint, o conteúdo é armazenado como dados BLOB não estruturados em um ou mais bancos de dados. Por padrão, esses bancos de dados são hospedados em computadores que executam o SQL Server e estão localizados no farm de servidores do SharePoint hello. Os BLOBs podem aumentar rapidamente de tamanho, consumindo grandes quantidades de armazenamento local. Por esse motivo, você poderá toofind solução de armazenamento de outro, menos dispendioso. SQL Server fornece uma tecnologia chamada RBS Remote Blob Storage () que permite armazenar conteúdo BLOB no sistema de arquivos hello, fora do banco de dados do SQL Server hello. Com o RBS, BLOBs podem residir no sistema de arquivos de saudação do computador Olá que está executando o SQL Server, ou eles podem ser armazenados no sistema de arquivos de saudação em outro computador do servidor.

O RBS requer que você use um provedor RBS, como saudação do adaptador StorSimple para SharePoint, tooenable RBS no SharePoint. Olá adaptador StorSimple para SharePoint funciona com o RBS, permitindo que você mover servidor tooa de BLOBs backup pelo sistema do Microsoft Azure StorSimple hello. Microsoft Azure StorSimple, em seguida, armazena dados BLOB Olá localmente ou na nuvem hello, com base no uso. BLOBs são muito ativos (normalmente referidos tooas da camada 1 ou dados ativos) residem localmente. Dados menos ativos e dados de arquivamento residem na nuvem hello. Depois de habilitar RBS em um banco de dados de conteúdo, qualquer novo conteúdo BLOB criado no SharePoint é armazenado no dispositivo do StorSimple hello e não no banco de dados de conteúdo do hello.

implementação do Microsoft Azure StorSimple de saudação do RBS fornece Olá benefícios a seguir:

* Ao mover BLOB tooa conteúdo servidor separado, você pode reduzir Olá carga da consulta no SQL Server, que pode melhorar a capacidade de resposta do SQL Server. 
* O Azure StorSimple usa eliminação de duplicação e compactação tooreduce tamanho dos dados.
* O Azure StorSimple fornece proteção de dados em forma de saudação de locais e instantâneos em nuvem. Além disso, se você colocar Olá próprio banco de dados no dispositivo do StorSimple hello, você pode fazer backup de banco de dados de conteúdo do hello e BLOBs juntos em uma forma de falha consistente. (Mover dispositivo toohello de banco de dados de conteúdo de saudação somente há suporte para o dispositivo da série StorSimple 8000 hello. Esse recurso não há suporte para a série de saudação 5000 ou 7000.)
* O Azure StorSimple inclui recursos de recuperação de desastres, inclusive failover, recuperação de arquivo e volume (incluindo recuperação de teste) e restauração rápida de dados.
* Você pode usar o software de recuperação de dados, como o Kroll Ontrack PowerControls, com instantâneos do StorSimple BLOB tooperform nível de item de recuperação de dados de conteúdo do SharePoint. (Esse software de recuperação de dados é uma compra separada.)
* Olá adaptador StorSimple para SharePoint conecta-se ao portal de Administração Central do SharePoint hello, permitindo que você toomanage sua solução do SharePoint inteira de um local central.

Mover o sistema de arquivos de conteúdo toohello BLOB pode fornecer outros benefícios e economias de custo. Por exemplo, usar o RBS pode reduzir a necessidade de saudação para armazenamento de nível 1 e, como ele diminui o banco de dados de conteúdo do hello, RBS pode reduzir o número de saudação de bancos de dados necessários no farm de servidores do SharePoint Olá. No entanto, outros fatores, como limites de tamanho do banco de dados e a quantidade de saudação do conteúdo, o RBS não também podem afetar os requisitos de armazenamento. Para obter mais informações sobre os custos de hello e benefícios de usar o RBS, consulte [planejar para RBS (SharePoint Foundation 2010)] [ 4] e [decidir toouse RBS no SharePoint 2013] [ 5].

### <a name="capacity-and-performance-limits"></a>Limites de capacidade e desempenho
Antes de considerar o uso de RBS em sua solução do SharePoint, você deve estar atento a saudação testado desempenho e limites de capacidade do SharePoint Server 2010 e SharePoint Server 2013, e como esses limites se relacionam tooacceptable desempenho. Para saber mais, consulte [Limites de software e limites para o SharePoint 2013](https://technet.microsoft.com/library/cc262787.aspx).

Examine a seguir Olá antes de configurar RBS:

* Certifique-se que tamanho total de saudação do hello conteúdo (tamanho de saudação de um banco de dados de conteúdo) mais o tamanho de saudação de qualquer blob externalizado associado não excede limite de tamanho RBS Olá suportado pelo SharePoint. Esse limite é de 200 GB. 
  
    **tamanho do BLOB e banco de dados de conteúdo do toomeasure**
  
  1. Execute esta consulta na Olá WFE de Administração Central. Iniciar Olá Shell de gerenciamento do SharePoint e digite Olá tamanho do Windows PowerShell comando tooget Olá de bancos de dados de conteúdo do hello a seguir:
     
     `Get-SPContentDatabase | Select-Object -ExpandProperty DiskSizeRequired`
     
      Esta etapa obtém o tamanho de saudação do banco de dados de conteúdo de saudação em disco hello.
  2. Execute um dos Olá consultas SQL no SQL Management Studio a seguir na caixa Olá SQL server em cada banco de dados de conteúdo e adicionar Olá resultado toohello número obtido na etapa 1.
     
     Nos bancos de dados de conteúdo do SharePoint 2013, digite:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[DocStreams] WHERE [Content] IS NULL`
     
     Nos bancos de dados de conteúdo do SharePoint 2010, digite:
     
     `SELECT SUM([Size]) FROM [ContentDatabaseName].[dbo].[AllDocs] WHERE [Content] IS NULL`
     
     Esta etapa obtém o tamanho de saudação do hello BLOBs que têm sido externalizados.
* É recomendável que você armazene todo o conteúdo BLOB e banco de dados localmente no dispositivo do StorSimple hello. o dispositivo StorSimple Olá é um cluster de dois nós para alta disponibilidade. Colocar bancos de dados de conteúdo do hello e BLOBs no dispositivo do StorSimple Olá fornece alta disponibilidade.
  
    Use tradicional do SQL Server migração melhores práticas toomove Olá banco de dados de conteúdo toohello dispositivo StorSimple. Mova o banco de dados de saudação somente depois que todo o conteúdo BLOB do banco de dados de saudação foi movido toohello compartilhamento de arquivos por meio do RBS. Se você escolher o dispositivo StorSimple de toohello de banco de dados de conteúdo do toomove Olá, é recomendável que você configure o armazenamento de banco de dados de conteúdo Olá no dispositivo hello como um volume primário.
* No Microsoft Azure StorSimple, se usar volumes em camadas, não é possível tooguarantee conteúdo armazenado localmente no dispositivo StorSimple de saudação não serão tooMicrosoft hierárquico armazenamento em nuvem do Azure. Portanto, é recomendável usar volumes do StorSimple localmente fixados em conjunto com o SharePoint RBS. Isso garantirá que todo conteúdo BLOB permanece localmente no dispositivo do StorSimple hello e não é movido tooMicrosoft do Azure.
* Se você não armazenar bancos de dados de conteúdo do hello no dispositivo do StorSimple hello, use tradicional do SQL Server alta disponibilidade práticas recomendadas que são compatíveis com o RBS. O clustering do SQL Server dá suporte a RBS, enquanto o espelhamento do SQL Server, não. 

> [!WARNING]
> Se você não tiver habilitado o RBS, não recomendamos mover o dispositivo de StorSimple toohello Olá conteúdo do banco de dados. Essa é uma configuração não testada.

## <a name="storsimple-adapter-for-sharepoint-installation"></a>Instalação do Adaptador StorSimple para SharePoint
Antes de instalar Olá adaptador StorSimple para SharePoint, você deve configurar o dispositivo StorSimple hello e certifique-se de que o farm de servidores do SharePoint hello e instanciação do SQL Server atendam todos os pré-requisitos. Este tutorial descreve os requisitos de configuração, bem como os procedimentos para instalar e atualizar Olá adaptador StorSimple para SharePoint.

## <a name="configure-prerequisites"></a>Configurar pré-requisitos
Antes de instalar Olá adaptador StorSimple para SharePoint, certifique-se de que o dispositivo StorSimple hello, farm do SharePoint server e do servidor SQL atendam Olá pré-requisitos a seguir.

### <a name="system-requirements"></a>Requisitos do sistema
Olá adaptador StorSimple para SharePoint funciona com hello hardware e software a seguir:

* Sistema operacional com suporte – Windows Server 2008 R2 SP1, Windows Server 2012 ou Windows Server 2012 R2
* Versões do SharePoint com suporte – SharePoint Server 2010 ou SharePoint Server 2013
* Versões do SQL Server com suporte – SQL Server 2008 Enterprise Edition, SQL Server 2008 R2 Enterprise Edition ou SQL Server 2012 Enterprise Edition
* Dispositivos do StorSimple com suporte –  StorSimple 8000 Series, StorSimple 7000 Series ou StorSimple 5000 Series.

### <a name="storsimple-device-configuration-prerequisites"></a>Pré-requisitos de configuração do dispositivo StorSimple
o dispositivo StorSimple Olá é um dispositivo de bloco e como tal requer um servidor de arquivos no qual os dados saudação podem ser hospedados. É recomendável que você use um servidor separado em vez de um servidor existente do farm do SharePoint hello. Este servidor de arquivos deve ser em Olá mesma rede local (LAN) como o computador do SQL Server Olá que hosts Olá bancos de dados.

> [!TIP]
> * Se você configurar seu farm do SharePoint para alta disponibilidade, você deve implantar o servidor de arquivos Olá para alta disponibilidade também.
> * Se você não armazenar o banco de dados de conteúdo do hello no dispositivo do StorSimple hello, use práticas tradicionais de alta disponibilidade que dão suporte ao RBS. O clustering do SQL Server dá suporte a RBS, enquanto o espelhamento do SQL Server, não. 


Certifique-se de que seu dispositivo StorSimple está configurado corretamente e que toosupport volumes adequados a implantação do SharePoint estão configurados e acessíveis do computador do SQL Server. Vá muito[implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md) se você ainda não tiver implantado e configurado seu dispositivo StorSimple. Observe o endereço IP de saudação do dispositivo do StorSimple Olá; Você precisará delas durante o adaptador StorSimple para SharePoint.

Além disso, certifique-se de que toobe de volume Olá usado para externalização BLOB atende Olá requisitos a seguir:

* volume Olá deve ser formatado com um tamanho de unidade de alocação de 64 KB.
* O front-end de web (WFE) e servidores de aplicativos devem ser tooaccess capaz de volume de saudação através de um caminho de convenção de nomenclatura Universal (UNC).
* farm de servidores do SharePoint Olá deve ser configurado toowrite toohello volume.

> [!NOTE]
> Depois de instalar e configurar o adaptador hello, toda externalização BLOB deve percorrer o dispositivo StorSimple hello (dispositivo Olá apresentarão Olá volumes tooSQL servidor e gerenciar as camadas de armazenamento Olá). Você não pode usar nenhum outro destino para externalização do BLOB.


Se você planejar toouse StorSimple Snapshot Manager tootake instantâneos de saudação BLOB e banco de dados, dados ser tooinstall-se de que o Gerenciador de instantâneos do StorSimple no servidor de banco de dados de saudação para que ele possa usar Olá tooimplement de serviço do gravador SQL Olá cópias de sombra de Volume do Windows Service (VSS).

> [!IMPORTANT]
> Gerenciador de instantâneos do StorSimple não oferece suporte a saudação gravador VSS do SharePoint e não é possível tirar instantâneos consistentes com aplicativos de dados do SharePoint. Em um cenário do SharePoint, o Gerenciador de instantâneos StorSimple fornece somente backups consistentes com falhas.


## <a name="sharepoint-farm-configuration-prerequisites"></a>Pré-requisitos de configuração de farm do SharePoint
Certifique-se de que seu farm do SharePoint Server esteja configurado corretamente da seguinte maneira:

* Verifique se seu farm de servidores do SharePoint está em um estado íntegro e verifique Olá seguinte:
* Todos os servidores de aplicativos registrados no farm hello e SharePoint WFE estão em execução e podem executar ping do servidor de saudação no qual você instalará Olá adaptador StorSimple para SharePoint.
* Olá serviço SharePoint Timer (SPTimerV3 ou SPTimerV4) está em execução em cada servidor WFE e servidor de aplicativos.
* Tanto hello serviço Timer do SharePoint e pool de aplicativos do IIS Olá sob a qual Olá executando o site de Administração Central do SharePoint tem privilégios administrativos.
* Certifique-se de que o IE ESC (Internet Explorer Enhanced Security Context) esteja desabilitado. Siga essas etapas toodisable IE ESC:
  
  1. Feche todas as instâncias do Internet Explorer.
  2. Inicie o Gerenciador do servidor de saudação.
  3. No painel esquerdo do hello, clique em **servidor Local**.
  4. Em Olá direita painel, em seguida muito**configuração de segurança aprimorada do IE**, clique em **em**.
  5. Em **Administradores**, clique em **Desabilitado**.
  6. Clique em **OK**.

## <a name="remote-blob-storage-rbs-prerequisites"></a>Pré-requisitos do RBS (Remote BLOB Storage)
Certifique-se de que você esteja usando uma versão com suporte do SQL Server. Somente hello versões a seguir são suportada e podem toouse RBS:

* SQL Server 2008 Enterprise Edition
* SQL Server 2008 R2 Enterprise Edition
* SQL Server 2012 Enterprise Edition

BLOBs podem ser externalizados somente naqueles volumes que Olá dispositivo StorSimple apresenta tooSQL Server. Não há suporte para outros destinos para externalização de BLOB.

Quando você concluiu todas as etapas de configuração de pré-requisitos, vá muito[Olá instalar adaptador StorSimple para SharePoint](#install-the-storsimple-adapter-for-sharepoint).

## <a name="install-hello-storsimple-adapter-for-sharepoint"></a>Instalar o hello adaptador StorSimple para SharePoint
Use Olá seguindo as etapas tooinstall Olá adaptador StorSimple para SharePoint. Se você estiver reinstalando o software hello, consulte [atualizar ou reinstalar o hello adaptador StorSimple para SharePoint](#upgrade-or-reinstall-the-storsimple-adapter-for-sharepoint). necessários para a instalação de saudação do tempo de saudação depende do número total de saudação de bancos de dados do SharePoint no farm do SharePoint.

[!INCLUDE [storsimple-install-sharepoint-adapter](../../includes/storsimple-install-sharepoint-adapter.md)]

## <a name="configure-rbs"></a>Configurar RBS
Depois de instalar Olá adaptador StorSimple para SharePoint, configure o RBS conforme descrito em Olá procedimento a seguir.

> [!TIP]
> Olá adaptador StorSimple para SharePoint conecta-se à página de Administração Central do SharePoint hello, permitindo que o RBS toobe habilitado ou desabilitado em cada banco de dados de conteúdo no farm do SharePoint hello. No entanto, habilitar ou desabilitar RBS no banco de dados de conteúdo do hello faz com que uma redefinição de IIS que, dependendo da configuração do farm, pode momentaneamente interromper a disponibilidade Olá de saudação do SharePoint web front-end (WFE). (Fatores como Olá uso de um balanceador de carga de front-end, às cargas de trabalho de servidor atual Olá e assim por diante, podem limitar ou eliminar essa interrupção). tooprotect usuários de uma interrupção, recomendamos que você habilite ou desabilite RBS somente durante uma janela de manutenção planejada.


[!INCLUDE [storsimple-sharepoint-adapter-configure-rbs](../../includes/storsimple-sharepoint-adapter-configure-rbs.md)]

## <a name="configure-garbage-collection"></a>Configurar a coleta de lixo
Quando objetos são excluídos de um site do SharePoint, eles não são excluídos automaticamente da saudação volume de armazenamento RBS. Em vez disso, um assíncrono, o programa de manutenção em segundo plano exclui os BLOBs órfãos do repositório de arquivo hello. Os administradores do sistema podem agendar esse processo toorun periodicamente ou pode iniciá-lo sempre que necessário.

Este programa de manutenção (Microsoft.Data.SqlRemoteBlobs.Maintainer.exe) é instalado automaticamente em todos os servidores SharePoint WFE e servidores de aplicativos quando você habilita RBS. Olá programa está instalado no hello local a seguir: *unidade de inicialização*: \Program Files\Microsoft SQL Remote Blob Storage 10.50\Maintainer\

Para obter informações sobre como configurar e usar o programa de manutenção hello, consulte [manter RBS no SharePoint Server 2013][8].

> [!IMPORTANT]
> programa de manutenção do RBS Olá faz uso de recursos. Você deve agendá-la toorun somente durante períodos de atividade leve no farm do SharePoint hello.


### <a name="delete-orphaned-blobs-immediately"></a>Excluir BLOBs órfãos imediatamente
Se você precisar BLOBs órfãos do toodelete imediatamente, você pode usar o hello instruções a seguir. Observe que essas instruções são um exemplo de como isso pode ser feito em um ambiente do SharePoint 2013 com hello componentes a seguir:

* nome de banco de dados de conteúdo de saudação é WSS_Content.
* nome do SQL Server de saudação é SHRPT13 SQL12\SHRPT13.
* nome do aplicativo web Hello é SharePoint-80.

[!INCLUDE [storsimple-sharepoint-adapter-garbage-collection](../../includes/storsimple-sharepoint-adapter-garbage-collection.md)]

## <a name="upgrade-or-reinstall-hello-storsimple-adapter-for-sharepoint"></a>Atualizar ou reinstalar Olá adaptador StorSimple para SharePoint
Usar Olá após o servidor do procedimento tooupgrade do SharePoint e reinstalar o adaptador StorSimple para SharePoint ou toosimply atualização ou reinstalar o adaptador de saudação em um farm do SharePoint server.

> [!IMPORTANT]
> Revisar Olá informações a seguir antes de tentar tooupgrade o software do SharePoint e/ou atualizar ou reinstalar Olá adaptador StorSimple para SharePoint:
> 
> * Todos os arquivos que foram movidos anteriormente tooexternal armazenamento via RBS não estarão disponível até que Olá reinstalação ser concluída e Olá recurso RBS é habilitado novamente. usuário toolimit afetar, execute qualquer atualização ou reinstalação durante uma janela de manutenção planejada.
> * tempo de saudação necessário para atualização/reinstalação Olá pode variar, dependendo do número total de saudação de bancos de dados do SharePoint no farm de servidores do SharePoint hello.
> * Após a conclusão da atualização/reinstalação hello, você precisa tooenable RBS para bancos de dados de conteúdo do hello. Consulte [Configurar RBS](#configure-rbs) para saber mais.
> * Se você estiver configurando o RBS para um farm do SharePoint que tem um número muito grande de bancos de dados (mais de 200), Olá **Administração Central do SharePoint** página pode atingir o tempo limite. Se isso ocorrer, atualize a página de saudação. Isso não afeta o processo de configuração de saudação.


[!INCLUDE [storsimple-upgrade-sharepoint-adapter](../../includes/storsimple-upgrade-sharepoint-adapter.md)]

## <a name="storsimple-adapter-for-sharepoint-removal"></a>Remoção do Adaptador StorSimple para SharePoint
Olá procedimentos a seguir descreve como toomove Olá BLOBs fazer toohello conteúdos bancos de dados e, em seguida, desinstalar Olá adaptador StorSimple para SharePoint. 

> [!IMPORTANT]
> Você tem toomove Olá BLOBs toohello back bancos de dados antes de desinstalar o software do adaptador hello.


### <a name="before-you-begin"></a>Antes de começar
Colete Olá informações a seguir antes de mover dados saudação fazer toohello conteúdos bancos de dados e começam o processo de remoção do adaptador de saudação:

* Olá nomes de todos os bancos de dados Olá para o qual o RBS está habilitado
* caminho UNC de saudação do hello configurado o armazenamento de BLOB

### <a name="move-hello-blobs-back-toohello-content-databases"></a>Mover Olá BLOBs toohello back conteúdos bancos de dados
Antes de desinstalar o hello adaptador StorSimple para o software do SharePoint, você deve migrar todos Olá BLOBs que foram externalizados toohello backup do SQL Server bancos de dados. Se você tentar toouninstall Olá adaptador StorSimple para SharePoint antes de mover todos os Olá BLOBs toohello back conteúdos bancos de dados, você verá Olá a seguinte mensagem de aviso.

![Mensagem de aviso](./media/storsimple-adapter-for-sharepoint/sasp1.png)

#### <a name="toomove-hello-blobs-back-toohello-content-databases"></a>toomove Olá BLOBs toohello back bancos de dados
1. Baixe cada um dos objetos externalizado de saudação.
2. Olá abrir **Administração Central do SharePoint** página e procurar muito**configurações do sistema**.
3. Em **Azure StorSimple**, clique em **Configurar Adaptador StorSimple**.
4. Em Olá **configurar adaptador do StorSimple** , clique em Olá **desabilitar** botão abaixo de cada Olá bancos de dados que você deseja tooremove do armazenamento BLOB externo. 
5. Excluir objetos de saudação do SharePoint e, em seguida, carregá-los novamente.

Como alternativa, você pode usar o hello Microsoft` RBS Migrate()` cmdlet do PowerShell incluído com o SharePoint. Para saber mais, consulte [Migrar o conteúdo para dentro ou fora do RBS](https://technet.microsoft.com/library/ff628255.aspx).

Depois de mover Olá BLOBs toohello back conteúdo banco de dados, vá toohello próxima etapa: [adaptador de saudação de desinstalação](#uninstall-the-adapter).

### <a name="uninstall-hello-adapter"></a>Desinstalar o adaptador Olá
Depois de mover Olá BLOBs toohello back conteúdos bancos de dados, use um dos Olá seguir opções toouninstall Olá adaptador StorSimple para SharePoint.

#### <a name="toouse-hello-installation-program-toouninstall-hello-adapter"></a>adaptador de saudação toouninstall do programa de instalação de saudação toouse
1. Use uma conta com toolog de privilégios de administrador no servidor de front-end (WFE) toohello web.
2. Clique duas vezes em Olá adaptador StorSimple para o instalador do SharePoint. Olá Assistente de instalação inicia.
   
    ![Assistente de instalação](./media/storsimple-adapter-for-sharepoint/sasp2.png)
3. Clique em **Avançar**. saudação de página a seguir é exibida.
   
    ![Página de remoção do assistente de instalação](./media/storsimple-adapter-for-sharepoint/sasp3.png)
4. Clique em **remover** tooselect processo de remoção de saudação. saudação de página a seguir é exibida.
   
    ![Página de confirmação do assistente de instalação](./media/storsimple-adapter-for-sharepoint/sasp4.png)
5. Clique em **remover** tooconfirm remoção de saudação. Olá após a página de progresso é exibida.
   
    ![Página de progresso do assistente de instalação](./media/storsimple-adapter-for-sharepoint/sasp5.png)
6. Quando a remoção de saudação for concluída, página de conclusão de saudação é exibida. Clique em **concluir** tooclose Olá Assistente de instalação.

#### <a name="toouse-hello-control-panel-toouninstall-hello-adapter"></a>adaptador de saudação do toouse Olá painel de controle toouninstall
1. Abra Olá painel de controle e, em seguida, clique em **programas e recursos**.
2. Selecione **Adaptador StorSimple para SharePoint** e clique em **Desinstalar**.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre o StorSimple](storsimple-overview.md).

<!--Reference links-->
[1]: https://www.microsoft.com/download/details.aspx?id=44073
[2]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[3]: https://technet.microsoft.com/library/ff628583(v=office.14).aspx
[4]: https://technet.microsoft.com/library/ff628569(v=office.14).aspx
[5]: https://technet.microsoft.com/library/ff628583(v=office.15).aspx
[8]: https://technet.microsoft.com/en-us/library/ff943565.aspx

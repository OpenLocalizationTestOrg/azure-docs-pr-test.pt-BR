---
title: aaaReplicate um IIS multicamado com base em aplicativo web usando o Azure Site Recovery | Microsoft Docs
description: "Este artigo descreve como tooreplicate IIS web farm máquinas de virtuais usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Replicar um aplicativo Web baseado em IIS de várias camadas usando o Azure Site Recovery

## <a name="overview"></a>Visão geral


Software de aplicativo é o mecanismo de saudação de produtividade de negócios em uma organização. Vários aplicativos Web podem servir para propósitos diferentes em uma organização. Alguns deles, como processamento de folha de pagamento, aplicativos financeiros e sites voltados para o cliente podem ser essenciais para uma organização. É importante para Olá organização toohave-los para cima e em execução com perda de tooprevent de todos os tempos de produtividade e mais importante evitar qualquer imagem de marca toohello danos da organização hello.

Aplicativos web críticos geralmente são definidos como aplicativos de várias camadas com Olá web, o banco de dados e o aplicativo em diferentes camadas. Seja espalhada em várias camadas, além de aplicativos de saudação também podem usar vários servidores em cada camada tooload Olá balancear. Além disso, os mapeamentos de saudação entre várias camadas e no servidor de web hello podem ser baseados em endereços IP estáticos. Durante o failover, alguns destes mapeamentos precisará toobe atualizado, especialmente, se você tiver vários sites configurados no servidor de web hello. No caso de aplicativos web usando SSL, associações de certificado serão necessário toobe atualizado.

Métodos tradicionais de recuperação baseados em replicação não envolvem fazendo backup de vários arquivos de configuração, as configurações do registro, associações, componentes personalizados (COM ou .NET), conteúdo e também certificados e recuperar arquivos Olá por meio de um conjunto de etapas manuais. Está claro que essas técnicas são inconvenientes, propensas a erros e não escalonáveis. Ele é, por exemplo, facilmente possível tooforget fazendo backup de certificados e ficar com nenhuma opção mas toobuy novos certificados para o servidor de saudação após o failover.

Uma solução de recuperação de desastres BOM, deve permitir modelagem de planos de recuperação em torno de saudação acima arquiteturas de aplicativos complexos e também ter Olá capacidade tooadd personalizado etapas toohandle aplicativo mapeamentos entre várias camadas, portanto, fornecendo um Clique se captura solução no evento de saudação de um desastre esquerda tooa reduzir o RTO.


Este artigo descreve como tooprotect um IIS com base em aplicativo web usando um [do Azure Site Recovery](site-recovery-overview.md). Este artigo aborda as práticas recomendadas para a replicação de uma camada de três IIS com base tooAzure de aplicativo web, como você pode fazer uma simulação de recuperação de desastres e como é possível o failover Olá aplicativo tooAzure.


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, certifique-se de que compreender o seguinte hello:

1. [Replicando tooAzure uma máquina virtual](site-recovery-vmware-to-azure.md)
1. Como muito[criar uma rede de recuperação](site-recovery-network-design.md)
1. [Fazer um tooAzure de failover de teste](./site-recovery-test-failover-to-azure.md)
1. [Fazer um failover tooAzure](site-recovery-failover.md)
1. Como muito[replicar um controlador de domínio](site-recovery-active-directory.md)
1. Como muito[replicar do SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Padrões de implantação
Um aplicativo de web do IIS com base em geralmente segue uma saudação padrões de implantação a seguir:

**Padrão de implantação 1** Um farm da Web baseado no IIS com ARR (Application Request Routing), o Servidor IIS e o Microsoft SQL Server.

![Padrão de implantação](./media/site-recovery-iis/deployment-pattern1.png)

**Padrão de implantação 2** Um farm da Web baseado no IIS com ARR (Application Request Routing), o Servidor IIS, Servidor de Aplicativos e o Microsoft SQL Server.


![Padrão de implantação](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Suporte do Site Recovery

Para fins de saudação de criação neste artigo as máquinas virtuais VMware com o servidor IIS versão 7.5 no Windows Server 2012 R2 Enterprise foram usados. Como a replicação de recuperação de site é independente do aplicativo, recomendações Olá fornecidos aqui são apenas toohold esperado nos seguintes cenários de e para uma versão diferente do IIS.

### <a name="source-and-target"></a>Origem e destino

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sim | Sim
**VMware** | Sim | Sim
**Servidor físico** | Não | Sim

## <a name="replicate-virtual-machines"></a>Replicar máquinas virtuais

Execute [neste guia](site-recovery-vmware-to-azure.md) toostart replicando todas as Olá IIS web farm máquinas virtuais tooAzure.

Se você estiver usando um endereço IP estático, especifique Olá IP que você deseja Olá tootake de máquina virtual em Olá [ **IP de destino** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) configuração em configurações de rede e computação.

![IP de Destino](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação

Um plano de recuperação permite sequenciamento Olá failover de várias camadas em um aplicativo de várias camada, assim, manter a consistência do aplicativo. Siga Olá etapas a seguir ao criar um plano de recuperação para um aplicativo web de várias camadas.  [Saiba mais sobre a criação de um plano de recuperação](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>A adição de grupos de toofailover de máquinas virtuais
Um aplicativo de web IIS de várias camado típico consiste em uma camada de banco de dados com máquinas virtuais do SQL, camada da web de saudação constituído por um servidor do IIS e uma camada de aplicativo. Adicione todos os grupo de toodifferent essas máquinas virtuais com base na camada como abaixo. [Saiba mais sobre como personalizar o plano de recuperação](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Crie um plano de recuperação. Adicione máquinas virtuais de camada de banco de dados Olá em 1 grupo tooensure que eles são desligadas última e colocado primeiro.

1. Adicione máquinas virtuais de camada de aplicativo hello sob o grupo 2, de modo que eles sejam ativados após a camada de banco de dados de saudação foram ativada.

1. Adicione máquinas virtuais do Olá web camada no grupo 3, de modo que eles sejam ativados depois de camada de aplicativo hello foram ativada.

1. Adicione balancear a carga de máquinas virtuais no grupo 4, de modo que eles sejam ativados depois da camada de dados da web hello foram ativada.


### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar plano de recuperação de toohello de scripts
Talvez seja necessário toodo algumas operações em máquinas virtuais do Azure post/teste de failover failover toomake função do IIS web farm de saudação corretamente. Você pode automatizar a operação de failover Olá post como atualizar a entrada DNS, alterando a associação do site, alterações na cadeia de caracteres de conexão adicionando scripts correspondentes no plano de recuperação hello como abaixo. [Saiba mais sobre como adicionar script ao plano de recuperação](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>Atualização de DNS
Se Olá DNS é configurado para a atualização dinâmica de DNS máquinas virtuais normalmente atualizar Olá DNS com hello novo IP quando eles são iniciados. Se desejar tooadd um tooupdate etapa explícita DNS com hello novos IPs de máquinas virtuais de hello, em seguida, adicione isso [script tooupdate IP no DNS](https://aka.ms/asr-dns-update) como uma ação de postagem em grupos do plano de recuperação.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Cadeia de conexão no web.config do aplicativo
cadeia de caracteres de conexão de saudação especifica o banco de dados Olá Olá site da web se comunica com.

Se cadeia de caracteres de conexão Olá assume o nome de saudação da máquina de virtual de banco de dados hello, nenhuma etapa adicional será necessária post failover e aplicativo hello poderá tooautomatically se comunicam toohello banco de dados. Além disso, se o endereço IP Olá Olá máquina de virtual de banco de dados é mantido, não será necessária a cadeia de caracteres de conexão do tooupdate hello. Se a cadeia de caracteres de conexão de saudação refere-se a máquina de virtual de banco de dados toohello usando um endereço IP, será necessário toobe atualizado após failover. Por exemplo Olá abaixo de cadeia de caracteres de conexão aponta toohello banco de dados com IP 127.0.1.2

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

Você pode atualizar a cadeia de caracteres de conexão de saudação na camada da web adicionando [script de atualização de conexão do IIS](https://aka.ms/asr-update-webtier-script-classic) após o grupo 3 no plano de recuperação de saudação.

#### <a name="site-bindings-for-hello-application"></a>Ligações do site para o aplicativo hello
Cada site consiste em informações que incluem o tipo de saudação de associação, o endereço IP de Olá no qual Olá servidor IIS escuta solicitações de toohello para site hello, número da porta hello e nomes de host de saudação do site Olá de associação. Em tempo de saudação de um failover, essas associações talvez seja necessário toobe atualizado se houver uma alteração no endereço IP hello associado a eles.

> [!NOTE]
>
> Se você tiver marcado como 'all unassigned' para associação do site Olá exemplo hello abaixo, você não precisará tooupdate esse failover de postagem de associação. Além disso, se o endereço IP de saudação associado a um site não for alterado após failover, associação do site Olá necessário não ser atualizada (retenção de endereço IP hello depende da arquitetura de rede hello e sub-redes atribuído toohello sites primário e de recuperação e, portanto, podem ou não seja viável para sua organização.)

![Associação de SSL](./media/site-recovery-iis/sslbinding.png)

Se você associou o endereço IP de saudação com um site, você precisará tooupdate todas as associações de site com o novo endereço IP hello. Você pode adicionar [script de atualização da camada da Web do IIS](https://aka.ms/asr-web-tier-update-runbook-classic) após o grupo 3 em associações de site saudação do toochange de plano de recuperação.


#### <a name="update-load-balancer-ip-address"></a>Atualizar o endereço IP do balanceador de carga
Se você tiver máquina de virtual Application Request Routing, adicione [script de failover de ARR IIS](https://aka.ms/asr-iis-arrtier-failover-script-classic) após o endereço IP do grupo 4 tooupdate hello.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>associação de certificado SSL Olá para uma conexão https
Sites podem ter um certificado SSL associado que ajuda a garantir uma comunicação segura entre Olá servidorweb e navegador saudação do usuário. Se o site Olá tem uma conexão https e um endereço IP https associado site associação toohello saudação do servidor do IIS com uma associação de certificado SSL, uma nova associação de site precisará toobe adicionado cert Olá com hello IP da máquina de virtual IIS Olá após o failover.

certificado SSL Olá pode ser emitido em relação a-

um) nome de domínio totalmente qualificado de Olá do site Olá<br>
b) nome saudação do servidor de saudação<br>
c) um certificado curinga para o nome de domínio Olá<br>
d) um endereço IP – se o certificado SSL da saudação é feito em IP hello saudação do servidor do IIS, outro toobe de necessidades de certificado SSL emitido para o endereço IP de saudação do hello servidor IIS em Olá site do Azure e uma associação de SSL adicional para este certificado será necessário toobe criado. Portanto, é aconselhável toonot usar um certificado SSL emitido em IP. Essa é uma opção menos usada e em breve será substituída de acordo com as novas alterações na CA/fórum do navegador.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Atualização Olá dependência entre Olá web e a camada de aplicativo hello
Se você tiver uma dependência específicas de aplicativo com base no endereço IP hello de máquinas virtuais de saudação, você precisa tooupdate esse failover de postagem de dependência.

## <a name="doing-a-test-failover"></a>Executar um failover de teste
Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de serviço.
1.  Clique no plano de recuperação de saudação criado para o farm da web do IIS.
1.  Clique em 'Failover de Teste'.
1.  Selecione o ponto de recuperação e o processo de failover de teste do rede virtual do Azure toostart hello.
1.  Após ambiente secundário hello, você pode executar a validação.
1.  Depois que as validações de saudação estiverem concluídas, você pode selecionar 'Validações Concluir' e ambiente de failover de teste hello serão limpos.

## <a name="doing-a-failover"></a>Executar um failover
Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de serviço.
1.  Clique no plano de recuperação de saudação criado para o farm da web do IIS.
1.  Clique em 'Failover'.
1.  Selecione o processo de failover de saudação de toostart de ponto de recuperação.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [replicar outros aplicativos](site-recovery-workload.md) usando o Site Recovery.

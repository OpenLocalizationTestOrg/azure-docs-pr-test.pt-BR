---
title: "funcionalidade do sistema aaaOperating no serviço de aplicativo do Azure"
description: "Saiba mais sobre Olá SO funcionalidade disponível tooweb aplicativos back-ends dos aplicativos móveis e aplicativos de API no serviço de aplicativo do Azure"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Funcionalidade do sistema operacional no Serviço de Aplicativo do Azure
Este artigo descreve Olá comuns da linha de base funcionalidade do sistema operacional que está disponível tooall aplicativos executados em [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Essa funcionalidade inclui acesso a arquivos, redes e registros, além de logs de diagnóstico e eventos. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Camadas de plano do Serviço de Aplicativo
O Serviço de Aplicativo executa aplicativos do cliente em um ambiente de hospedagem multilocatário. Aplicativos implantados em Olá **livre** e **compartilhado** camadas executado em processos de trabalho em máquinas virtuais compartilhadas, enquanto os aplicativos implantados no hello **padrão** e  **Premium** camadas executados em máquinas virtuais dedicadas especificamente para aplicativos de saudação associados a um único cliente.

Como o serviço de aplicativo oferece suporte a uma experiência perfeita de dimensionamento entre níveis diferentes, a configuração de segurança Olá imposta para saudação do serviço de aplicativo aplicativos permanece mesmo. Isso garante que aplicativos não repentinamente se comportam de maneira diferente, falha de maneiras inesperadas, quando o plano de serviço de aplicativo alterna de uma camada tooanother.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Estruturas de desenvolvimento
Quantidade de saudação de controle de camadas de recursos de computação (CPU, armazenamento em disco, memória e saída de rede) de preços do serviço de aplicativo tooapps disponíveis. No entanto, a amplitude de saudação do framework funcionalidade disponível tooapps permanece Olá que mesmo independentemente do hello níveis de dimensionamento.

O Serviço de Aplicativo dá suporte a várias estruturas de desenvolvimento, inclusive ASP.NET, ASP clássico, node.js, PHP e python, todas executadas como extensões no IIS. Em ordem toosimplify e normalizar a configuração de segurança, aplicativos de serviço de aplicativo geralmente são executados Olá várias estruturas de desenvolvimento com suas configurações padrão. Uma abordagem tooconfiguring aplicativos podem ter sido área da superfície toocustomize Olá API e a funcionalidade para cada estrutura de desenvolvimento individuais. Em vez disso, o Serviço de Aplicativo utiliza uma abordagem mais genérica, habilitando uma linha de base comum de funcionalidade do sistema operacional, independentemente da estrutura de desenvolvimento do aplicativo.

Olá seções a seguir resumem tipos gerais de saudação de aplicativos de serviço do sistema operacional funcionalidade tooApp disponíveis.

<a id="FileAccess"></a>

## <a name="file-access"></a>Acesso a arquivos
Existem diversas unidades dentro do Serviço de Aplicativo, incluindo unidades locais e unidades de rede.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Unidades locais
Essencialmente, o serviço de aplicativo é um serviço executado sobre a infraestrutura do Azure PaaS (plataforma como serviço) de saudação. Como resultado, unidades locais de saudação que "conectado" máquina virtual de tooa é hello mesma função de trabalho unidade tipos tooany disponíveis em execução no Azure. Isso inclui uma unidade do sistema operacional (Olá unidade D:\), uma unidade de aplicativo que contém os arquivos do pacote do Azure cspkg usados exclusivamente pelo serviço de aplicativo (e toocustomers inacessível) e uma unidade de "usuário" (Olá unidade C:\), cujo tamanho varia dependendo do tamanho de saudação de hello VM.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Unidades de rede (também conhecidas como compartilhamentos UNC)
Um dos aspectos de saudação exclusivo do aplicativo de serviço que facilita a manutenção e implantação de aplicativos é que todo o conteúdo de usuário é armazenado em um conjunto de compartilhamentos UNC. Esse modelo perfeitamente mapeia toohello o padrão comum de armazenamento de conteúdo usado pelo local de hospedagem na web ambientes com vários servidores com balanceamento de carga. 

No Serviço de Aplicativo, existem vários compartilhamentos UNC criados em cada datacenter. Uma porcentagem do conteúdo de usuário Olá para todos os clientes em cada data center é alocada tooeach compartilhamento UNC. Além disso, todo o conteúdo do arquivo hello para assinatura de um único cliente sempre é colocada no hello compartilhamento UNC mesmo. 

Observe que, devido a serviços de nuvem toohow funcionam, Olá máquina virtual específica responsável para hospedar um compartilhamento UNC será alterado ao longo do tempo. É garantido que compartilhamentos UNC serão montados por máquinas virtuais diferentes conforme eles são abertos para cima e para baixo durante o curso normal de saudação de operações de nuvem. Por esse motivo, aplicativos nunca devem fazer suposições embutido que informações da máquina Olá em um caminho de arquivo UNC permanece estáveis ao longo do tempo. Em vez disso, eles devem usar Olá conveniente *falso* caminho absoluto **D:\home\site** que fornece o serviço de aplicativo. Esse caminho absoluto falso fornece um método portátil, independente de aplicativo e usuário para referir-se o aplicativo do tooone. Usando **D:\home\site**, um pode transferir arquivos compartilhados de tooapp do aplicativo sem ter que tooconfigure um novo caminho absoluto para cada transferência.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Tipos de arquivo acesso concedido tooan aplicativo
A assinatura de cada cliente tem uma estrutura de diretório reservado em um compartilhamento UNC específico dentro de um data center. Um cliente pode ter vários aplicativos criados em um data center específico, para que todos os diretórios de saudação pertencentes a assinatura de cliente único tooa são criados no hello mesmo compartilhamento UNC. compartilhamento de saudação pode incluir diretórios, como aqueles de conteúdo, erro e logs de diagnóstico e versões anteriores do aplicativo hello criado pelo controle de origem. Conforme o esperado, os diretórios de aplicativo do cliente estão disponíveis para acesso de leitura e gravação em tempo de execução pelo código do aplicativo do aplicativo hello.

Em Olá unidades locais conectado toohello máquina de virtual que executa um aplicativo, serviço de aplicativo reserva uma parte do espaço no hello unidade C:\ para armazenamento temporário de local específico do aplicativo. Embora um aplicativo tenha acesso de leitura/gravação completa tooits possui temporário armazenamento local, que o armazenamento não é realmente pretendido toobe usada diretamente pelo código do aplicativo hello. Em vez disso, a intenção de saudação é tooprovide armazenamento de arquivo temporário para estruturas de aplicativo web e o IIS. Serviço de aplicativo também limita a quantidade de saudação de local de armazenamento temporário disponíveis tooeach aplicativo tooprevent aplicativos individuais consuma quantidades excessivas de armazenamento de arquivo local.

Dois exemplos de como o serviço de aplicativo usa o armazenamento local temporário são directory Olá para arquivos temporários do ASP.NET e diretório de saudação do IIS em arquivos compactados. Olá sistema de compilação do ASP.NET usa o diretório de "Arquivos temporários do ASP.NET" hello como um local de cache temporário de compilação. O IIS usa hello "IIS compactado arquivos temporários" diretório de saída da resposta de toostore compactado. Ambos os tipos de arquivo uso (assim como outras) são remapeados no armazenamento local temporário do tooper aplicativo do serviço de aplicativo. Esse remapeamento garante que a funcionalidade continua conforme esperado.

Cada aplicativo no serviço de aplicativo é executado como uma identidade de processo do operador de com poucos privilégios exclusivo aleatório chamado hello "identidade pool de aplicativos", mais descrita aqui: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Código do aplicativo usa essa identidade para a unidade do sistema operacional do acesso somente leitura básico toohello (Olá unidade D:\). Isso significa que o código do aplicativo pode listar estruturas de diretório comuns e ler arquivos comuns na unidade do sistema operacional. Embora isso podem aparecer toobe um nível um pouco mais amplo de acesso, Olá mesmos diretórios e arquivos são acessíveis quando você provisiona uma função de trabalho em um Azure serviço hospedado e ler o conteúdo da unidade hello. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Acesso a arquivos em várias instâncias
diretório base Olá contém conteúdo do aplicativo e o código do aplicativo pode gravar tooit. Se um aplicativo é executado em várias instâncias, diretório base Olá é compartilhado entre todas as instâncias para que todas as instâncias consulte Olá mesmo diretório. Portanto, por exemplo, se um aplicativo salva o diretório base do toohello arquivos carregados, esses arquivos são instâncias tooall imediatamente disponíveis. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Acesso à rede
Código do aplicativo pode usar o TCP/IP e UDP com base em protocolos toomake saída rede conexões tooInternet acessível pontos de extremidade que expõem serviços externos. Os aplicativos podem usar esses protocolos tooconnect tooservices mesmo dentro do Azure &#151; por exemplo, ao estabelecer conexões de HTTPS tooSQL banco de dados.

Também há uma funcionalidade limitada para conexão de loopback local um tooestablish de aplicativos, e ter um aplicativo escutar no soquete que loopback local. Esse recurso existe principalmente tooenable aplicativos que escutam em soquetes de loopback local como parte de sua funcionalidade. Observe que cada aplicativo vê uma conexão de loopback "private"; o aplicativo "A" não é possível escutar tooa loopback local soquete estabelecida pelo aplicativo "B".

Os pipes nomeados também são compatíveis como um mecanismo de comunicação entre processos (IPC) entre processos diferentes que executam coletivamente um aplicativo. Por exemplo, módulo FastCGI do IIS de saudação depende de pipes nomeados toocoordinate Olá processos individuais que executar as páginas do PHP.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Execução de código, processos e memória
Conforme observado anteriormente, os aplicativos são executados em processos de trabalho com poucos privilégios usando uma identidade de pool de aplicativos aleatória. Código do aplicativo tem espaço de memória do access toohello associado com o processo de trabalho hello, bem como os processos filho que podem ser gerados por outros aplicativos ou processos CGI. No entanto, um aplicativo não pode acessar a memória de saudação ou Olá de dados de outro aplicativo mesmo se ele estiver na mesma máquina virtual.

Os aplicativos podem executar scripts ou páginas gravadas com estruturas de desenvolvimento na Web com suporte. Serviço de aplicativo não configurar qualquer modos de toomore restringido de configurações de estrutura da web. Por exemplo, aplicativos ASP.NET em execução no serviço de aplicativo executado em confiança "completa" como modo de confiança tooa contrário mais restringido. Estruturas da Web, incluindo o ASP clássico e o ASP.NET, podem chamar componentes COM no processo (mas não a saída de componentes do processo COM) como o ADO (ActiveX Data Objects) que são registrados por padrão no sistema de operacional do Windows hello.

Os aplicativos podem gerar e executar códigos arbitrários. É permitido para itens de toodo um aplicativo como gerar um shell de comando ou executa um script do PowerShell. No entanto, mesmo que processos e um código arbitrário podem ser gerados a partir de um aplicativo, programas executáveis e scripts são restritas ainda toohello privilégios concedidos toohello pai pool de aplicativos. Por exemplo, um aplicativo pode gerar um executável que faz uma chamada de saída HTTP, mas esse mesmo executável não é possível tentar o endereço IP de saudação toounbind de uma máquina virtual de seu NIC. Fazer uma chamada de rede de saída é permitido com privilégios toolow código, mas tentar tooreconfigure as configurações de rede em uma máquina virtual requer privilégios administrativos.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Logs de diagnóstico e eventos
Informações de log são outro conjunto de dados que alguns aplicativos de tentam de tooaccess. tipos de saudação de toocode disponíveis de informações de log em execução no serviço de aplicativo inclui diagnósticos e log informações geradas por um aplicativo que também é facilmente acessível toohello aplicativo. 

Por exemplo, logs de HTTP do W3C gerados por um aplicativo ativo estão disponíveis em um diretório de log na rede Olá compartilhar local criado para o aplicativo hello, ou disponível no armazenamento de blob, se um cliente tiver configurado o log W3C toostorage. Olá última opção permite grandes quantidades de toobe logs coletados sem o risco de saudação do exceder os limites de armazenamento de arquivo hello associados a um compartilhamento de rede.

Do mesmo modo, o diagnóstico em tempo real, informações de aplicativos .NET também podem ser registradas com hello .NET diagnóstico e rastreamento de infraestrutura, com opções toowrite Olá do aplicativo do rastreamento informações tooeither hello ou compartilhamento de rede, como alternativa tooa o armazenamento de blob local.

Áreas de diagnóstico log e rastreamento que não está disponíveis tooapps são eventos ETW do Windows e logs de eventos comuns do Windows (por exemplo, sistema, aplicativo e segurança logs de eventos). Como as informações de rastreamento ETW potencialmente podem estar visíveis eventos de tooETW de acesso de leitura e gravação de todo o computador (com o direito de saudação ACLs), são bloqueados. Os desenvolvedores podem observar essa API chama tooread e gravar eventos ETW e logs de eventos comuns do Windows aparecer toowork, mas isso é porque o serviço de aplicativo é "falsificação" hello chamadas para que elas apareçam toosucceed. Na realidade, o código do aplicativo hello não possui acesso toothis evento dados.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Acesso ao Registro
Aplicativos têm acesso somente leitura toomuch (mas não todos) do registro de saudação da máquina virtual de saudação estiverem sendo executados em. Na prática, isso significa que as chaves de registro que permitem que o grupo de usuários local toohello acesso somente leitura são acessíveis por aplicativos. Uma área do registro Olá que atualmente não tem suporte para leitura ou acesso de gravação é hello HKEY\_atual\_hive do usuário.

Registro de toohello de acesso de gravação está bloqueado, incluindo as chaves de registro do acesso tooany por usuário. Da perspectiva do aplicativo hello, acesso de gravação toohello registro deve nunca ser confiado no ambiente do Azure de saudação como aplicativos podem (e fazer) serão migrados máquinas virtuais diferentes. Olá somente gravável armazenamento persistente que pode ser depende de um aplicativo é a estrutura de diretório de conteúdo por aplicativo hello armazenada em compartilhamentos UNC do serviço de aplicativo de saudação. 

## <a name="more-information"></a>Mais informações

[Área restrita de aplicativo Web do Azure](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -Olá a maioria das informações atualizadas sobre o ambiente de execução de saudação do serviço de aplicativo. Esta página é mantida diretamente pelo Olá, equipe de desenvolvimento de aplicativo de serviço.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 



---
title: "aaaData Gateway de gerenciamento de fábrica de dados | Microsoft Docs"
description: Configurar um gateway toomove de dados entre locais e hello nuvem. Use o Gateway de gerenciamento de dados no Azure Data Factory toomove seus dados.
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a>Gateway de gerenciamento de dados
gateway de gerenciamento de dados de saudação é um agente de cliente que você deve instalar em seus dados de toocopy do ambiente local entre armazenamentos de dados locais e de nuvem. Olá dados repositórios com suporte pela fábrica de dados são listados no hello local [suporte para fontes de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) seção.

Este artigo complementa Olá passo a passo em Olá [mover dados entre locais e na nuvem armazenamentos de dados](data-factory-move-data-between-onprem-and-cloud.md) artigo. Olá instruções passo a passo, você criará um pipeline que usa Olá gateway toomove dados de um tooan de banco de dados do SQL Server local BLOBs do Azure. Este artigo fornece informações detalhadas de detalhada sobre o gateway de gerenciamento de dados de saudação. 

Você pode expandir um gateway de gerenciamento de dados por meio da associação várias máquinas locais com o gateway de saudação. Você pode escalar verticalmente com o aumento do número de trabalhos de movimentação de dados que podem ser executados simultaneamente em um nó. Esse recurso também está disponível para um gateway lógico com um único nó. Consulte o artigo [Escalar o Gateway de Gerenciamento de Dados no Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) para obter detalhes.

> [!NOTE]
> Atualmente, o gateway suporta apenas a atividade de cópia de saudação e a atividade de procedimento armazenado na fábrica de dados. Não é possível toouse gateway de saudação uma atividade personalizada tooaccess locais de fontes de dados.      

## <a name="overview"></a>Visão geral
### <a name="capabilities-of-data-management-gateway"></a>Funcionalidades do Gateway de Gerenciamento de Dados
Gateway de gerenciamento de dados fornece Olá recursos a seguir:

* Modelo de fontes de dados locais e fontes de dados de nuvem dentro Olá mesma fábrica de dados e movem dados.
* Ter um único painel de controle para monitoramento e gerenciamento com visibilidade do status do gateway da página de fábrica de dados hello.
* Gerencie fontes de dados do access tooon local com segurança.
  * Nenhuma alteração necessária toocorporate firewall. Gateway faz apenas conexões de saída com base em HTTP tooopen internet.
  * Criptografar credenciais para seus armazenamentos de dados locais com seu certificado.
* Mover dados com eficiência – os dados são transferidos no toointermittent paralela e resiliente a problemas de rede com lógica de repetição automática.

### <a name="command-flow-and-data-flow"></a>Fluxo de comando e fluxo de dados
Quando você usa um copiar atividade toocopy dados entre locais e na nuvem, a atividade de saudação usa dados de tootransfer um gateway do toocloud de fonte de dados local e vice-versa.

Aqui está Olá fluxo de dados de alto nível para e resumo das etapas para a cópia com o gateway de dados: ![fluxo de dados usando o gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)

1. Desenvolvedor de dados cria um gateway para uma fábrica de dados do Azure usando o hello [portal do Azure](https://portal.azure.com) ou [Cmdlet do PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).
2. Desenvolvedor de dados cria um serviço vinculado para um repositório de dados local, especificando o gateway hello. Como parte da configuração saudação do serviço vinculado, o desenvolvedor de dados usa as credenciais e tipos de autenticação Olá definindo credenciais aplicativo toospecify.  caixa de diálogo do aplicativo se comunica com dados de saudação do Hello definindo credenciais armazenar tootest conexão e hello toosave credenciais do gateway.
3. Gateway criptografa credenciais Olá com certificado Olá associado gateway hello (fornecido pelo desenvolvedor de dados), antes de salvar credenciais Olá na nuvem hello.
4. Serviço de fábrica de dados se comunica com o gateway Olá para agendamento e gerenciamento de trabalhos através de um canal de controle que usa uma fila do barramento do serviço compartilhado do Azure. Quando um trabalho de atividade de cópia precisa toobe foi iniciada, Data Factory filas solicitação Olá juntamente com informações de credenciais. Gateway inicia o trabalho de saudação após sondagem Olá fila.
5. gateway Olá descriptografa as credenciais de saudação com hello mesmo certificado e, em seguida, conecta-se o repositório de dados do local de toohello com as credenciais e o tipo de autenticação adequada.
6. gateway Olá copia dados de um armazenamento de nuvem no local repositório tooa, ou vice-versa dependendo de como hello atividade de cópia é configurado no pipeline de saudação de dados. Nesta etapa, gateway Olá se comunica diretamente com os serviços de armazenamento baseado em nuvem, como o armazenamento de BLOBs do Azure por um canal seguro de (HTTPS).

### <a name="considerations-for-using-gateway"></a>Considerações para o uso do gateway
* Uma única instância do Gateway de Gerenciamento de Dados pode ser usada para várias fontes de dados locais. No entanto, **uma única instância do gateway é uma fábrica de dados do Azure associado tooonly** e não pode ser compartilhada com outro fábrica de dados.
* Você pode ter **apenas uma instância do Gateway de Gerenciamento de Dados** instalada em um único computador. Suponha que, você tem duas fábricas de dados que precisam de fontes de dados do tooaccess no local, você precisa tooinstall gateways em computadores de dois locais. Em outras palavras, um gateway é tooa empatados fábrica de dados específicos
* Olá **gateway não precisa toobe em Olá mesmo computador como fonte de dados Olá**. No entanto, com a fonte de dados de toohello mais próximo do gateway reduz o tempo de Olá Olá gateway tooconnect toohello fonte de dados. É recomendável que você instale o gateway de saudação em um computador diferente do hello uma fonte de dados local hosts. Quando Olá gateway e fonte de dados estiverem em computadores diferentes, o gateway de saudação não disputam os recursos com a fonte de dados.
* Você pode ter **vários gateways em máquinas diferentes conectando toohello mesma fonte de dados local**. Por exemplo, você pode ter dois gateways que atende as fábricas de duas dados mas Olá a mesma fonte de dados local está registrado com ambas as fábricas de dados hello.
* Se você já tiver um gateway instalado no computador atendendo um cenário do **Power BI**, instale um gateway **separado para o Azure Data Factory** em outro computador.
* O gateway deve ser usado mesmo quando você usar o **ExpressRoute**.
* Trate a fonte de dados como local (isto é, protegida por um firewall) mesmo quando você usar o **ExpressRoute**. Use Olá gateway tooestablish conectividade entre o serviço hello e fonte de dados de saudação.
* Você deve **usar gateway Olá** mesmo se Olá repositório de dados está na nuvem de saudação em uma **Azure IaaS VM**.

## <a name="installation"></a>Instalação
### <a name="prerequisites"></a>Pré-requisitos
* Olá suportada **sistema operacional** versões são Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2. Instalação do gateway de gerenciamento de dados de saudação em um controlador de domínio não é suportada atualmente.
* O .NET framework 4.5.1 ou superior é necessário. Se você estiver instalando o gateway em um computador com Windows 7, instale o .NET Framework 4.5 ou posterior. Confira [Requisitos de sistema do .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) para obter detalhes.
* Olá recomendado **configuração** máquina de gateway de saudação é pelo menos 2 GHz, 4 núcleos, 8 GB de RAM e 80 GB de disco.
* Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata. Portanto, configurar adequados **plano de energia** no computador de saudação antes de instalar o gateway de saudação. Se máquina Olá for toohibernate configurado, instalação do gateway Olá solicita uma mensagem.
* Você deve ser um administrador no hello máquina tooinstall e configurar o gateway de gerenciamento de dados de saudação com êxito. Você pode adicionar usuários adicionais toohello **gateway de gerenciamento de dados usuários** grupo local do Windows. membros desse grupo Olá são Olá capaz de toouse **Gerenciador de configuração de Gateway de gerenciamento de dados** gateway de saudação tooconfigure ferramenta.

Como copiar atividade executa acontecer em uma frequência específica, hello uso de recursos (CPU, memória) no computador de saudação também segue Olá mesmo padrão com o horário de pico e ocioso. Utilização de recursos também depende intensamente Olá quantidade de dados que está sendo movidos. Quando vários trabalhos de cópia estiverem em andamento, você verá o uso do recurso aumentar durante horários de pico.

### <a name="installation-options"></a>Opções de instalação
Gateway de gerenciamento de dados pode ser instalado em Olá maneiras a seguir:

* Ao baixar um pacote de instalação do MSI da saudação [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).  Olá MSI também pode ser usado tooupgrade existente dados gerenciamento gateway toohello versão mais recente, com todas as configurações preservadas.
* Clicando no link **Baixar e instalar o gateway de dados** em INSTALAÇÃO MANUAL ou **Instalar diretamente neste computador** em INSTALAÇÃO EXPRESSA. Veja o artigo [Mover dados entre locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo sobre como usar a instalação expressa. etapa manual Olá leva toohello Centro de download.  Olá instruções para baixar e instalar o gateway de saudação do Centro de download são na próxima seção, Olá.

### <a name="installation-best-practices"></a>Práticas recomendadas de instalação:
1. Configure plano de energia no computador de host Olá para o gateway de saudação para que hello máquina não entra em hibernação. Se a máquina de host Olá hibernação, gateway Olá não responde solicitações toodata.
2. Fazer backup de certificado Olá associado Olá gateway.

### <a name="install-hello-gateway-from-download-center"></a>Instalar o gateway de saudação do Centro de download
1. Navegue muito[página de download da Microsoft Data Management Gateway](https://www.microsoft.com/download/details.aspx?id=39717).
2. Clique em **baixar**, selecione Olá versão apropriada (**32-bit** vs. **64 bits**) e clique em **Avançar**.
3. Executar Olá **MSI** diretamente ou salvá-lo tooyour disco e execute.
4. Em Olá **bem-vindo** página, selecione um **idioma** clique **próximo**.
5. **Aceitar** Olá contrato de licença de usuário final e clique em **próximo**.
6. Selecione **pasta** tooinstall Olá gateway e clique em **próximo**.
7. Em Olá **tooinstall pronto** , clique em **instalar**.
8. Clique em **concluir** toocomplete instalação.
9. Obter chave de saudação do hello portal do Azure. Consulte a próxima seção Olá para obter instruções passo a passo.
10. Em Olá **registrar gateway** página de **Gerenciador de configuração de Gateway de gerenciamento de dados** em execução no seu computador, Olá seguintes etapas:
    1. Cole a chave de saudação em texto de saudação.
    2. Opcionalmente, clique em **chave do gateway Mostrar** texto da tecla toosee hello.
    3. Clique em **Registrar**.

### <a name="register-gateway-using-key"></a>Registrar gateway usando chave
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a>Se você já não criou um gateway lógico no portal de saudação
toocreate um gateway na chave de saudação de portal e get hello da saudação **configurar** página, execute estas etapas do passo a passo em Olá [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a>Se você já tiver criado o gateway lógico Olá no portal de saudação
1. No portal do Azure, navegue até toohello **Data Factory** página e, em seguida, clique em **serviços vinculados** lado a lado.

    ![Página Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. Em Olá **serviços vinculados** página, selecione Olá lógica **gateway** criado no portal de saudação.

    ![gateway lógico](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. Em Olá **Gateway de dados** , clique em **baixar e instalar o gateway de dados**.

    ![Baixe o link no portal de saudação](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. Em Olá **configurar** , clique em **chave recrie**. Clique em Sim na mensagem de saudação do aviso depois de ler cuidadosamente.

    ![Recriar chave](media/data-factory-data-management-gateway/recreate-key-button.png)
5. Clique em copiar botão Avançar toohello chave. chave de saudação é toohello copiado na área de transferência.

    ![Copiar chave](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a>Ícones/notificações da bandeja do sistema
Olá imagem a seguir mostra algumas das Olá ícones da bandeja do que você vê.

![ícones da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

Se você mover o cursor sobre a mensagem de ícone e notificação da bandeja de sistema hello, você verá detalhes sobre o estado de saudação da operação de atualização do gateway de saudação em uma janela pop-up.

### <a name="ports-and-firewall"></a>Portas e firewall
Há dois firewalls, você precisa tooconsider: **firewall corporativo** em execução no roteador central de saudação da organização Olá, e **firewall do Windows** configurado como um daemon na máquina local Olá onde hello gateway está instalado.  

![firewalls](./media/data-factory-data-management-gateway/firewalls2.png)

No nível do firewall corporativo, você precisa configurar o seguinte Olá domínios e portas de saída:

| Nomes de domínio | Portas | Descrição |
| --- | --- | --- |
| *.servicebus.windows.net |443, 80 |Usado para comunicação com o back-end do Serviço de Movimentação de Dados |
| *.core.windows.net |443 |Usado para cópia em etapas usando Blobs do Azure (se estiver configurado)|
| *.frontend.clouddatahub.net |443 |Usado para comunicação com o back-end do Serviço de Movimentação de Dados |


No nível do Firewall do Windows, essas portas de saída normalmente são habilitadas. Se não, você pode configurar portas e domínios Olá adequadamente no computador do gateway.

> [!NOTE]
> 1. Com base em sua origem / coletores, você pode ter domínios adicionais toowhitelist e portas de saída em sua empresa/firewall do Windows.
> 2. Para alguns bancos de dados de nuvem (por exemplo: [banco de dados do SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), talvez seja necessário toowhitelist endereço IP do computador do Gateway em sua configuração de firewall.
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a>Copiar dados de um repositório de dados fonte dados repositório tooa coletor
Verifique se as regras de firewall Olá estão habilitadas corretamente no firewall corporativo hello, firewall do Windows no computador do gateway Olá, e do repositório de dados de saudação em si. Essas regras permite Olá fonte do gateway tooconnect tooboth e coletar com êxito. Habilite regras para cada repositório de dados que está envolvido na operação de cópia de saudação.

Por exemplo, toocopy de **um coletor de banco de dados SQL local dados repositório tooan ou um coletor do Azure SQL Data Warehouse**, Olá seguintes etapas:

* Permitir a comunicação **TCP** de saída na porta **1433** para o firewall do Windows e o firewall corporativo.
* Definir configurações de firewall de saudação do endereço IP saudação do SQL Azure server tooadd de saudação gateway máquina toohello a lista de endereços IP permitidos.

> [!NOTE]
> Se o firewall não permitir a porta de saída 1433, o Gateway não poderá acessar diretamente o Azure SQL. Nesse caso, você pode usar [cópia preparados](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL banco de dados do Azure / DW do SQL Azure. Nesse cenário, exigiria apenas HTTPS (porta 443) Olá para movimentação de dados.
>
>


### <a name="proxy-server-considerations"></a>Considerações do servidor proxy
Se seu ambiente de rede corporativa usar um proxy server tooaccess Olá da internet, definir configurações de proxy adequadas toouse do gateway de gerenciamento de dados. Você pode definir o proxy Olá durante a fase de registro inicial hello.

![Definir proxy durante o registro](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

O gateway usa o serviço de nuvem do hello proxy server tooconnect toohello. Clique no link **Alteração** durante a configuração inicial. Consulte Olá **configuração de proxy** caixa de diálogo.

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxySettings.png)

Há três opções de configuração:

* **Não use proxy**: Gateway não usa qualquer serviço do proxy tooconnect toocloud explicitamente.
* **Use o proxy do sistema**: o Gateway usa o proxy Olá configuração que é configurado no diahost.exe.config e diawp.exe.config.  Se nenhum proxy está configurado no diahost.exe.config e diawp.exe.config, o gateway conecta toocloud serviço diretamente, sem passar por meio do proxy.
* **Usar proxy personalizado**: configurar Olá HTTP toouse de configuração de proxy para o gateway, em vez de usar as configurações no diahost.exe.config e diawp.exe.config.  Endereço e porta são necessários.  O Nome de Usuário e a Senha são opcionais, dependendo da configuração de autenticação do seu proxy.  Todas as configurações são criptografadas com o certificado de credencial de saudação do gateway hello e armazenadas localmente no computador de host do gateway de saudação.

gateway de gerenciamento de dados Olá Host de serviço é reiniciado automaticamente depois de salvar as configurações de proxy Olá atualizado.

Depois que o gateway foi registrado com sucesso, se você quiser tooview ou atualizar as configurações de proxy, use o Gerenciador de configuração de Gateway de gerenciamento de dados.

1. Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**.
2. Alternar toohello **configurações** guia.
3. Clique em **alteração** link no **HTTP Proxy** Olá de toolaunch seção **definir Proxy HTTP** caixa de diálogo.  
4. Depois de clicar em Olá **próximo** botão, verá uma caixa de diálogo de aviso solicitando sua permissão toosave Olá configuração do proxy e a reinicialização Olá serviço de Host do Gateway.

Você pode exibir e atualizar o proxy HTTP usando a ferramenta Gerenciador de Configurações.

![Definir proxy usando o gerenciador de configurações](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> Se você configurar um servidor proxy com autenticação NTLM, o serviço de Host do Gateway é executado na conta de domínio de saudação. Se você alterar a senha Olá Olá conta de domínio mais tarde, lembre-se de tooupdate definições de configuração para serviço hello e reiniciá-lo adequadamente. Devido a requisitos de toothis, sugerimos que você usar um servidor de proxy de saudação domínio dedicada conta tooaccess que não exigir senha de saudação tooupdate com frequência.
>
>

### <a name="configure-proxy-server-settings"></a>Definir configurações do servidor proxy
Se você selecionar **usar o proxy do sistema** configuração proxy Olá HTTP, o gateway usa Olá configuração do proxy no diahost.exe.config e diawp.exe.config.  Se nenhum proxy for especificado em diahost.exe.config e diawp.exe.config, o gateway conecta toocloud serviço diretamente, sem passar por meio do proxy. Olá procedimento a seguir fornece instruções para atualizar o arquivo de diahost.exe.config hello.  

1. No Explorador de arquivos, faça uma cópia de segurança do C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback backup do arquivo original hello.
2. Inicie o Notepad.exe executando como administrador e abra o arquivo de texto "C:\Arquivos de Programas\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config." Você localizar a marca de padrão de saudação para system.net conforme Olá código a seguir:

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   Em seguida, você pode adicionar detalhes do servidor proxy, conforme mostrado no exemplo a seguir de saudação:

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   Propriedades adicionais são permitidas em Olá proxy marca toospecify Olá necessárias configurações como scriptLocation. Consulte também[proxy (configurações de rede) do elemento](https://msdn.microsoft.com/library/sa91de1e.aspx) na sintaxe.

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. Salve o arquivo de configuração de saudação no local original Olá, reiniciar Olá serviço de Host do Gateway de gerenciamento de dados, que seleciona Olá alterações. serviço de saudação toorestart: usar o miniaplicativo Serviços Olá no painel de controle ou de saudação **Gerenciador de configuração de Gateway de gerenciamento de dados** > clique Olá **parar serviço** e clique em Olá **Iniciar serviço**. Se o serviço de saudação não iniciar, é provável que uma sintaxe de marca XML incorreta foi adicionada ao arquivo de configuração do aplicativo hello foi editado.

> [!IMPORTANT]
> Não se esqueça de tooupdate **ambos** diahost.exe.config e diawp.exe.config.  


Além disso pontos toothese, você também precisa toomake se o que Microsoft Azure está na lista de permissões da sua empresa. lista de saudação de endereços IP do Microsoft Azure válidos pode ser baixada do hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a>Possíveis sintomas de problemas relacionados ao firewall e ao servidor proxy
Se você encontrar erros toohello semelhante à seguir, é provável devido a configuração de tooimproper de saudação firewall ou servidor proxy, que bloqueia o gateway de conexão tooauthenticate tooData de fábrica em si. Consulte tooprevious seção tooensure seu servidor de firewall e proxy estão configurados corretamente.

1. Quando você tenta tooregister gateway de saudação, você receberá Olá erro a seguir: "chave do gateway falha tooregister hello. Antes de tentar novamente a chave do gateway tooregister hello, confirme se Olá gateway de gerenciamento de dados está em um estado conectado e hello serviço de Host do Gateway de gerenciamento de dados é iniciado."
2. Ao abrir o Gerenciador de Configurações, você vê o status "Desconectado" ou "Conectando". Ao exibir os logs de eventos do Windows, em "Visualizador de eventos" > "Logs de aplicativos e serviços" > "Gateway de gerenciamento de dados", ver mensagens de erro como Olá erro a seguir:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`

### <a name="open-port-8050-for-credential-encryption"></a>Abrir a porta 8050 para criptografia de credencial
Olá **definindo credenciais** aplicativo usa a porta de entrada de Olá **8050** toorelay gateway de toohello credenciais ao configurar um local vinculado de serviço no portal do Azure de saudação. Durante a instalação do gateway, por padrão, instalação do gateway Olá abre-o no computador do gateway hello.

Se você estiver usando um firewall de terceiros, você pode abrir porta Olá 8050 manualmente. Se você tiver problema de firewall durante a instalação do gateway, você pode tentar usar Olá seguindo o gateway de saudação do comando tooinstall sem configurar o firewall hello.

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

Se você escolher não tooopen porta Olá 8050 no computador do gateway hello, usar mecanismos diferentes do uso Olá **definindo credenciais** dados tooconfigure de aplicativo armazenam credenciais. Por exemplo, você pode usar o cmdlet do PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) . Confira a seção [Definir Credenciais e Segurança](#set-credentials-and-securityy) para saber como as credenciais do armazenamento de dados podem ser definidas.

## <a name="update"></a>Atualização
Por padrão, o gateway de gerenciamento de dados é atualizado automaticamente quando uma versão mais recente do gateway hello está disponível. gateway de saudação não é atualizado até que todas as tarefas agendada de saudação terminar. Nenhuma tarefa adicional é processada pelo gateway Olá até a conclusão da operação de atualização de saudação. Se Olá atualização falhar, gateway será revertido toohello uma versão antiga.

Consulte o tempo de atualização de saudação agendada em Olá locais a seguir:

* página de propriedades de gateway de saudação no hello portal do Azure.
* Home page do Gerenciador de configuração de Gateway de gerenciamento de dados de saudação
* Na mensagem de notificação da bandeja do sistema.

Guia de início de saudação do hello Gerenciador de configuração de Gateway de gerenciamento de dados exibe a agenda de atualização de saudação e gateway do hello última hora Olá foi instalado e atualizado.

![Agende atualizações](media/data-factory-data-management-gateway/UpdateSection.png)

Você pode instalar atualização Olá imediatamente ou aguardar Olá gateway toobe atualizada automaticamente em tempo de saudação agendado. Por exemplo, hello imagem mostra Olá mostrada no hello Gateway Configuration Manager juntamente com o botão de atualização de saudação que você pode clicar em tooinstall-lo imediatamente de mensagem de notificação a seguir.

![Atualizar no Gerenciador de Configurações DMG](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

mensagem de notificação de saudação na bandeja do sistema Olá seria conforme Olá a imagem a seguir:

![Mensagem da bandeja do sistema](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

Você ver o status de saudação da operação de atualização (manual ou automática) na bandeja do sistema hello. Quando você inicia o Gerenciador de configuração de Gateway próxima vez, verá uma mensagem de saudação de barra de notificação gateway Olá foi atualizada juntamente com um link muito[o que há de novo tópico](data-factory-gateway-release-notes.md).

### <a name="toodisableenable-auto-update-feature"></a>toodisable/ativar o recurso de atualização automática
Você pode desabilitar/habilitar o recurso de atualização automática de saudação fazendo Olá etapas a seguir:

[Para o gateway de nó único]
1. Inicie o Windows PowerShell no computador do gateway hello.
2. Alternar toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript pasta.
3. Olá execução após o comando tooturn Olá a atualização automática de recursos desativado (desativar).   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. tooturn-a novamente:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
[[Para vários nó altamente disponíveis e gateway dimensionável(versão prévia)](data-factory-data-management-gateway-high-availability-scalability.md)]
1. Inicie o Windows PowerShell no computador do gateway hello.
2. Alternar toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript pasta.
3. Olá execução após o comando tooturn Olá a atualização automática de recursos desativado (desativar).   

    Para o gateway com o recurso de alta disponibilidade (versão prévia), um parâmetro AuthKey adicional é necessário.
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. tooturn-a novamente:

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
Se você acessar o portal de saudação de um computador diferente do computador do gateway hello, você deve garantir que aplicativo do Gerenciador de credenciais hello pode se conectar a máquina de gateway toohello. Se o aplicativo hello não conseguem acessar o computador do gateway hello, ele não permite tooset credenciais para a fonte de dados de saudação e fonte de dados de toohello tootest conexão.  

Quando você usa Olá **definindo credenciais** aplicativo, o portal Olá criptografa credenciais Olá com hello certificado especificado no hello **certificado** guia da saudação **Gateway Gerenciador de configuração** no computador do gateway hello.

Se você estiver procurando uma abordagem baseada em API para criptografar credenciais hello, você pode usar o hello [AzureRmDataFactoryEncryptValue novo](https://msdn.microsoft.com/library/mt603802.aspx) credenciais de tooencrypt de cmdlet do PowerShell. Olá cmdlet usa o certificado de saudação que gateway é configurado toouse tooencrypt Olá credenciais. Adicionar credenciais criptografadas toohello **EncryptedCredential** elemento de saudação **connectionString** em Olá JSON. Use Olá JSON com hello [AzureRmDataFactoryLinkedService novo](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet ou em Olá Editor da fábrica de dados.

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

Há mais uma abordagem para definir as credenciais usando o Editor Data Factory. Se você criar um SQL Server vinculado serviço usando o editor de saudação e insira as credenciais em texto sem formatação, credenciais de saudação são criptografadas usando um certificado de serviço da fábrica de dados Olá possui. Não usa certificados Olá que gateway é configurado toouse. Embora essa abordagem possa ser um pouco mais rápida em alguns casos, ela é menos segura. Portanto, é recomendável que você siga essa abordagem somente para fins de desenvolvimento/teste.

## <a name="powershell-cmdlets"></a>Cmdlets do PowerShell
Esta seção descreve como toocreate e registrar um gateway usando cmdlets do PowerShell do Azure.

1. Inicie o **PowerShell do Azure** no modo de administrador.
2. Faça logon no tooyour conta do Azure executando Olá comando a seguir e inserir suas credenciais do Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Saudação de uso **AzureRmDataFactoryGateway novo** cmdlet toocreate um gateway lógico da seguinte maneira:

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    **Exemplo de comando e saída**:

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. No PowerShell do Azure, alternar pasta toohello: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**. Executar **RegisterGateway.ps1** associado à variável local Olá **$Key** conforme mostrado no comando a seguir de saudação. Esse script registra o agente de cliente Olá instalado em seu computador com o gateway de lógica Olá que criar anteriormente.

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    Você pode registrar o gateway de saudação em um computador remoto usando o parâmetro de IsRegisterOnRemoteMachine hello. Exemplo:

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. Você pode usar o hello **Get-AzureRmDataFactoryGateway** lista de saudação tooget cmdlet gateways na fábrica dados. Olá quando **Status** mostra **online**, isso significa que o gateway é toouse pronto.

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
Você pode remover um gateway usando Olá **remover AzureRmDataFactoryGateway** descrição de cmdlet e a atualização para um gateway usando Olá **AzureRmDataFactoryGateway conjunto** cmdlets. Para sintaxe e outros detalhes sobre esses cmdlets, consulte Referência de Cmdlet de Data Factory.  

### <a name="list-gateways-using-powershell"></a>Listar gateways usando o PowerShell

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a>Remover gateways usando o PowerShell

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a>Próximas etapas
* Consulte o artigo [Mover os dados entre os armazenamentos de dados local e de nuvem](data-factory-move-data-between-onprem-and-cloud.md) . Olá instruções passo a passo, você criará um pipeline que usa Olá gateway toomove dados de um tooan de banco de dados do SQL Server local BLOBs do Azure.  

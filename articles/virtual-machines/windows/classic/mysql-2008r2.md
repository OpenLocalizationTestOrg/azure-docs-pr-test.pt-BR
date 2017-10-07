---
title: "aaaCreate uma VM clássico do Azure que está executando MySQL | Microsoft Docs"
description: "Criar uma máquina virtual do Azure executando o Windows Server 2012 R2 e hello usando o modelo de implantação clássico de saudação do banco de dados do MySQL."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Instalar o MySQL em uma máquina virtual criada com o modelo de implantação clássico Olá executando o Windows Server 2016
[MySQL](https://www.mysql.com) é um banco de dados SQL fonte aberto popular. Este tutorial mostra como Olá tooinstall e execute **versão da comunidade do MySQL 5.7.18** como um servidor MySQL em uma máquina virtual em execução **Windows Server 2016**. Sua experiência pode ser um pouco diferente em outras versões do MySQL ou do Windows Server.

Para obter instruções sobre como instalar o MySQL no Linux, consulte: [como tooinstall MySQL no Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Criar uma máquina virtual com o Windows Server 2016 em execução
Se você ainda não tiver uma VM que executa o Windows Server 2016, você pode usar isso [tutorial](./tutorial.md) toocreate Olá VM.

## <a name="attach-a-data-disk"></a>Anexar um disco de dados
Após a criação de máquina virtual de hello, opcionalmente, você pode anexar um disco de dados. Adicionar que um disco de dados é recomendado para cargas de trabalho de produção e tooavoid espaço insuficiente na unidade do sistema operacional (c) de saudação, que inclui o sistema operacional de saudação.

Consulte [como tooattach dados de um disco máquina de virtual do Windows tooa](../attach-managed-disk-portal.md) e siga as instruções de saudação para anexar um disco vazio. Olá host cache configuração muito**nenhum** ou **somente leitura**.

## <a name="log-on-toohello-virtual-machine"></a>Faça logon na máquina virtual de toohello
Em seguida, você vai [fazer logon na máquina virtual de toohello](./connect-logon.md) para que você possa instalar o MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Instalar e executar o MySQL Community Server na máquina virtual de saudação
Siga estas etapas tooinstall, configurar e executar a versão da comunidade de saudação do servidor MySQL:

> [!NOTE]
> Ao fazer o download de itens usando o Internet Explorer, você pode definir o IE Olá **configuração de segurança reforçada** tooOff e a simplificar o processo de download de saudação. Saudação do menu de início, clique em ferramentas/Server Manager/Local Server administrativas, clique IE **configuração de segurança reforçada** e defina Olá configuração tooOff).
>
>

1. Depois de se conectar a máquina virtual de toohello usando a área de trabalho remota, clique em **Internet Explorer** na tela de início de saudação.
2. Selecione Olá **ferramentas** botão no canto superior direito de saudação (ícone de roda cogged Olá) e, em seguida, clique em **opções da Internet**. Clique em Olá **segurança** , clique em Olá **Sites confiáveis** ícone e, em seguida, clique em Olá **Sites** botão. Adicione http://*.mysql.com toohello lista de sites confiáveis. Clique em **Fechar** e, em seguida, em **OK**.
3. Em Olá barra endereços do Internet Explorer, digite https://dev.mysql.com/downloads/mysql/.
4. Usar Olá MySQL site toolocate e baixar a versão mais recente de saudação do hello instalador do MySQL para Windows. Ao escolher Olá instalador do MySQL, baixe a versão de saudação com hello conclua a configuração de arquivo (por exemplo, Olá mysql-instalador-comunidade-5.7.18.0.msi com um tamanho de arquivo de 352.8 MB) e salve o instalador de saudação.
5. Quando o instalador Olá download for concluído, clique em **executar** toolaunch a instalação.
6. Em Olá **contrato de licença** , aceite o contrato de licença hello e em **próximo**.
7. Em Olá **escolhendo um tipo de instalação** , clique em tipo de instalação de saudação que você deseja e, em seguida, clique em **próximo**. Olá, etapas a seguir pressupõem seleção de saudação do hello **somente servidor** tipo de instalação.
8. Se hello **verificar requisitos** exibe, clique em **Execute** instalador de saudação toolet instalar todos os componentes ausentes. Siga as instruções que exibem, como tempo de execução C++ redistribuível hello.
9. Em Olá **instalação** , clique em **Execute**. Quando a instalação for concluída, clique em **Avançar**.

10. Em Olá **configuração do produto** , clique em **próximo**.

11. Em Olá **tipo e rede** , especifique seu desejado conectividade e o tipo de opções de configuração, incluindo a porta TCP hello, se necessário. Selecione **Mostrar Opções Avançadas** e clique em **Próximo**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Em Olá **contas e funções** , especifique uma senha forte de raiz do MySQL. Adicione mais contas de usuário do MySQL, conforme a necessidade, e clique em **Avançar**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Em Olá **Windows Service** página, especifique as configurações padrão de toohello alterações para a execução de saudação do MySQL Server como um serviço do Windows conforme necessário e, em seguida, clique em **próximo**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Olá opções Olá **plug-ins e extensões** página são opcionais. Clique em **próximo** toocontinue.
15. Em Olá **opções avançadas de** página, especifique opções de toologging alterações conforme necessário e, em seguida, clique em **próximo**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Em Olá **aplicar a configuração de servidor** , clique em **Execute**. Quando etapas de configuração de saudação estiverem concluídas, clique em **concluir**.
17. Em Olá **configuração do produto** , clique em **próximo**.
18. Em Olá **instalação completa** , clique em **tooClipboard de Log de cópia** se você quiser tooexamine-lo mais tarde e depois clique em **concluir**.
19. Na tela de início do hello, digite **mysql**e, em seguida, clique em **cliente de linha de comando do MySQL 5.7**.
20. Insira a senha de raiz de saudação que você especificou na etapa 12 e você verá um prompt de onde você pode emitir comandos tooconfigure MySQL. Para obter detalhes de saudação de comandos e sintaxe, consulte [manuais de referência do MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Você também pode configurar as configurações de padrão de configuração do servidor, como unidades, diretórios de dados e Olá base. Para obter mais informações, confira [6.1.2 Padrões de configuração do servidor](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Configurar pontos de extremidade

Para computadores Olá MySQL serviço toobe tooclient disponível em Olá da Internet, deverá configurar um ponto de extremidade para a porta TCP de saudação e criar uma regra de Firewall do Windows. valor da porta saudação padrão em qual servidor MySQL Olá serviço escuta para clientes do MySQL é 3306. Você pode especificar outra porta, como porta Olá é consistente com valor de saudação fornecido em Olá **tipo e rede** página (etapa 11 do procedimento anterior Olá).

> [!NOTE]
> Para uso em produção, considere Olá implicações de segurança de tornando os computadores de tooall disponíveis do serviço de saudação do MySQL Server da saudação da Internet. Você pode definir o conjunto de saudação de endereços IP de origem que têm permissão de ponto de extremidade do toouse Olá com uma lista de controle de acesso (ACL). Para obter mais informações, consulte [como pontos de extremidade de tooSet tooa Máquina Virtual](setup-endpoints.md).
>
>

um ponto de extremidade de serviço do MySQL Server de saudação do tooconfigure:

1. No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)**, clique em nome de saudação da máquina virtual MySQL e, em seguida, clique em **pontos de extremidade**.
2. Na barra de comandos de saudação, clique em **adicionar**.
3. Em Olá **Adicionar ponto de extremidade** página, digite um nome exclusivo para **nome**.
4. Selecione **TCP** como protocolo de saudação.
5. Digite o número da porta hello, como **3306**, em ambos os **porta pública** e **porta privada**e, em seguida, clique em **Okey**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Adicionar uma regra de Firewall do Windows tooallow tráfego MySQL
tooadd uma regra de Firewall do Windows que permite o tráfego de MySQL de saudação da Internet, execute Olá seguinte comando em um _prompt de comando do Windows PowerShell_ na máquina virtual do hello MySQL server.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Testar sua conexão remota
tootest Olá executando sua conexão remota toohello VM do Azure do MySQL Server de serviço, você deverá fornecer o nome DNS Olá Olá do serviço de nuvem que contém a saudação VN.

1. No portal do Azure de Olá, clique em **máquinas virtuais (clássicas)**, clique em nome de saudação da sua máquina virtual do servidor MySQL e, em seguida, clique em **visão geral**.
2. No painel de máquina virtual hello, observe Olá **nome DNS** valor. Aqui está um exemplo:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Em um computador local executando o MySQL ou Olá cliente MySQL, execute Olá toolog de comando no como um usuário do MySQL a seguir.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   Por exemplo, usando Olá nome de usuário do MySQL _dbadmin3_ e hello _testmysql.cloudapp.net_ o nome DNS da máquina virtual de saudação, você pode começar usando o comando a seguir de saudação do MySQL:

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o que está executando MySQL, consulte Olá [documentação do MySQL](http://dev.mysql.com/doc/).

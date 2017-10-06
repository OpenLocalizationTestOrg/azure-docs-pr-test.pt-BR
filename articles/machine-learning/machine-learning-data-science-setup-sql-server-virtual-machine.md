---
title: "aaaSet uma máquina de virtual do SQL Server como um servidor de bloco de anotações do IPython | Microsoft Docs"
description: "Configurar uma Máquina Virtual de Ciência de Dados com o SQL Server e o IPython Server."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurar uma máquina virtual SQL Server do Azure como um servidor do IPython Notebook para análises avançadas
Este tópico mostra como tooprovision e configurar um toobe de máquina virtual do SQL Server usado como parte de um ambiente de ciência de dados com base em nuvem. máquina de virtual do Windows Hello está configurada com ferramentas como bloco de anotações do IPython, o Azure Storage Explorer e o AzCopy, bem como outros utilitários que são úteis para projetos de ciência de dados de suporte. Azure Storage Explorer e AzCopy, por exemplo, fornecem maneiras convenientes armazenamento de blob de tooAzure tooupload dados do seu computador local ou toodownload-tooyour o computador local do armazenamento de blob.

Galeria de máquina virtual do Azure Olá inclui várias imagens que contêm o Microsoft SQL Server. Selecione uma imagem de VM do SQL Server que seja adequada para as suas necessidades de dados. As imagens recomendadas são:

* SQL Server 2012 SP2 Enterprise toomedium pequeno para tamanhos de dados
* SQL Server 2012 SP2 Enterprise otimizado para cargas de trabalho DataWarehousing toovery grande grande para tamanhos de dados
  
  > [!NOTE]
  > A imagem do SQL Server 2012 SP2 Enterprise **não inclui um disco de dados**. Você será necessário tooadd e/ou anexar toostore de discos rígidos virtuais de um ou mais de seus dados. Quando você cria uma máquina virtual do Azure, ele tem um disco Olá unidade do sistema operacional mapeado toohello C e uma unidade de disco temporário mapeado toohello D. Não use os dados Olá D toostore da unidade. Como Olá nome sugere, ele fornece armazenamento temporário apenas. Não oferece redundância nem backup porque eles não residem no armazenamento do Azure.
  > 
  > 

## <a name="Provision"></a>Conecte-se toohello Portal clássico do Azure e provisionar uma máquina de virtual do SQL Server
1. Faça logon no toohello [portal clássico do Azure](http://manage.windowsazure.com/) usando sua conta.
   Se você não tiver uma conta do Azure, visite [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
2. No portal clássico do Azure hello, no hello inferior esquerdo da página da web de saudação, clique em **+ novo**, clique em **de computação**, clique em **máquina VIRTUAL**e, em seguida, clique em **FROM GALERIA**.
3. Em Olá **criar uma máquina Virtual** página, selecione uma imagem de máquina virtual que contém o SQL Server com base em suas necessidades de dados e clique Olá próxima seta no canto inferior direito da página de saudação. Para obter informações mais atualizadas sobre Olá Olá com suporte a imagens do SQL Server no Azure, consulte [guia de Introdução ao SQL Server em máquinas virtuais Azure](http://go.microsoft.com/fwlink/p/?LinkId=294720) tópico Olá [do SQL Server em máquinas virtuais Azure](http://go.microsoft.com/fwlink/p/?LinkId=294719) conjunto de documentação.
   
   ![Selecionar uma VM do SQL Server][1]
4. Em Olá primeiro **configuração de máquina Virtual** , forneça as seguintes informações:
   
   * Forneça um **NOME DE MÁQUINA VIRTUAL**.
   * Em Olá **novo nome de usuário** caixa, digite o nome de usuário exclusivo para Olá conta de administrador local da VM.
   * Em Olá **nova senha** , digite uma senha forte. Para obter mais informações, consulte [Senhas fortes (a página pode estar em inglês)](http://msdn.microsoft.com/library/ms161962.aspx).
   * Em Olá **Confirmar senha** caixa, digite novamente a senha de saudação.
   * Selecione Olá apropriado **tamanho** de saudação lista suspensa.
     
     > [!NOTE]
     > tamanho de saudação da máquina virtual de saudação é especificado durante o provisionamento: A2 é recomendado para cargas de trabalho de produção de hello ao menor tamanho. O tamanho mínimo recomendado para uma máquina virtual é A3 ao usar o SQL Server Enterprise Edition. Selecione A3 ou maior ao usar o SQL Server Enterprise Edition. Selecione A4 ao usar o SQL Server 2012 ou 2014 Enterprise otimizado para imagens de cargas de trabalho transacionais.
     > Selecione A7 ao usar o SQL Server 2012 ou 2014 Enterprise otimizado para imagens de cargas de trabalho do Data Warehouse. tamanho de saudação selecionado limita o número de discos de dados, que você pode configurar. Para obter informações mais atualizadas sobre tamanhos de máquina virtual disponíveis e o número de saudação de discos de dados que você pode anexar a máquina virtual de tooa, consulte [tamanhos de máquina Virtual para o Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Para obter informações sobre preços, consulte [Preços de Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Clique em seta próximo Olá Olá inferior direita toocontinue.
   
   ![Configuração da VM][2]
5. Em Olá segundo **configuração de máquina Virtual** página, configure os recursos de rede, armazenamento e disponibilidade:
   
   * Em Olá **serviço de nuvem** caixa, escolha **criar um novo serviço de nuvem**.
   * Em Olá **nome de DNS do serviço de nuvem** caixa, forneça a primeira parte de um nome DNS de sua escolha, Olá para que ele constitua um nome no formato **TESTNAME.cloudapp.net**
   * Em Olá **AFINIDADE região/grupo/rede VIRTUAL** , selecione uma região onde esta imagem virtual será hospedada.
   * Em Olá **conta de armazenamento**, selecione uma conta de armazenamento existente ou selecione um gerado automaticamente.
   * Em Olá **conjunto de disponibilidade** selecione **(nenhum)**.
   * Leia e aceite Olá informações sobre preços.
6. Em Olá **pontos de EXTREMIDADE** seção, clique no menu suspenso vazio de saudação em **nome**e selecione **MSSQL** , em seguida, digite o número de porta de saudação da instância do mecanismo de banco de dados (desaudação**1433** para a instância padrão de saudação).
7. A sua VM do SQL Server também pode funcionar como um IPython Notebook Server, que será configurado em uma etapa posterior.
   Adicione um novo ponto de extremidade toospecify Olá porta toouse para o servidor de bloco de anotações do IPython. Insira um nome no hello **nome** coluna, selecione um número de porta de sua escolha para a porta pública hello e 9999 para a porta privada hello.
   
   Clique em seta próximo Olá Olá inferior direita toocontinue.
   
   ![Selecionar portas MSSQL e IPython][3]
8. Aceite o padrão de saudação **instalar o VM agent** opção marcada e clique em marca de seleção de Olá Olá no hello inferior direita da saudação toocomplete de assistente Olá processo de provisionamento de VM.
   
   `![Opções finais de VM][4]
9. Aguarde enquanto o Azure prepara sua máquina virtual. Espera Olá tooproceed de status de máquina virtual por meio de:
   
   * Iniciando (Provisionamento)
   * Parada
   * Iniciando (Provisionamento)
   * Executando (Provisionamento)
   * Executando

## <a name="RemoteDesktop"></a>Abrir máquina virtual de saudação usando a área de trabalho remota e concluir a instalação
1. Quando o provisionamento for concluído, clique no nome de saudação sua máquina virtual toogo toohello da página de painel. Final Olá Olá página, clique em **conectar**.
2. Escolha tooopen Olá rpd arquivo usando o programa de área de trabalho remota do Windows hello (`%windir%\system32\mstsc.exe`).
3. Em Olá **a segurança do Windows** caixa de diálogo caixa, forneça a senha de saudação para a conta de administrador local que você especificou em uma etapa anterior.
   (Você pode ser solicitado tooverify credenciais de saudação da máquina virtual de hello.)
4. Olá primeira vez que você faça logon na máquina virtual de toothis, vários processos talvez seja necessário toocomplete, inclusive a configuração de área de trabalho, as atualizações do Windows e conclusão de tarefas de configuração inicial do Windows hello (sysprep). Depois que o sysprep do Windows é concluído, a configuração do SQL Server conclui as tarefas de configuração. Essas tarefas podem causar um atraso de alguns minutos enquanto são concluídas. `SELECT @@SERVERNAME`não pode retornar o nome correto da saudação até a conclusão da instalação do SQL Server e SQL Server Management Studio não pode ser visable na página inicial do hello.

Quando você estiver conectado toohello máquina virtual Windows de área de trabalho remota, Olá máquina virtual funciona assim como qualquer outro computador. Conecte-se a instância de padrão de toohello do SQL Server com o SQL Server Management Studio (em execução na máquina virtual de saudação) em Olá maneira normal.

## <a name="InstallIPython"></a>Instalar o IPython Notebook e outras ferramentas de suporte
tooconfigure seu novo tooserve de VM do SQL Server como um servidor de bloco de anotações do IPython e suporte adicional a instalação das ferramentas de tal AzCopy, Azure Storage Explorer, pacotes do Python de ciência de dados úteis e outros, um script de personalização especial é fornecido tooyou. tooinstall:

1. Saudação de atalho **inicial do Windows** ícone e clique em **Prompt de comando (Admin)**
2. Copie Olá comandos a seguir e cole no prompt de comando hello.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Quando solicitado, insira uma senha de sua escolha para Olá server do bloco de anotações do IPython.
4. script de personalização de saudação automatiza vários procedimentos de pós-instalação, que incluem:
    * Instalação e configuração do servidor do IPython Notebook
    * A abertura de portas TCP no firewall do Windows hello para pontos de extremidade Olá criado anteriormente:
    * Para conectividade remota do SQL Server
    * Para a conectividade remota do servidor IPython Notebook
    * Busca de scripts Python Notebooks e SQL de amostra
    * Baixar e instalar pacotes úteis de Python para ciência dados
    * Baixar e instalar ferramentas do Azure como o AzCopy e o Azure Storage Explorer   
    <br>
5. Você pode acessar e executar o bloco de anotações do IPython em qualquer navegador local ou remoto usando uma URL do formulário de saudação `https://<virtual_machine_DNS_name>:<port>`, onde a porta é Olá IPython pública selecionado durante o provisionamento de máquina virtual de saudação.
6. Servidor do bloco de anotações do IPython está sendo executado como um serviço em segundo plano e será reiniciado automaticamente quando você reiniciar a máquina virtual de saudação.

## <a name="Optional"></a>Anexe um disco de dados conforme necessário
Se a imagem VM não inclui discos de dados, ou seja, os discos que não seja a unidade C (disco do sistema operacional) e a unidade D (disco temporário), você precisa tooadd um ou mais dados discos toostore seus dados. imagem VM Olá para SQL Server 2012 SP2 Enterprise otimizado para cargas de trabalho DataWarehousing vem pré-configurada com discos adicionais para arquivos de log e de dados do SQL Server.

> [!NOTE]
> Não use os dados Olá D toostore da unidade. Como Olá nome sugere, ele fornece armazenamento temporário apenas. Não oferece redundância nem backup porque eles não residem no armazenamento do Azure.
> 
> 

tooattach discos de dados adicionais, execute as etapas de saudação descritas em [como tooAttach tooa um disco de dados Máquina Virtual do Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), que guiará você por meio de:

1. Anexar discos vazios toohello VM provisionado nas etapas anteriores
2. Inicialização dos discos de novo Olá na máquina virtual de saudação

## <a name="SSMS"></a>Conecte-se tooSQL Server Management Studio e habilitar a autenticação de modo misto
Olá mecanismo de banco de dados do SQL Server não pode usar a autenticação do Windows sem um ambiente de domínio. tooconnect toohello o mecanismo de banco de dados de outro computador, configurar o SQL Server para a autenticação de modo misto. A autenticação de modo misto permite a Autenticação do SQL Server e a Autenticação do Windows. Modo de autenticação do SQL é necessária nos dados de tooingest ordem diretamente de seus bancos de dados na VM do SQL Server a [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) usando o módulo de importação de dados de saudação.

1. Enquanto a máquina virtual de toohello conectado usando a área de trabalho remota, use o Windows hello **pesquisa** painel e o tipo **SQL Server Management Studio** (SMSS). Clique em toostart Olá SQL Server Management Studio (SSMS). Talvez você queira tooadd tooSSMS um atalho na área de trabalho para uso futuro.
   
   ![Iniciar o SSMS][5]
   
   Olá primeira vez que você abra o Management Studio, é necessário criar o ambiente do hello usuários Management Studio. Isso pode demorar alguns instantes.
2. Ao abrir, Management Studio apresenta Olá **conectar tooServer** caixa de diálogo. Em Olá **nome do servidor** caixa, digite o nome de saudação do hello máquina virtual tooconnect toohello mecanismo de banco de dados com hello Pesquisador de objetos.
   (Em vez do nome da máquina virtual Olá você também pode usar **(local)** ou um único ponto como Olá **nome do servidor**. Selecione **autenticação do Windows**e deixe  ***sua\_VM\_nome*\\sua\_local\_administrador**  em Olá **nome de usuário** caixa. Clique em **Conectar**.
   
   ![Conecte-se tooServer][6]
   
   <br>
   
   > [!TIP]
   > Você pode alterar o modo de autenticação do SQL Server hello usando uma alteração de chave de registro do Windows ou Olá SQL Server Management Studio. modo de autenticação de toochange usando a alteração de chave do registro do hello, iniciar um **nova consulta** e execute Olá script a seguir:
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    modo de autenticação de saudação toochange usando o SQL Server management Studio:

1. Em **Pesquisador de objetos do SQL Server Management Studio**, clique no nome da instância de saudação do SQL Server (nome da máquina virtual Olá) e, em seguida, clique em **propriedades**.
   
   ![Propriedades do servidor][7]
2. Em Olá **segurança** página em **autenticação de servidor**, selecione **modo de autenticação do Windows e SQL Server**e, em seguida, clique em **Okey** .
   
   ![Selecionar modo de autenticação][8]
3. Em Olá **SQL Server Management Studio** caixa de diálogo, clique em **Okey** confirmar toorestart requisito de saudação do SQL Server.
4. No **Object Explorer**, clique com o botão direito do mouse no seu servidor e clique em **Reiniciar**. (Se o SQL Server Agent estiver em execução, ele também deverá ser reinicializado.)
   
   ![Reiniciar][9]
5. Em Olá **SQL Server Management Studio** caixa de diálogo, clique em **Sim** concordar que você deseja toorestart do SQL Server.

## <a name="Logins"></a>Criar logons de autenticação do SQL Server
tooconnect toohello do mecanismo de banco de dados de outro computador, você deve criar pelo menos um logon de autenticação do SQL Server.  

Você pode criar novos logons do SQL Server programaticamente ou usando Olá SQL Server Management Studio. toocreate um novo usuário de administrador do sistema com a autenticação do SQL por meio de programação, iniciar um **nova consulta** e execute Olá script a seguir. Substitua <novo nome do usuário\> e <nova senha\> pelo *nome de usuário* e pela *senha* de sua escolha. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Ajuste a política de senha Olá conforme necessário (código de exemplo hello desativa a expiração da política de senha e de verificação). Para obter mais informações sobre logons do SQL Server, consulte [Criar um logon (a página pode estar em inglês)](http://msdn.microsoft.com/library/aa337562.aspx).  

toocreate novos logons de SQL Server usando Olá SQL Server Management Studio:

1. Em **Pesquisador de objetos do SQL Server Management Studio**, expanda a pasta Olá Olá da instância do servidor no qual você deseja que o novo logon do toocreate hello.
2. Saudação de atalho **segurança** pasta, ponto muito**novo**e selecione **logon...** .
   
   ![Novo Logon][10]
3. Em Olá **logon - novo** caixa de diálogo Olá **geral** página, insira o nome de saudação do novo usuário de saudação em Olá **nome de logon** caixa.
4. Selecione **Autenticação do SQL Server**.
5. Em Olá **senha** caixa, digite uma senha para Olá novo usuário. Digite essa senha novamente em Olá **Confirmar senha** caixa.
6. tooenforce opções de política de senha para complexidade e execução, selecione **impor política de senha** (recomendado). Essa é uma opção padrão quando a autenticação do SQL Server está selecionada.
7. tooenforce opções de política de senha para expiração, selecione **impor expiração de senha** (recomendado). Impor política de senha deve ser selecionada tooenable essa caixa de seleção. Essa é uma opção padrão quando a autenticação do SQL Server está selecionada.
8. tooforce Olá usuário toocreate uma nova senha após Olá primeiro o logon for usada, selecione **usuário deve alterar a senha no próximo logon** (recomendado se esse logon é para outra pessoa toouse. Se o logon de saudação é para seu próprio uso, não selecione essa opção.) Impor expiração de senha deve ser selecionada tooenable essa caixa de seleção. Essa é uma opção padrão quando a autenticação do SQL Server está selecionada.
9. De saudação **banco de dados padrão** , selecione um banco de dados padrão para logon de saudação. **mestre** é saudação padrão para essa opção. Se você ainda não tiver criado um banco de dados de usuário, deixe essa definição muito**mestre**.
10. Em Olá **idioma padrão** lista, deixe **padrão** como valor de saudação.
    
    ![Propriedades de Logon][11]
11. Se esse for o primeiro logon de saudação que você está criando, convém designar esse logon como um administrador do SQL Server. Em caso afirmativo, na página **Funções de Servidor**, marque **sysadmin**.
    
    > [!IMPORTANT]
    > Os membros da função de servidor fixa de sysadmin de Olá tem total controle sobre Olá mecanismo de banco de dados. Por motivos de segurança, você deve restringir cuidadosamente a associação nessa função.
    > 
    > 
    
    ![sysadmin][12]
12. Clique em OK.

## <a name="DNS"></a>Determinar nome DNS de saudação da máquina virtual de saudação
tooconnect toohello do mecanismo de banco de dados do SQL Server de outro computador, você deve saber Olá sistema de nome de domínio (DNS) nome da máquina virtual de saudação.

(Isso é Olá nome hello internet usa tooidentify Olá máquina virtual. Você pode usar o endereço IP hello, mas o endereço IP hello pode mudar quando o Azure move recursos de redundância ou manutenção. nome DNS de saudação será estável porque ele pode ser redirecionado tooa novo endereço IP.)

1. Olá Portal clássico do Azure (ou da etapa anterior Olá), selecione **máquinas virtuais**.
2. Em Olá **INSTÂNCIAS de máquina VIRTUAL** página Olá **nome DNS** coluna, localizar e copiar nome DNS de Olá Olá máquina virtual aparece precedido por **http://**. (interface do usuário Olá poderá não exibir nome inteiro hello, mas com o botão direito nele e selecione Copiar.)

## <a name="cde"></a>Conectar toohello mecanismo de banco de dados de outro computador
1. Em um computador conectado toohello internet, abra o SQL Server Management Studio.
2. Em Olá **conectar tooServer** ou **conectar tooDatabase mecanismo** caixa de diálogo Olá **nome do servidor** , digite o nome DNS de saudação da máquina virtual (determinada na Olá tarefa anterior) e um número de porta do ponto de extremidade público no formato de saudação do *DNSName, portnumber* como **tutorialtestVM.cloudapp.net,57500**.
3. Em Olá **autenticação** selecione **autenticação do SQL Server**.
4. Em Olá **Login** caixa, digite o nome de saudação de um logon que você criou em uma tarefa anterior.
5. Em Olá **senha** caixa, digite a senha de saudação do logon de saudação que você cria em uma tarefa anterior.
6. Clique em **Conectar**.

## <a name="amlconnect"></a>Conecte-se toohello mecanismo de banco de dados de aprendizado de máquina do Azure
Etapas posteriores de saudação processo de ciência de dados de equipe, você usará Olá [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) toobuild e implantar modelos de aprendizado de máquina. dados de tooingest de seus bancos de dados da VM do SQL Server diretamente no aprendizado de máquina do Azure para treinamento ou pontuação, usar Olá **importar dados** módulo em uma nova [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) experiências. Este tópico é abordado em mais detalhes por meio de saudação links de guia do processo de ciência de dados de equipe. Para obter uma introdução, consulte [O que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md).

1. Em Olá **propriedades** painel da saudação [módulo de importação de dados](https://msdn.microsoft.com/library/azure/dn905997.aspx), selecione **banco de dados do SQL Azure** de saudação **fonte de dados** lista suspensa.
2. Em Olá **nome do servidor de banco de dados** texto, digite`tcp:<DNS name of your virtual machine>,1433`
3. Insira o nome de usuário do SQL de saudação em Olá **nome de conta de usuário do servidor** caixa de texto.
4. Insira a senha do usuário do sql Olá no hello **senha de conta de usuário do servidor** caixa de texto.
   
   ![Importar Dados no Azure Machine Learning][13]

## <a name="shutdown"></a>Desligar e desalocar a máquina virtual quando ela não estiver em uso
A cobrança das máquinas virtuais do Azure ocorre na forma **pague somente pelo que usa**. tooensure que não estão sendo cobrado quando não estiver usando sua máquina virtual, ele tem toobe em Olá **parado (desalocado)** estado.

> [!NOTE]
> Desligar a máquina virtual de saudação do dentro (usando as opções de energia do Windows), hello VM for interrompida, mas permanece alocada. tooensure você não estiver sendo cobrado, sempre irá parar máquinas virtuais de saudação [Portal clássico do Azure](http://manage.windowsazure.com/). Você também pode interromper Olá VM por meio do Powershell chamando muito ShutdownRoleOperation com "PostShutdownAction" igual "StoppedDeallocated".
> 
> 

tooshutdown e desalocar máquina virtual de saudação:

1. Faça logon no toohello [Portal clássico do Azure](http://manage.windowsazure.com/) usando sua conta.  
2. Selecione **máquinas virtuais** saudação à esquerda na barra de navegação.
3. Na lista de saudação de máquinas virtuais, clique no nome da saudação de sua máquina virtual, vá toohello **painel** página.
4. Final Olá Olá página, clique em **desligamento**.

![Desligamento da VM][15]

máquina virtual de saudação será desalocada mas não excluída. Você pode reiniciar a máquina virtual a qualquer momento de saudação Portal clássico do Azure.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>A VM do Azure SQL Server está pronto toouse: próximas etapas?
Sua máquina virtual agora está pronto toouse seu exercícios de ciência de dados. máquina virtual de saudação também está pronta para uso como um servidor de bloco de anotações do IPython para exploração hello e processamento de dados e outras tarefas em conjunto com o aprendizado de máquina do Azure e hello processo de ciência de dados da equipe (TDSP).

Olá próximas etapas no processo de ciência de dados Olá estão mapeadas em Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) e podem incluir etapas que movem dados para HDInsight, o processo e de exemplo-lo na preparação para aprender com dados saudação com a máquina do Azure Aprendizado.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png


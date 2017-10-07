---
title: "aaaCreating uma imagem de máquina virtual para hello Azure Marketplace | Microsoft Docs"
description: "Instruções detalhadas sobre como toocreate uma máquina virtual de imagem hello Azure Marketplace para outros toopurchase."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5c937b8e-e28d-4007-9fef-624046bca2ae
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio; v-divte
ms.openlocfilehash: 65e1c0530bb050fb379a52544e36c55faacd84df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-virtual-machine-image-for-hello-azure-marketplace"></a>Guia toocreate uma imagem de máquina virtual para hello Azure Marketplace
Neste artigo, **etapa 2**, orienta Preparando Olá discos de rígidos virtuais (VHDs) que você implantará toohello Azure Marketplace. Seus VHDs são a base de saudação do seu SKU. processo de saudação difere dependendo se você está fornecendo um SKU baseado em Windows ou Linux. Este artigo aborda ambos os cenários. Esse processo pode ser executado em paralelo com [Criação e registro de conta][link-acct-creation].

## <a name="1-define-offers-and-skus"></a>1. Definir ofertas e SKUs
Nesta seção, você aprenderá toodefine Olá ofertas e seus SKUs associados.

Uma oferta é um tooall "pai" de seus SKUs. Pode haver várias ofertas. Como decidir toostructure suas ofertas é tooyou. Quando uma oferta é impulsionada toostaging, ele é enviado junto com todos os seus SKUs. Considere cuidadosamente seu identificadores SKU, porque eles estarão visíveis na URL de saudação:

* Azure.com: http://azure.microsoft.com/marketplace/partners/{PartnerNamespace}/{OfferIdentifier}-{SKUidentifier}
* Versão Prévia do Portal do Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{SKUIDdentifier}  

Um SKU é Olá comercial de uma imagem de VM. Uma imagem de VM contém um disco de sistema operacional e zero ou mais discos de dados. É essencialmente o perfil de armazenamento completa Olá para uma máquina virtual. É necessário um VHD por disco. Discos de dados em branco até mesmo exigem um toobe VHD criado.

Independentemente de qual sistema operacional que você usar, adicione somente Olá número mínimo de discos de dados necessários ao Olá SKU. Os clientes não é possível remover os discos que fazem parte de uma imagem em tempo de saudação de implantação, mas sempre poderá adicionar discos durante ou após a implantação se necessário.

> [!IMPORTANT]
> **Não altere a contagem de discos em uma nova versão da imagem.** Se você deve reconfigurar os discos de dados na imagem hello, defina um SKU de novo. Publicar uma nova versão de imagem com contagens de disco diferente terá o potencial de saudação da nova implantação baseada em hello, a nova versão de imagem em caso de implantações de dimensionamento automático e automáticas das soluções através de modelos ARM e outros cenários de quebra.
>
>

### <a name="11-add-an-offer"></a>1.1 Adicionar uma oferta
1. Entrar toohello [Portal de publicação] [ link-pubportal] usando sua conta do vendedor.
2. Selecione Olá **máquinas virtuais** guia da saudação Portal de publicação. No campo de entrada solicitada do hello, insira seu nome de oferta. Olá oferta nome é normalmente saudação do produto de saudação ou serviço que você planeje toosell em hello Azure Marketplace.
3. Selecione **Criar**.

### <a name="12-define-a-sku"></a>1.2 Defina uma SKU
Depois de ter adicionado uma oferta, você precisa toodefine e identifique seus SKUs. Você pode ter várias ofertas e cada oferta pode ter várias SKUs abaixo dela. Quando uma oferta é impulsionada toostaging, ele é enviado junto com todos os seus SKUs.

1. **Adicionar uma SKU.** Olá SKU exige um identificador, que é usado na URL de saudação. Identificador de saudação deve ser exclusivo dentro de seu perfil de publicação, mas não há nenhum risco de colisão de identificador com outros editores.

   > [!NOTE]
   > oferta de saudação e identificadores SKU são exibidos em URL oferta Olá Olá Marketplace.
   >
   >
2. **Adicionar uma descrição resumida para a sua SKU.** Descrições resumidas são toocustomers visível, portanto, você deverá torná-los facilmente legível. Essas informações não precisam toobe bloqueado até que a fase de "Push tooStaging" hello. Até lá, você está livre tooedit-lo.
3. Se você estiver usando SKUs do Windows, siga links sugerido Olá Olá tooacquire aprovadas versões do Windows Server.

## <a name="2-create-an-azure-compatible-vhd-linux-based"></a>2. Criar VHD compatível com o Azure (baseado em Linux)
Esta seção aborda as práticas recomendadas para criar uma imagem VM baseadas em Linux para hello Azure Marketplace. Para obter instruções passo a passo, consulte toohello documentação a seguir: [criando e carregando um disco rígido Virtual que contém Olá o sistema operacional Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="3-create-an-azure-compatible-vhd-windows-based"></a>3. Criar um VHD compatível com Azure (baseado no Windows)
Esta seção discute Olá etapas toocreate uma SKU baseada no Windows Server para hello Azure Marketplace.

### <a name="31-ensure-that-you-are-using-hello-correct-base-vhds"></a>3.1 Certifique-se de que você está usando Olá corrigir VHDs de base
Olá VHD do sistema operacional para a imagem VM deve ser baseada em uma imagem de base aprovada do Azure que contém o Windows Server ou SQL Server.

toobegin, criar uma máquina virtual de uma saudação imagens, localizadas em Olá a seguir [portal do Microsoft Azure][link-azure-portal]:

* Windows Server ([2012 R2 Datacenter][link-datactr-2012-r2], [2012 Datacenter][link-datactr-2012], [2008 R2 SP1][link-datactr-2008-r2])
* SQL Server 2014 ([Enterprise][link-sql-2014-ent], [Standard][link-sql-2014-std], [Web][link-sql-2014-web])
* SQL Server 2012 SP2 ([Enterprise][link-sql-2012-ent], [Standard][link-sql-2012-std], [Web][link-sql-2012-web])

Esses links também podem ser encontrados no hello Portal de publicação na página SKU de saudação.

> [!TIP]
> Se você estiver usando o portal do Azure atual de saudação ou o PowerShell, as imagens do Windows Server publicadas em 8 de setembro de 2014 e versões posteriores são aprovadas.
>
>

### <a name="32-create-your-windows-based-vm"></a>3.2 Criar sua VM baseada em Windows
No portal do Microsoft Azure hello, você pode criar sua VM com base em uma imagem de base aprovada em apenas algumas etapas simples. a seguir Olá é uma visão geral do processo de saudação:

1. Na página de imagem base do hello, selecione **criar Máquina Virtual** toobe direcionado toohello novo [portal do Microsoft Azure][link-azure-portal].

    ![desenho][img-acom-1]
2. Faça logon no portal de toohello com hello conta da Microsoft e a senha para Olá assinatura do Azure que você deseja toouse.
3. Siga Olá prompts toocreate uma VM usando Olá imagem base que você selecionou. Você precisa tooprovide um nome de host (nome do computador de saudação), o nome de usuário (registrado como administrador) e a senha para Olá VM.

    ![desenho][img-portal-vm-create]
4. Selecione o tamanho de saudação do hello VM toodeploy:

    a.    Se você planejar toodevelop Olá VHD local, tamanho de saudação não importa. Considere usar uma saudação VMs menores.

    b.    Se você planejar a imagem de saudação toodevelop no Azure, considere usando uma saudação recomendado tamanhos de VM para imagem selecionada hello.

    c.    Para obter informações sobre preços, consulte toohello **recomendado camadas de preços** exibido no portal de saudação do seletor. Ele fornecerá Olá três tamanhos recomendados fornecidos pelo editor de saudação. (Nesse caso, o publicador Olá é Microsoft.)

    ![desenho][img-portal-vm-size]
5. Defina as propriedades:

    a.    Para implantação rápida, você pode deixar Olá valores padrão para propriedades de saudação em **configuração opcional** e **grupo de recursos**.

    b.    Em **conta de armazenamento**, você pode opcionalmente Selecionar conta de armazenamento Olá em qual sistema operacional de saudação VHD será armazenado.

    c.    Em **grupo de recursos**, você pode opcionalmente Selecionar grupo lógico de saudação no qual tooplace Olá VM.
6. Selecione Olá **local** para implantação:

    a.    Se você planejar toodevelop Olá VHD local, local de saudação não importa porque você fará o upload Olá imagem tooAzure mais tarde.

    b.    Se você planejar a imagem de saudação toodevelop no Azure, considere usar uma saudação baseado nos EUA regiões do Microsoft Azure desde o início de saudação. Isso acelera a saudação VHD processo de cópia que executa Microsoft em seu nome, ao enviar sua imagem para certificação.

    ![desenho][img-portal-vm-location]
7. Clique em **Criar**. Olá VM inicia toodeploy. Em minutos, você terá uma implantação bem-sucedida e pode começar a imagem de saudação toocreate para o SKU.

### <a name="33-develop-your-vhd-in-hello-cloud"></a>3.3 desenvolver seu VHD na nuvem Olá
É altamente recomendável que você desenvolver seu VHD na nuvem hello usando o protocolo de área de trabalho remota (RDP). Você se conectar tooRDP Olá nome e a senha especificada durante o provisionamento.

> [!IMPORTANT]
> Se você desenvolve seu VHD no local (não recomendado), consulte [Criando um imagem de máquina virtual no local](marketplace-publishing-vm-image-creation-on-premise.md). Baixar o VHD não é necessário se você estiver desenvolvendo em nuvem hello.
>
>

**Conectar via RDP usando Olá [portal do Microsoft Azure][link-azure-portal]**

1. Selecione **Procurar** > **VMs**.
2. Abre a folha de máquinas virtuais de saudação. Verifique se essa máquina virtual que você deseja tooconnect com hello está em execução e, em seguida, selecione-o na lista de saudação de VMs implantadas.
3. Abre um blade que descreve a saudação selecionado de VM. Na parte superior da saudação, clique em **conectar**.
4. Você está tooenter solicitadas Olá nome e a senha que você especificou durante o provisionamento.

**Conecte-se via RDP usando PowerShell**

toodownload uma máquina local do tooa de arquivo de área de trabalho remota, use Olá [cmdlet Get-AzureRemoteDesktopFile][link-technet-2]. Em ordem toouse esse cmdlet, é necessário tooknow nome de saudação do serviço de saudação e o nome do hello VM. Se você criou Olá VM do hello [portal do Microsoft Azure][link-azure-portal], você pode encontrar essas informações em Propriedades da VM:

1. No portal do Microsoft Azure hello, selecione **procurar** > **VMs**.
2. Abre a folha de máquinas virtuais de saudação. Selecione Olá VM implantado.
3. Abre um blade que descreve a saudação selecionado de VM.
4. Clique em **Propriedades**.
5. a primeira parte do nome de domínio Olá Olá é o nome do serviço de saudação. nome de host de saudação é o nome VM de saudação.

    ![desenho][img-portal-vm-rdp]
6. arquivo Hello cmdlet toodownload Olá RDP para a área de trabalho do administrador do hello criado VM toohello local é o seguinte.

        Get‐AzureRemoteDesktopFile ‐ServiceName “baseimagevm‐6820cq00” ‐Name “BaseImageVM” –LocalPath “C:\Users\Administrator\Desktop\BaseImageVM.rdp”

Para obter mais informações sobre o RDP podem ser localizadas no MSDN no artigo Olá [conectar tooan VM do Azure com RDP ou SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx).

**Configure uma VM e crie sua SKU**

Depois que o sistema de operacional Olá que VHD é baixado, use o Hyper-v e configurar um toobegin VM criando o SKU. Etapas detalhadas podem ser encontradas em Olá TechNet link a seguir: [instalar o Hyper-v e configurar uma VM](http://technet.microsoft.com/library/hh846766.aspx).

### <a name="34-choose-hello-correct-vhd-size"></a>3.4 escolher o tamanho correto de VHD Olá
sistema operacional Windows Hello VHD em sua imagem VM deve ser criado como um VHD de formato fixo de 128 GB.  

Se o tamanho físico da saudação é menos de 128 GB, Olá VHD deve ser esparso. Olá Windows e SQL Server imagens básicas fornecidas já atender a esses requisitos, portanto, não altere Olá formato ou Olá o tamanho da saudação obtido do VHD.  

Discos de dados podem ser de até 1 TB. Ao decidir sobre o tamanho do disco hello, lembre-se de que os clientes não é possível redimensionar VHDs dentro de uma imagem em tempo de saudação da implantação. Os VHDs de disco de dados devem ser criados como um VHD de formato fixo. Eles também devem ser esparsos. Discos de dados podem estar vazios ou conter dados.

### <a name="35-install-hello-latest-windows-patches"></a>3.5 instalar patches do Windows mais recentes Olá
Olá base imagens contêm o patches mais recentes Olá backup tootheir data de publicação. Antes de publicar o sistema operacional de saudação VHD que você criou, certifique-se de que o Windows Update foi executado e que todos os Olá crítico mais recente e atualizações de segurança importantes foram instaladas.

### <a name="36-perform-additional-configuration-and-schedule-tasks-as-necessary"></a>3.6 Execute as tarefas de configuração e programação adicionais, conforme necessário
Se a configuração adicional é necessária, considere o uso de uma tarefa agendada que é executado na inicialização toomake toohello quaisquer alterações finais VM após ele ter sido implantado:

* É uma tarefa de saudação de toohave de prática recomendada excluir a mesmo após a execução bem-sucedida.
* Nenhuma configuração deve confiar em unidades diferentes unidades C ou D, pois elas são apenas duas unidades de saudação sempre garantidos tooexist. A unidade C é o disco do sistema operacional hello e unidade D é o disco local temporário de saudação.

### <a name="37-generalize-hello-image"></a>3.7 generalizar a imagem de saudação
Todas as imagens em hello Azure Marketplace devem ser reutilizáveis de forma genérica. Em outras palavras, a saudação no VHD do sistema operacional deve ser generalizado:

* Para Windows, a imagem de saudação deve ser "Sysprep", e nenhuma configuração deve ser feita que não dão suporte a saudação **sysprep** comando.
* Você pode executar Olá Olá diretório WINDIR%\System32\Sysprep após o comando.

        sysprep.exe /generalize /oobe /shutdown

  Orientação sobre como sistema de operacional Olá toosysprep é fornecido na etapa de saudação seguinte artigo do MSDN: [criar e carregar um VHD do Windows Server tooAzure](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="4-deploy-a-vm-from-your-vhds"></a>4. Implantar uma VM por meio dos seus VHDs
Depois de carregar seus VHDs (Olá generalizado no VHD do sistema operacional e dados de zero ou mais VHDs em disco) tooan conta de armazenamento do Azure, você pode registrá-los como uma imagem VM do usuário. Em seguida, você pode testar essa imagem. Observe que como seu VHD do sistema operacional é generalizada, você não pode diretamente implantar Olá VM fornecendo Olá URL do VHD.

toolearn mais sobre imagens de VM, examine Olá postagens de blog a seguir:

* [Image da VM](https://azure.microsoft.com/blog/vm-image-blog-post/)
* [Guia do PowerShell da Imagem da VM](https://azure.microsoft.com/blog/vm-image-powershell-how-to-blog-post/)
* [Sobre imagens VM no Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)

### <a name="set-up-hello-necessary-tools-powershell-and-azure-cli"></a>Configurar as ferramentas necessárias hello, PowerShell e a CLI do Azure
* [Como toosetup PowerShell](/powershell/azure/overview)
* [Como toosetup CLI do Azure](../cli-install-nodejs.md)

### <a name="41-create-a-user-vm-image"></a>4.1 Criar uma imagem VM de usuário
#### <a name="capture-vm"></a>Capturar VM
Leia os links de saudação fornecidos abaixo para obter orientação sobre como capturar Olá VM usando a CLI do PowerShell/API/Azure.

* [API](https://msdn.microsoft.com/library/mt163560.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI do Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="generalize-image"></a>Generalizar uma imagem
Leia os links de saudação fornecidos abaixo para obter orientação sobre como capturar Olá VM usando a CLI do PowerShell/API/Azure.

* [API](https://msdn.microsoft.com/library/mt269439.aspx)
* [PowerShell](../virtual-machines/windows/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI do Azure](../virtual-machines/linux/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="42-deploy-a-vm-from-a-user-vm-image"></a>4.2 Implante uma VM usando uma imagem de VM de usuário
toodeploy uma VM de uma imagem VM do usuário, você pode usar o hello atual [portal do Azure](https://manage.windowsazure.com) ou o PowerShell.

**Implantar uma VM do portal do Azure atual de saudação**

1. Vá muito**novo** > **de computação** > **Máquina Virtual** > **da galeria**.

    ![desenho][img-manage-vm-new]
2. Vá muito**Minhas imagens**, e, em seguida, selecione Olá imagem VM da qual toodeploy uma VM:

   1. Imagem de toowhich atenção de pagamento selecionar, pois Olá **Minhas imagens** exibir listas de imagens do sistema operacional e imagens da VM.
   2. Observando o número de saudação de discos pode ajudar a determinar que tipo de imagem que você está implantando, porque a maioria de saudação de imagens VM tem mais de um disco. No entanto, é possível toohave uma imagem de VM com apenas um único disco do sistema operacional que teria **número de discos** definir too1.

      ![desenho][img-manage-vm-select]
3. Siga o Assistente para criação de VM hello e especifique o nome da VM hello, tamanho VM, local, nome de usuário e senha.

**Implantar uma VM a partir do PowerShell**

toodeploy que uma VM grande de saudação generalizado imagem VM que acabou de criar, você pode usar o hello cmdlets a seguir.

    $img = Get-AzureVMImage -ImageName "myVMImage"
    $user = "user123"
    $pass = "adminPassword123"
    $myVM = New-AzureVMConfig -Name "VMImageVM" -InstanceSize "Large" -ImageName $img.ImageName | Add-AzureProvisioningConfig -Windows -AdminUsername $user -Password $pass
    New-AzureVM -ServiceName "VMImageCloudService" -VMs $myVM -Location "West US" -WaitForBoot

> [!IMPORTANT]
> Consulte [solução de problemas comuns encontrados durante a criação do VHD] para obter assistência adicional.
>
>

## <a name="5-obtain-certification-for-your-vm-image"></a>5. Obter a certificação para a sua Imagem VM
Olá próxima etapa de preparar sua imagem VM para hello Azure Marketplace é toohave que ele certificado.

Esse processo inclui a execução de uma ferramenta de certificação especial, carregando toohello de resultados de verificação de saudação imagem de contêiner do Azure onde residem os seus VHDs, adicionando uma oferta, definindo o SKU e enviar sua VM para certificação.

### <a name="51-download-and-run-hello-certification-test-tool-for-azure-certified"></a>5.1 Baixe e execute Olá, ferramenta de teste de certificação do Azure Certified
ferramenta de certificação de saudação é executada em uma VM em execução, provisionada de sua imagem VM do usuário, tooensure que Olá a imagem da VM é compatível com o Microsoft Azure. Ele verificará se requisitos sobre como preparar o VHD e orientação Olá foram atendidos. saída de saudação da ferramenta de saudação é um relatório de compatibilidade, o que deve ser carregado no hello Portal de publicação ao solicitante de certificação.

ferramenta de certificação de saudação pode ser usada com o Windows e VMs do Linux. Ele se conecta com base em tooWindows VMs por meio do PowerShell e se conecta tooLinux VMs via SSH.Net:

1. Primeiro, baixe a ferramenta de certificação de saudação em Olá [site de download da Microsoft][link-msft-download].
2. Abra a ferramenta de certificação Olá e clique em Olá **Iniciar novo teste** botão.
3. De saudação **teste informações** tela, insira um nome para a execução de teste de saudação.
4. Escolha se a VM está em Linux ou Windows. Dependendo do que você escolher, selecione opções subsequentes hello.

### <a name="connect-hello-certification-tool-tooa-linux-vm-image"></a>**Conecte-se Olá certificação ferramenta tooa imagem de VM do Linux**
1. Modo de autenticação SSH selecione Olá: arquivo de senha ou chave.
2. Se usar autenticação baseada em senha, insira o nome de sistema de nome de domínio (DNS) do hello, nome de usuário e senha.
3. Se usando a autenticação de arquivo de chave, insira o nome DNS hello, o nome de usuário e o local da chave privada.

   ![Autenticação de senha da Imagem de VM do Linux][img-cert-vm-pswd-lnx]

   ![Autenticação de chave de arquivo da Imagem de VM do Linux][img-cert-vm-key-lnx]

### <a name="connect-hello-certification-tool-tooa-windows-based-vm-image"></a>**Conecte-se a imagem VM baseadas em Windows hello certificação ferramenta tooa**
1. Insira o nome DNS da VM Olá totalmente qualificado (por exemplo, MyVMName.Cloudapp.net).
2. Insira a senha e nome de usuário de saudação.

   ![Autenticação de senha de Imagem de VM do Windows][img-cert-vm-pswd-win]

Depois de selecionar opções de saudação correto para a imagem VM de baseados em Windows ou Linux, selecione **Conexão de teste** tooensure que SSH.Net ou o PowerShell tem uma conexão válida para fins de teste. Depois que uma conexão é estabelecida, selecione **próximo** toostart teste de saudação.

Quando o teste de saudação for concluído, você receberá resultados hello (passagem/aviso/falha) para cada elemento de teste.

![Casos de teste para a Imagem de VM do Linux][img-cert-vm-test-lnx]

![Casos de teste para a Imagem de VM do Windows][img-cert-vm-test-win]

Se algum dos testes de saudação falhar, a imagem não ser certificada. Se isso ocorrer, verifique os requisitos de saudação e faça as alterações necessárias.

Depois que o teste automatizado de Olá, você será solicitado a entrada adicional tooprovide em sua imagem VM por meio de uma tela de questionário.  Concluir perguntas hello e, em seguida, selecione **próximo**.

![Questionário da Ferramenta de Certificação][img-cert-vm-questionnaire]

![Questionário da Ferramenta de Certificação][img-cert-vm-questionnaire-2]

Depois de concluir questionário hello, você pode fornecer informações adicionais, como informações de acesso SSH para Olá imagem de VM do Linux e uma explicação para todas as avaliações de falha. Você pode baixar os resultados de teste hello e arquivos de log para casos de teste Olá executado em questionário de toohello adição tooyour respostas. Salvar resultados de saudação em Olá mesmo contêiner que seus VHDs.

![Salvar resultados do teste de certificação][img-cert-vm-results]

### <a name="52-get-hello-shared-access-signature-uri-for-your-vm-images"></a>5.2 obter o URI de assinatura de acesso compartilhado Olá para as imagens VM
Durante a saudação ao processo de publicação, você deve especificar Olá URIs uniform resource identifiers () que levam tooeach de saudação VHDs que você criou para o SKU. A Microsoft precisa acesso toothese VHDs durante o processo de certificação hello. Portanto, você precisa toocreate um URI de assinatura de acesso compartilhado para cada VHD. Isso é hello URI que deve ser inserido no **imagens** guia Olá Portal de publicação.

assinatura de acesso compartilhado Olá URI criado deve aderir toohello requisitos a seguir:

* Ao gerar um URI de assinatura de acesso compartilhado para seus VHDs, as permissões de leitura e lista são suficientes. Não forneça acesso para gravação ou exclusão.
* duração de saudação para acesso deve ser um mínimo de três (3) semanas a partir de quando o URI de assinatura de acesso compartilhado Olá é criado.
* toosafeguard para o horário UTC dia selecione Olá antes Olá data atual. Por exemplo, se Olá a data atual for 6 de outubro de 2014, selecione 5/10/2014.

URL da SAS pode ser gerada na tooshare de várias maneiras o VHD para o Azure Marketplace.
A seguir são Olá 3 ferramentas recomendadas:

1.  Gerenciador de Armazenamento do Azure
2.  Microsoft Storage Explorer
3.  CLI do Azure

**Gerenciador de Armazenamento do Azure (recomendado para usuários do Windows)**

Estas são as etapas de saudação para gerar a URL de SAS usando o Azure Storage Explorer

1. Baixe o [Gerenciador de Armazenamento do Azure 6 Visualização 3](https://azurestorageexplorer.codeplex.com/) do CodePlex. Vá muito[visualização do Azure Storage Explorer 6](https://azurestorageexplorer.codeplex.com/) e clique em **"Baixa"**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_01.png)

2. Baixe [AzureStorageExplorer6Preview3.zip](https://azurestorageexplorer.codeplex.com/downloads/get/891668) e instale-lo após descompactá-lo.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_02.png)

3. Após a instalação, abra o aplicativo hello.
4. Clique em **Adicionar Conta**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_03.png)

5. Especifique o nome de conta de armazenamento hello, chave de conta de armazenamento e domínio de pontos de extremidade de armazenamento. Essa é a conta de armazenamento de saudação na sua assinatura do Azure onde você manteve o VHD no portal do Azure.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_04.png)

6. Depois que o Azure Storage Explorer é conectado tooyour conta de armazenamento específica, ela será iniciada mostrando todos Olá contém na conta de armazenamento hello. Selecione o contêiner Olá onde você copiou o arquivo VHD de disco de sistema operacional de Olá (também discos de dados se elas forem aplicáveis para seu cenário).

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_05.png)

7. Depois de selecionar o contêiner de blob hello, Azure Storage Explorer inicia mostrando arquivos Olá contêiner hello. Selecione o arquivo de imagem da saudação (. vhd) que precisa toobe enviada.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_06.png)

8.  Depois de selecionar o arquivo. vhd de saudação no contêiner de saudação, clique em Olá **segurança** guia.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_07.png)

9.  Em Olá **segurança de contêiner de Blob** caixa de diálogo, deixe padrões Olá Olá **nível de acesso** guia e, em seguida, clique em **assinaturas de acesso compartilhado** guia.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_08.png)

10. Siga as próximas etapas, Olá toogenerate um URI de assinatura de acesso compartilhado para a imagem de VHD hello:

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_09.png)

    a. **O acesso permitido do:** toosafeguard para o horário UTC dia selecione Olá antes Olá data atual. Por exemplo, se Olá a data atual for 6 de outubro de 2014, selecione 5/10/2014.

    b. **O acesso permitido para:** selecionar uma data que seja pelo menos três semanas após Olá **acesso permitido do** Data.

    c. **Ações permitidas:** Olá selecione **lista** e **leitura** permissões.

    d. Se você selecionou corretamente o arquivo. vhd, o arquivo é exibido no **tooaccess nome de Blob** com extensão VHD.

    e. Clique em **Gerar Assinatura**.

    f. Em **gerado compartilhado acesso assinatura URI desse contêiner**, procure Olá a seguir como destacado acima:

       - Certifique-se de que a imagem do nome do arquivo e **". vhd"** no hello URI.
       - No final da saudação da assinatura hello, verifique se **"= rl"** é exibida. Isso demonstra que os acessos de leitura e lista foram fornecidos com êxito.
       - No meio da assinatura hello, verifique se **"sr = c"** é exibida. Isso demonstra que você tem acesso ao nível de contêiner

11. tooensure Olá gerado compartilhados funciona URI de assinatura de acesso, clique em **teste no navegador**. Ele deve iniciar o processo de download de saudação.

12. Copie o URI de assinatura de acesso compartilhado hello. Isso é Olá URI toopaste em Olá Portal de publicação.

13. Repita as etapas 6-10 para cada VHD em Olá SKU.

**Gerenciador de Armazenamento do Microsoft Azure (Windows/MAC/Linux)**

Estas são as etapas de saudação para gerar a URL de SAS usando o Microsoft Azure Storage Explorer

1.  Baixe o formulário do Gerenciador de Armazenamento do Microsoft Azure no site [http://storageexplorer.com/](http://storageexplorer.com/). Vá muito[Microsoft Azure Storage Explorer](http://storageexplorer.com/releasenotes.html) e clique em **"Fazer Download do Windows"**.

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_10.png)

2.  Após a instalação, abra o aplicativo hello.

3.  Clique em **Adicionar Conta**.

4.  Configurar a assinatura do Microsoft Azure Storage Explorer tooyour por conta tooyour de entrada

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_11.png)

5.  Vá toostorage conta e selecione Olá contêiner

6.  Selecione **“Obter a assinatura de acesso ao compartilhamento...”** usando o botão direito do mouse do hello **contêiner**

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_12.png)

7.  Hora de início da atualização, Hora de expiração e Permissões conforme mostrado no seguinte

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_13.png)

    a.  **Hora de início:** toosafeguard para o horário UTC dia selecione Olá antes Olá data atual. Por exemplo, se Olá a data atual for 6 de outubro de 2014, selecione 5/10/2014.

    b.  **Tempo de expiração:** selecionar uma data que seja pelo menos três semanas após Olá **Start Time** Data.

    c.  **Permissões:** Olá selecione **lista** e **leitura** permissões

8.  Copie o URI da assinatura de acesso compartilhado do contêiner

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_14.png)

    URL SAS gerada é de nível de contêiner e agora precisamos de nome do VHD tooadd nele.

    Formato da URL SAS de nível de contêiner: `https://testrg009.blob.core.windows.net/vhds?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Insira o nome do VHD após o nome de contêiner de saudação na URL SAS como abaixo`https://testrg009.blob.core.windows.net/vhds/<VHD NAME>?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    Exemplo:

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_15.png)

    TestRGVM201631920152.vhd é hello VHD nome, URL de SAS do VHD será`https://testrg009.blob.core.windows.net/vhds/TestRGVM201631920152.vhd?st=2016-04-22T23%3A05%3A00Z&se=2016-04-30T23%3A05%3A00Z&sp=rl&sv=2015-04-05&sr=c&sig=J3twCQZv4L4EurvugRW2klE2l2EFB9XyM6K9FkuVB58%3D`

    - Certifique-se de que a imagem do nome do arquivo e **". vhd"** no hello URI.
    - No meio da assinatura hello, verifique se **"sp = rl"** é exibida. Isso demonstra que os acessos de leitura e lista foram fornecidos com êxito.
    - No meio da assinatura hello, verifique se **"sr = c"** é exibida. Isso demonstra que você tem acesso ao nível de contêiner

9.  tooensure que Olá funciona URI de assinatura de acesso compartilhado gerada, testá-lo no navegador. Ele deve iniciar o processo de download de saudação

10. Copie o URI de assinatura de acesso compartilhado hello. Isso é Olá URI toopaste em Olá Portal de publicação.

11. Repita essas etapas para cada VHD em Olá SKU.

**CLI do Azure (recomendado para não Windows e Integração Contínua)**

Estas são as etapas de saudação para gerar a URL de SAS usando a CLI do Azure

1.  Baixe a CLI do Microsoft Azure [aqui](https://azure.microsoft.com/en-in/documentation/articles/xplat-cli-install/). Você também pode encontrar links diferentes para **[Windows](http://aka.ms/webpi-azure-cli)** e **[MAC OS](http://aka.ms/mac-azure-cli)**.

2.  Após concluir o download, instale-o

3.  Crie um arquivo do PowerShell com o código a seguir e salve-o no local

          $conn="DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<Storage Account Key>"
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl <Permission End Date> -c $conn --start <Permission Start Date>  

    Atualizar a seguir Olá parâmetros acima

    a. **`<StorageAccountName>`**: informe o nome da conta de armazenamento

    b. **`<Storage Account Key>`**: informe a chave de conta de armazenamento

    c. **`<Permission Start Date>`**: toosafeguard para o horário UTC dia selecione Olá antes Olá data atual. Por exemplo, se hello data atual for 26 de outubro de 2016, em seguida, o valor deve ser 25/10/2016

    d. **`<Permission End Date>`**: Selecione uma data que seja pelo menos três semanas após Olá **data de início**. O valor deverá ser **02/11/2016**.

    A seguir é o código de exemplo hello depois de atualizar os parâmetros corretos

          $conn="DefaultEndpointsProtocol=https;AccountName=st20151;AccountKey=TIQE5QWMKHpT5q2VnF1bb+NUV7NVMY2xmzVx1rdgIVsw7h0pcI5nMM6+DVFO65i4bQevx21dmrflA91r0Vh2Yw=="
          azure storage container list vhds -c $conn
          azure storage container sas create vhds rl 11/02/2016 -c $conn --start 10/25/2016  

4.  Abra o editor do Powershell com o modo de “Executar como Administrador” e abra o arquivo na etapa 3.

5.  Script de execução hello e fornecerá que Olá URL SAS para acesso de nível de contêiner

    A seguir serão saída Olá Olá assinatura SAS e cópia Olá realçado partes em um bloco de notas

    ![desenho](media/marketplace-publishing-vm-image-creation/img5.2_16.png)

6.  Agora, você receberá o nível de contêiner URL SAS e você precisará tooadd VHD nome nele.

    No. de URL de SAS de nível de contêiner

    `https://st20151.blob.core.windows.net/vhds?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

7.  Inserir nome do VHD após o nome do contêiner de saudação na URL SAS, conforme mostrado abaixo`https://st20151.blob.core.windows.net/vhds/<VHDName>?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    Exemplo:

    TestRGVM201631920152.vhd é hello VHD nome, URL de SAS do VHD será

    `https://st20151.blob.core.windows.net/vhds/ TestRGVM201631920152.vhd?st=2016-10-25T07%3A00%3A00Z&se=2016-11-02T07%3A00%3A00Z&sp=rl&sv=2015-12-11&sr=c&sig=wnEw9RfVKeSmVgqDfsDvC9IHhis4x0fc9Hu%2FW4yvBxk%3D`

    - Certifique-se de que seu nome de arquivo de imagem e ". vhd" são Olá URI.
    -   No meio da assinatura hello, verifique se "sp = rl" é exibida. Isso demonstra que os acessos de leitura e lista foram fornecidos com êxito.
    -   No meio da assinatura hello, verifique se "sr = c" é exibida. Isso demonstra que você tem acesso ao nível de contêiner

8.  tooensure que Olá funciona URI de assinatura de acesso compartilhado gerada, testá-lo no navegador. Ele deve iniciar o processo de download de saudação

9.  Copie o URI de assinatura de acesso compartilhado hello. Isso é Olá URI toopaste em Olá Portal de publicação.

10. Repita essas etapas para cada VHD em Olá SKU.


### <a name="53-provide-information-about-hello-vm-image-and-request-certification-in-hello-publishing-portal"></a>5.3 fornecem informações sobre a imagem da VM hello e solicitação de certificação no Portal de publicação de saudação
Depois que você criou sua oferta e SKU, você deve inserir os detalhes da imagem Olá associados SKU:

1. Vá toohello [Portal de publicação][link-pubportal]e entre com sua conta do vendedor.
2. Selecione Olá **imagens da VM** guia.
3. Identificador de Olá listada na parte superior de saudação da página de saudação é realmente o identificador de oferta hello e identificador SKU de saudação não.
4. Preencha as propriedades Olá Olá **SKUs** seção.
5. Em **família de sistemas operacionais**, clique em tipo de sistema operacional Olá associado Olá no VHD do sistema operacional.
6. Em Olá **sistema operacional** caixa, descrevem o sistema operacional de saudação. Considere um formato como família do sistema operacional, tipo, versão e atualizações. Um exemplo é o “Windows Server Datacenter 2014 R2”.
7. Selecione toosix recomendado tamanhos de máquina virtual. Essas são as recomendações que obtém cliente toohello exibidas na folha de camada de preços Olá no hello Portal do Azure quando decidir toopurchase e implantar a imagem. **Essas são apenas recomendações. Prezado cliente é capaz de tooselect qualquer tamanho VM que acomoda discos Olá especificado em sua imagem.**
8. Insira a versão de saudação. o campo de versão Olá encapsula uma versão semântica tooidentify hello e as atualizações:
   * Versões devem ser do formato de saudação X.Y.Z, onde X, Y e Z são números inteiros.
   * Imagens em SKUs diferentes podem ter diferentes versões principais e secundárias.
   * Versões dentro de uma SKU só devem ser alterações incrementais, o que aumentam a versão de patch da saudação (Z de X.Y.Z).
9. Em Olá **URL do VHD de sistema operacional** , digite o URI criado para o VHD do sistema operacional Olá de assinatura de acesso compartilhado hello.
10. Se houver discos de dados associados a este SKU, selecione Olá unidade lógica número (LUN) toowhich você gostaria que este toobe de disco de dados montado após a implantação.
11. Em Olá **URL do VHD do LUN X** , digite o URI criado para dados primeiro saudação VHD de assinatura de acesso compartilhado hello.

    ![desenho](media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-3.png)


## <a name="common-sas-url-issues--fixes"></a>Problemas comuns e correções da URL de SAS

|Problema|Mensagem de Falha|Correção|Link da Documentação|
|---|---|---|---|
|Falha ao copiar imagens – "?" não foi encontrado na URL SAS|Falha: Copiando Imagens. Não é possível toodownload blob desde Uri SAS.|Atualização Olá Url SAS usando ferramentas recomendadas|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens – Os parâmetros “st” e “se” não existem na URL SAS|Falha: Copiando Imagens. Não é possível toodownload blob desde Uri SAS.|Atualizar Olá Url SAS com datas de início e término nele|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar as imagens – “sp=rl” não existe URL SAS|Falha: Copiando Imagens. Não é possível toodownload blob desde Uri SAS|Atualizar Olá Url SAS com as permissões definidas como "Ler" e "lista|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens – A URL SAS tem espaços em branco no nome do vhd|Falha: Copiando Imagens. Não é possível toodownload blob desde Uri SAS.|Atualizar Olá Url SAS, sem espaços em branco|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|
|Falha ao copiar imagens – Erro de autorização da URL SAS|Falha: Copiando Imagens. Blob toodownload não é possível devido a erro de tooauthorization|Regenerar Olá Url SAS|[https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)|


## <a name="next-step"></a>Próxima etapa
Depois de terminar com detalhes SKU hello, você pode mover forward toohello [guia de conteúdo de marketing do Azure Marketplace][link-pushstaging]. Essa etapa do processo de publicação de saudação, você fornece Olá marketing conteúdo, preço e antes de necessárias outras informações muito**etapa 3: testar sua VM oferecem em preparo**, onde você testar vários cenários de caso de uso antes de implantar Olá oferta toohello Azure Marketplace para visibilidade pública e compra.  

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)

[img-acom-1]:media/marketplace-publishing-vm-image-creation/vm-image-acom-datacenter.png
[img-portal-vm-size]:media/marketplace-publishing-vm-image-creation/vm-image-portal-size.png
[img-portal-vm-create]:media/marketplace-publishing-vm-image-creation/vm-image-portal-create-vm.png
[img-portal-vm-location]:media/marketplace-publishing-vm-image-creation/vm-image-portal-location.png
[img-portal-vm-rdp]:media/marketplace-publishing-vm-image-creation/vm-image-portal-rdp.png
[img-azstg-add]:media/marketplace-publishing-vm-image-creation/vm-image-storage-add.png
[img-manage-vm-new]:media/marketplace-publishing-vm-image-creation/vm-image-manage-new.png
[img-manage-vm-select]:media/marketplace-publishing-vm-image-creation/vm-image-manage-select.png
[img-cert-vm-key-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-keyfile-linux.png
[img-cert-vm-pswd-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-linux.png
[img-cert-vm-pswd-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-password-win.png
[img-cert-vm-test-lnx]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-linux.png
[img-cert-vm-test-win]:media/marketplace-publishing-vm-image-creation/vm-image-certification-test-sample-win.png
[img-cert-vm-results]:media/marketplace-publishing-vm-image-creation/vm-image-certification-results.png
[img-cert-vm-questionnaire]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire.png
[img-cert-vm-questionnaire-2]:media/marketplace-publishing-vm-image-creation/vm-image-certification-questionnaire-2.png
[img-pubportal-vm-skus]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus.png
[img-pubportal-vm-skus-2]:media/marketplace-publishing-vm-image-creation/vm-image-pubportal-skus-2.png

[link-pushstaging]:marketplace-publishing-push-to-staging.md
[link-github-waagent]:https://github.com/Azure/WALinuxAgent
[link-azure-codeplex]:https://azurestorageexplorer.codeplex.com/
[link-azure-2]:../storage/blobs/storage-dotnet-shared-access-signature-part-2.md
[link-azure-1]:../storage/common/storage-dotnet-shared-access-signature-part-1.md
[link-msft-download]:http://www.microsoft.com/download/details.aspx?id=44299
[link-technet-3]:https://technet.microsoft.com/library/hh846766.aspx
[link-technet-2]:https://msdn.microsoft.com/library/dn495261.aspx
[link-azure-portal]:https://portal.azure.com
[link-pubportal]:https://publish.windowsazure.com
[link-sql-2014-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014enterprisewindowsserver2012r2/
[link-sql-2014-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014standardwindowsserver2012r2/
[link-sql-2014-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2014webwindowsserver2012r2/
[link-sql-2012-ent]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2enterprisewindowsserver2012/
[link-sql-2012-std]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2standardwindowsserver2012/
[link-sql-2012-web]:http://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2012sp2webwindowsserver2012/
[link-datactr-2012-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012r2datacenter/
[link-datactr-2012]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2012datacenter/
[link-datactr-2008-r2]:http://azure.microsoft.com/marketplace/partners/microsoft/windowsserver2008r2sp1/
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-technet-1]:https://technet.microsoft.com/library/hh848454.aspx
[link-azure-vm-2]:./virtual-machines-linux-agent-user-guide/
[link-openssl]:https://www.openssl.org/
[link-intsvc]:http://www.microsoft.com/download/details.aspx?id=41554
[link-python]:https://www.python.org/

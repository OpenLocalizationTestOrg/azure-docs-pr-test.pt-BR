---
title: "Usar o PowerShell para criar uma VM com um servidor de relatório no modo nativo | Microsoft Docs"
description: "Este tópico descreve e fornece orientação para a implantação e a configuração de um servidor de relatório em modo nativo do SQL Server Reporting Services em uma Máquina Virtual do Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="319bd-103">Use o PowerShell para criar uma VM do Azure com um servidor de relatório em modo nativo</span><span class="sxs-lookup"><span data-stu-id="319bd-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="319bd-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="319bd-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="319bd-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="319bd-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="319bd-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="319bd-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="319bd-107">Este tópico descreve e fornece orientação para a implantação e a configuração de um servidor de relatório em modo nativo do SQL Server Reporting Services em uma Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="319bd-108">As etapas neste documento usam uma combinação de etapas manuais para criar a máquina virtual e um script do Windows PowerShell para configurar o Reporting Services na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="319bd-109">O script de configuração inclui a abertura de uma porta de firewall para HTTP ou HTTPs.</span><span class="sxs-lookup"><span data-stu-id="319bd-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="319bd-110">Se você não precisar de **HTTPS** no servidor de relatório, **ignorar a etapa 2**.</span><span class="sxs-lookup"><span data-stu-id="319bd-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="319bd-111">Depois de criar a VM na etapa 1, vá até a seção Usar o script para configurar o servidor de relatório e HTTP.</span><span class="sxs-lookup"><span data-stu-id="319bd-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="319bd-112">Após a execução do script, o servidor de relatório estará pronto para ser usado.</span><span class="sxs-lookup"><span data-stu-id="319bd-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="319bd-113">Pré-requisitos e suposições</span><span class="sxs-lookup"><span data-stu-id="319bd-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="319bd-114">**Assinatura do Azure**: verifique o número de núcleos disponíveis em sua Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="319bd-115">Se você criar o tamanho recomendado de VM, **A3**, precisará de **4** núcleos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="319bd-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="319bd-116">Se você usar um tamanho de VM **A2**, precisará de **2** núcleos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="319bd-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="319bd-117">Para verificar o limite de núcleos de sua assinatura, no portal clássico do Azure, clique em CONFIGURAÇÕES no painel esquerdo e clique em USO no menu superior.</span><span class="sxs-lookup"><span data-stu-id="319bd-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="319bd-118">Para aumentar a cota de núcleos, entre em contato com o [Suporte do Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="319bd-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="319bd-119">Para saber mais sobre o tamanho da VM, consulte [Tamanhos de máquinas virtuais do Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="319bd-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="319bd-120">**Script do Windows PowerShell**: o tópico supõe que você tenha um conhecimento funcional básico do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="319bd-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="319bd-121">Para saber mais sobre como usar o Windows PowerShell, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="319bd-122">Iniciando o Windows PowerShell no Windows Server</span><span class="sxs-lookup"><span data-stu-id="319bd-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="319bd-123">Introdução ao Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="319bd-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="319bd-124">Etapa 1: provisionar uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="319bd-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="319bd-125">Navegue até o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="319bd-126">Clique em **Máquinas Virtuais** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="319bd-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![máquinas virtuais do microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="319bd-128">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="319bd-128">Click **New**.</span></span>
   
    ![botão novo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="319bd-130">Clique em **Da Galeria**.</span><span class="sxs-lookup"><span data-stu-id="319bd-130">Click **From Gallery**.</span></span>
   
    ![nova vm da galeria](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="319bd-132">Clique em **SQL Server 2014 RTM Standard – Windows Server 2012 R2** e clique na seta para continuar.</span><span class="sxs-lookup"><span data-stu-id="319bd-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="319bd-134">Se você precisar do recurso de assinaturas voltadas para dados do Reporting Services, escolha **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="319bd-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="319bd-135">Para saber mais sobre as edições do SQL Server e o suporte dos recursos, consulte [Recursos com Suporte das Edições do SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="319bd-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="319bd-136">Na página **Configuração da máquina virtual** , edite os seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="319bd-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="319bd-137">Se houver mais de uma **DATA DE LANÇAMENTO DA VERSÃO**, selecione a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="319bd-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="319bd-138">**Nome da Máquina Virtual**: o nome da máquina também é usado na próxima página de configuração como o nome DNS do Serviço de Nuvem padrão.</span><span class="sxs-lookup"><span data-stu-id="319bd-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="319bd-139">O nome DNS deve ser exclusivo em todo o serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="319bd-140">Considere a configuração da VM com um nome de computador que descreva a utilização da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="319bd-141">Por exemplo, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="319bd-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="319bd-142">**Camada**: Standard</span><span class="sxs-lookup"><span data-stu-id="319bd-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="319bd-143">**Tamanho:A3** é o tamanho recomendado da VM para as cargas de trabalho do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="319bd-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="319bd-144">Se uma VM for usada apenas como um servidor de relatório, o tamanho de VM A2 será suficiente, a menos que o servidor de relatório enfrente uma grande carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="319bd-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="319bd-145">Para saber mais sobre preços da VM, consulte [Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="319bd-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="319bd-146">**Novo Nome de Usuário**: o nome fornecido é criado como um administrador na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="319bd-147">**Nova Senha** e **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="319bd-148">Essa senha será usada para a nova conta de administrador, portanto, recomendamos o uso de uma senha forte.</span><span class="sxs-lookup"><span data-stu-id="319bd-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="319bd-149">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-149">Click **Next**.</span></span> <span data-ttu-id="319bd-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="319bd-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="319bd-151">Na próxima página edite os campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="319bd-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="319bd-152">**Serviço de Nuvem**: selecione **Criar um novo Serviço de Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="319bd-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="319bd-153">**Nome DNS do Serviço de Nuvem**: é o nome DNS público do Serviço de Nuvem associado à VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="319bd-154">O nome padrão é o nome que você digitou para a VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="319bd-155">Se em etapas posteriores do tópico você criar um certificado SSL confiável e o nome DNS for usado para o valor de "**Emitido para**" do certificado.</span><span class="sxs-lookup"><span data-stu-id="319bd-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="319bd-156">**Região/Grupo de Afinidades/Rede Virtual**: escolha a região mais próxima de seus usuários finais.</span><span class="sxs-lookup"><span data-stu-id="319bd-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="319bd-157">**Conta de Armazenamento**: use uma conta de armazenamento gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="319bd-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="319bd-158">**Conjunto de Disponibilidades**: nenhum.</span><span class="sxs-lookup"><span data-stu-id="319bd-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="319bd-159">**PONTOS DE EXTREMIDADE**: mantenha os pontos de extremidade **Área de Trabalho Remota** e **PowerShell** e adicione o ponto de extremidade HTTP ou HTTPS, dependendo de seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="319bd-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="319bd-160">**HTTP**: as portas pública e privada padrão são **80**.</span><span class="sxs-lookup"><span data-stu-id="319bd-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="319bd-161">Se você usar uma porta privada diferente de 80, modifique **$HTTPport = 80** no script http.</span><span class="sxs-lookup"><span data-stu-id="319bd-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="319bd-162">**HTTPS**: as portas pública e privada padrão são **443**.</span><span class="sxs-lookup"><span data-stu-id="319bd-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="319bd-163">Uma prática recomendada de segurança é alterar a porta privada e configurar o firewall e o servidor de relatório para usar a porta privada.</span><span class="sxs-lookup"><span data-stu-id="319bd-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="319bd-164">Para saber mais sobre os pontos de extremidade, consulte [Como Configurar a Comunicação com uma Máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="319bd-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="319bd-165">Se você usar uma porta diferente da 443, altere o parâmetro **$HTTPsport = 443** no script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="319bd-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="319bd-166">Clique em Próximo.</span><span class="sxs-lookup"><span data-stu-id="319bd-166">Click next .</span></span> ![Próximo](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="319bd-168">Na última página do assistente, mantenha o padrão **Instalar o agente de VM** selecionado.</span><span class="sxs-lookup"><span data-stu-id="319bd-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="319bd-169">As etapas neste tópico não utilizam o agente de VM, mas se você planeja manter essa VM, o agente de VM e as extensões permitirão o aprimoramento da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="319bd-170">Para saber mais sobre o agente de VM, consulte [Agente de VM e Extensões – Parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="319bd-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="319bd-171">Uma das extensões padrão instaladas e em execução é a “BGINFO”, que exibe na área de trabalho da VM informações sobre o sistema, por exemplo, o IP interno e o espaço disponível na unidade.</span><span class="sxs-lookup"><span data-stu-id="319bd-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="319bd-172">Clique em Concluído.</span><span class="sxs-lookup"><span data-stu-id="319bd-172">Click complete .</span></span> ![Ok](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="319bd-174">O **Status** da VM é exibido como **Iniciando (Provisionando)** durante o processo de provisionamento. Em seguida, é exibido como **Executando** quando a VM é provisionada e está pronta para ser usada.</span><span class="sxs-lookup"><span data-stu-id="319bd-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="319bd-175">Etapa 2: criar um certificado de servidor</span><span class="sxs-lookup"><span data-stu-id="319bd-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="319bd-176">Se você não exigir o HTTPS no servidor de relatório, poderá **ignorar a etapa 2** e ir para a seção **Usar o script para configurar o servidor de relatório e HTTP**.</span><span class="sxs-lookup"><span data-stu-id="319bd-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="319bd-177">Use o script HTTP para configurar rapidamente o servidor de relatório e deixá-lo pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="319bd-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="319bd-178">Para usar HTTPS na VM, será necessário um certificado SSL confiável.</span><span class="sxs-lookup"><span data-stu-id="319bd-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="319bd-179">Dependendo do cenário, você poderá usar um dos dois métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="319bd-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="319bd-180">Um certificado SSL válido emitido por uma Autoridade de Certificação (CA) e de confiança da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="319bd-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="319bd-181">Exige-se que os certificados raiz de CA sejam distribuídos por meio do Microsoft Root Certificate Program.</span><span class="sxs-lookup"><span data-stu-id="319bd-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="319bd-182">Para saber mais sobre esse programa, consulte [SSL Root Certificate Program (CAs membros) do Windows](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) e do [Windows Phone 8 e Introdução ao Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="319bd-183">Um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="319bd-183">A self-signed certificate.</span></span> <span data-ttu-id="319bd-184">Os certificados autoassinados não são recomendados para ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="319bd-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="319bd-185">Para usar um certificado criado por uma Autoridade de Certificação (CA) confiável</span><span class="sxs-lookup"><span data-stu-id="319bd-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="319bd-186">**Solicite um certificado do servidor para o site em uma autoridade de certificação**.</span><span class="sxs-lookup"><span data-stu-id="319bd-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="319bd-187">Você pode usar o Assistente de Certificado de Servidor Web para gerar um arquivo de solicitação de certificado (Certreq.txt) e enviá-lo a uma autoridade de certificação ou para gerar uma solicitação para uma autoridade de certificação online.</span><span class="sxs-lookup"><span data-stu-id="319bd-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="319bd-188">Por exemplo, os Serviços de Certificados da Microsoft no Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="319bd-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="319bd-189">Dependendo do nível de garantia de identificação oferecido por seu certificado de servidor, talvez demore alguns dias até vários meses para que a autoridade de certificação aprove sua solicitação e envie um arquivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="319bd-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="319bd-190">Para saber mais sobre como solicitar certificados de servidor, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="319bd-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="319bd-192">Ferramentas de segurança para administrar o Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="319bd-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="319bd-193">Ferramentas de segurança para administrar o Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="319bd-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="319bd-194">O campo **emitido para** do certificado SSL confiável deve ser igual ao **NOME DNS do Serviço de Nuvem** usado para a nova VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="319bd-195">**Instale o certificado do servidor no servidor Web**.</span><span class="sxs-lookup"><span data-stu-id="319bd-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="319bd-196">Nesse caso, o servidor Web é a VM que hospeda o servidor de relatório, e o site é criado em etapas posteriores durante a configuração do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="319bd-197">Para saber mais sobre como instalar o certificado do servidor no servidor Web usando o snap-in do MMC de Certificados, consulte [Instalar um certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="319bd-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="319bd-198">Se você quiser usar o script incluído neste tópico para configurar o servidor de relatório, o valor de **impressão digital** dos certificados será exigido como um parâmetro do script.</span><span class="sxs-lookup"><span data-stu-id="319bd-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="319bd-199">Consulte a próxima seção para obter detalhes sobre como obter a impressão digital do certificado.</span><span class="sxs-lookup"><span data-stu-id="319bd-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="319bd-200">Atribua o certificado do servidor ao servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="319bd-201">A atribuição será concluída na próxima seção, após a configuração do servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="319bd-202">Para usar o certificado autoassinado de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="319bd-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="319bd-203">Um certificado autoassinado foi criado na VM quando a VM foi provisionada.</span><span class="sxs-lookup"><span data-stu-id="319bd-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="319bd-204">O certificado tem o mesmo nome que o nome DNS da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="319bd-205">Para evitar erros de certificado, é necessário que o certificado seja de confiança na própria VM e também de todos os usuários do site.</span><span class="sxs-lookup"><span data-stu-id="319bd-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="319bd-206">Para confiar na CA raiz do certificado na VM Local, adicione o certificado às **Autoridades de Certificação Raiz Confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="319bd-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="319bd-207">A seguir, um resumo dos métodos exigidos.</span><span class="sxs-lookup"><span data-stu-id="319bd-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="319bd-208">Para obter etapas detalhadas sobre como confiar na CA, consulte [Instalar um Certificado do Servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="319bd-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="319bd-209">No portal clássico do Azure, selecione a VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="319bd-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="319bd-210">Dependendo da configuração do navegador, talvez seja necessário salvar um arquivo .rdp para conectar-se à VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![conectar-se à máquina virtual do azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="319bd-212">Use o nome de usuário da VM, o nome de usuário e a senha que você configurou na criação da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="319bd-213">Por exemplo, na imagem a seguir, o nome da VM é **ssrsnativecloud** e o nome de usuário é **testuser**.</span><span class="sxs-lookup"><span data-stu-id="319bd-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="319bd-215">Execute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="319bd-215">Run mmc.exe.</span></span> <span data-ttu-id="319bd-216">Para saber mais, consulte [Como Exibir Certificados com o Snap-in do MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="319bd-217">No menu **Arquivo** do aplicativo do console, adicione o snap-in **Certificados**, selecione **Conta de Computador** quando solicitado e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="319bd-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="319bd-218">Selecione **Computador Local** para gerenciar e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="319bd-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="319bd-219">Clique em **Ok**, expanda os nós **Certificados - Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="319bd-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="319bd-220">O certificado recebe o nome com base no nome DNS da VM e termina com **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="319bd-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="319bd-221">Clique com o botão direito do mouse no nome do certificado e clique em **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="319bd-222">Expanda o nó **Autoridades de Certificação Raiz Confiáveis**, clique com botão direito do mouse em **Certificados** e clique em **Colar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="319bd-223">Para validar, clique duas vezes no nome do certificado em **Autoridades de Certificação Raiz Confiáveis** , verifique se não há erros e veja seu certificado.</span><span class="sxs-lookup"><span data-stu-id="319bd-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="319bd-224">Se você quiser usar o script HTTPS incluído neste tópico para configurar o servidor de relatório, o valor da **Impressão digital** dos certificados será exigido como um parâmetro do script.</span><span class="sxs-lookup"><span data-stu-id="319bd-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="319bd-225">**Para obter o valor da impressão digital**, preencha o seguinte.</span><span class="sxs-lookup"><span data-stu-id="319bd-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="319bd-226">Também há um exemplo do PowerShell para recuperar a impressão digital na seção [Usar o script para configurar o servidor de relatório e HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="319bd-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="319bd-227">Clique duas vezes no nome do certificado, por exemplo, ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="319bd-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="319bd-228">Clique na guia **Detalhes** .</span><span class="sxs-lookup"><span data-stu-id="319bd-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="319bd-229">Clique em **Impressão digital**.</span><span class="sxs-lookup"><span data-stu-id="319bd-229">Click **Thumbprint**.</span></span> <span data-ttu-id="319bd-230">O valor da impressão digital é exibido no campo detalhes, por exemplo, ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="319bd-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="319bd-231">Copie a impressão digital e salve o valor para mais tarde ou edite o script agora.</span><span class="sxs-lookup"><span data-stu-id="319bd-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="319bd-232">(*) Antes de executar o script, remova os espaços entre os pares de valores.</span><span class="sxs-lookup"><span data-stu-id="319bd-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="319bd-233">Por exemplo, a impressão digital observada anteriormente agora seria ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="319bd-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="319bd-234">Atribua o certificado do servidor ao servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="319bd-235">A atribuição será concluída na próxima seção, após a configuração do servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="319bd-236">Se você estiver usando um certificado SSL autoassinado, o nome no certificado já corresponderá ao nome de host da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="319bd-237">Portanto, o DNS da máquina já estará registrado globalmente e poderá ser acessado de qualquer cliente.</span><span class="sxs-lookup"><span data-stu-id="319bd-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="319bd-238">Etapa 3: configurar servidor de relatório</span><span class="sxs-lookup"><span data-stu-id="319bd-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="319bd-239">Esta seção descreve a configuração da VM como um servidor de relatório em modo nativo do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="319bd-240">Você pode usar um dos métodos a seguir para configurar o servidor de relatório:</span><span class="sxs-lookup"><span data-stu-id="319bd-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="319bd-241">Usar o script para configurar o servidor de relatório</span><span class="sxs-lookup"><span data-stu-id="319bd-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="319bd-242">Usar o Gerenciador de Configuração para configurar o servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="319bd-243">Para obter etapas mais detalhadas, consulte a seção [Conectar a Máquina Virtual e Iniciar o Gerenciador de Configuração do Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="319bd-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="319bd-244">**Nota de Autenticação:** a autenticação do Windows é o método de autenticação recomendado e é a autenticação padrão do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="319bd-245">Somente os usuários configurados na VM podem acessar o Reporting Services e podem receber as funções do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="319bd-246">Usar o script para configurar o servidor de relatório e HTTP</span><span class="sxs-lookup"><span data-stu-id="319bd-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="319bd-247">Para usar o script do Windows PowerShell a fim de configurar o servidor de relatório, conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="319bd-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="319bd-248">A configuração inclui HTTP, não HTTPS:</span><span class="sxs-lookup"><span data-stu-id="319bd-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="319bd-249">No portal clássico do Azure, selecione a VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="319bd-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="319bd-250">Dependendo da configuração do navegador, talvez seja necessário salvar um arquivo .rdp para conectar-se à VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![conectar-se à máquina virtual do azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="319bd-252">Use o nome de usuário da VM, o nome de usuário e a senha que você configurou na criação da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="319bd-253">Por exemplo, na imagem a seguir, o nome da VM é **ssrsnativecloud** e o nome de usuário é **testuser**.</span><span class="sxs-lookup"><span data-stu-id="319bd-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="319bd-255">Na VM, abra **ISE do Windows PowerShell** com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="319bd-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="319bd-256">O ISE do PowerShell está instalado por padrão no Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="319bd-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="319bd-257">Recomendamos o uso do ISE, em vez de uma janela padrão do Windows PowerShell, para que você possa colar o script no ISE, modificar e executar o script.</span><span class="sxs-lookup"><span data-stu-id="319bd-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="319bd-258">No ISE do Windows PowerShell, clique no menu **Exibir** e clique em **Mostrar Painel de Script**.</span><span class="sxs-lookup"><span data-stu-id="319bd-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="319bd-259">Copie o script a seguir e cole-o no painel de script do ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="319bd-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="319bd-260">Se você criou a VM com uma porta HTTP diferente de 80, modifique o parâmetro $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="319bd-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="319bd-261">Atualmente, o script está configurado para o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="319bd-262">Se você quiser executar o script do Reporting Services, modifique a parte da versão do caminho até o namespace para "v11", na instrução Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="319bd-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="319bd-263">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="319bd-263">Run the script.</span></span>

<span data-ttu-id="319bd-264">**Validação**: para verificar se a funcionalidade básica do servidor de relatório está funcionando, consulte a seção [Verificar a configuração](#verify-the-configuration) , mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="319bd-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="319bd-265">Usar o script para configurar o servidor de relatório e HTTPS</span><span class="sxs-lookup"><span data-stu-id="319bd-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="319bd-266">Para usar o Windows PowerShell a fim de configurar o servidor de relatório, conclua as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="319bd-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="319bd-267">A configuração inclui HTTPS, não HTTP.</span><span class="sxs-lookup"><span data-stu-id="319bd-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="319bd-268">No portal clássico do Azure, selecione a VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="319bd-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="319bd-269">Dependendo da configuração do navegador, talvez seja necessário salvar um arquivo .rdp para conectar-se à VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![conectar-se à máquina virtual do azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="319bd-271">Use o nome de usuário da VM, o nome de usuário e a senha que você configurou na criação da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="319bd-272">Por exemplo, na imagem a seguir, o nome da VM é **ssrsnativecloud** e o nome de usuário é **testuser**.</span><span class="sxs-lookup"><span data-stu-id="319bd-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![o logon inclui o nome da vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="319bd-274">Na VM, abra **ISE do Windows PowerShell** com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="319bd-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="319bd-275">O ISE do PowerShell está instalado por padrão no Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="319bd-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="319bd-276">Recomendamos o uso do ISE, em vez de uma janela padrão do Windows PowerShell, para que você possa colar o script no ISE, modificar e executar o script.</span><span class="sxs-lookup"><span data-stu-id="319bd-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="319bd-277">Para habilitar a execução de scripts, execute o seguinte comando do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="319bd-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="319bd-278">Em seguida, você pode executar o seguinte procedimento para verificar a política:</span><span class="sxs-lookup"><span data-stu-id="319bd-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="319bd-279">No ISE do **Windows PowerShell**, clique no menu **Exibir** e clique em **Mostrar Painel de Script**.</span><span class="sxs-lookup"><span data-stu-id="319bd-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="319bd-280">Copie o script a seguir e cole-o no painel de script do ISE do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="319bd-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="319bd-281">Modifique o parâmetro **$certificatehash** no script:</span><span class="sxs-lookup"><span data-stu-id="319bd-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="319bd-282">Esse é um parâmetro **obrigatório** .</span><span class="sxs-lookup"><span data-stu-id="319bd-282">This is a **required** parameter.</span></span> <span data-ttu-id="319bd-283">Se você não tiver salvo o valor do certificado nas etapas anteriores, use um dos métodos a seguir para copiar o valor de hash do certificado da impressão digital dos certificados:</span><span class="sxs-lookup"><span data-stu-id="319bd-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="319bd-284">Na VM, abra o ISE do Windows PowerShell e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="319bd-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="319bd-285">A saída parecerá com o seguinte: Se o script retornar uma linha em branco, a VM não terá um certificado configurado, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="319bd-285">The output will look similar to the following.</span></span> <span data-ttu-id="319bd-286">Consulte a seção [Para usar o Certificado Autoassinado das Máquinas Virtuais](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="319bd-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="319bd-287">OU</span><span class="sxs-lookup"><span data-stu-id="319bd-287">OR</span></span>
   * <span data-ttu-id="319bd-288">Na VM, execute mmc.exe e adicione o snap-in **Certificados** .</span><span class="sxs-lookup"><span data-stu-id="319bd-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="319bd-289">Sob o nó **Autoridades de Certificação Raiz Confiáveis** , clique duas vezes no nome do certificado.</span><span class="sxs-lookup"><span data-stu-id="319bd-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="319bd-290">Se você estiver usando o certificado autoassinado da VM, o certificado receberá o nome com base no nome DNS da VM e terminará com **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="319bd-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="319bd-291">Clique na guia **Detalhes** .</span><span class="sxs-lookup"><span data-stu-id="319bd-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="319bd-292">Clique em **Impressão digital**.</span><span class="sxs-lookup"><span data-stu-id="319bd-292">Click **Thumbprint**.</span></span> <span data-ttu-id="319bd-293">O valor da impressão digital é exibido no campo detalhes, por exemplo, af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="319bd-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="319bd-294">**Antes de executar o script**, remova os espaços entre os pares de valores.</span><span class="sxs-lookup"><span data-stu-id="319bd-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="319bd-295">Por exemplo, af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="319bd-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="319bd-296">Modifique o parâmetro **$httpsport** :</span><span class="sxs-lookup"><span data-stu-id="319bd-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="319bd-297">Se você usou a porta 443 para o ponto de extremidade HTTPS, não será necessário atualizar esse parâmetro no script.</span><span class="sxs-lookup"><span data-stu-id="319bd-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="319bd-298">Caso contrário, use o valor de porta selecionado quando você configurou o ponto de extremidade HTTPS privado na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="319bd-299">Modifique o parâmetro **$DNSName** :</span><span class="sxs-lookup"><span data-stu-id="319bd-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="319bd-300">O script é configurado para obter um certificado curinga $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="319bd-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="319bd-301">Se você não quiser configurar uma associação de certificado curinga, comente $DNSName ="+"e habilite a linha a seguir, a referência completa de $DNSNAme, ##$DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="319bd-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="319bd-302">Altere o valor de $DNSName se não quiser usar o nome DNS da máquina virtual para o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="319bd-303">Se você usar o parâmetro, o certificado também deverá usar esse nome, e será necessário registrar o nome globalmente em um servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="319bd-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="319bd-304">Atualmente, o script está configurado para o Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="319bd-305">Se você quiser executar o script do Reporting Services, modifique a parte da versão do caminho até o namespace para "v11", na instrução Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="319bd-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="319bd-306">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="319bd-306">Run the script.</span></span>

<span data-ttu-id="319bd-307">**Validação**: para verificar se a funcionalidade básica do servidor de relatório está funcionando, consulte a seção [Verificar a configuração](#verify-the-connection) , mais adiante neste tópico.</span><span class="sxs-lookup"><span data-stu-id="319bd-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="319bd-308">Para verificar a associação do certificado, abra um prompt de comando com privilégios administrativos e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="319bd-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="319bd-309">O resultado incluirá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="319bd-310">Usar o Gerenciador de Configuração para configurar o servidor de relatório</span><span class="sxs-lookup"><span data-stu-id="319bd-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="319bd-311">Se você não quiser executar o script do PowerShell para configurar o servidor de relatório, execute as etapas nesta seção para usar o gerenciador de configuração em modo nativo do Reporting Services para configurar o servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="319bd-312">No portal clássico do Azure, selecione a VM e clique em conectar.</span><span class="sxs-lookup"><span data-stu-id="319bd-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="319bd-313">Use o nome de usuário e a senha configurados durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![conectar-se à máquina virtual do azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="319bd-315">Execute a atualização do Windows e instale as atualizações da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="319bd-316">Se for necessário reinicializar a VM, reinicie e reconecte-se à VM no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="319bd-317">No menu Iniciar da VM, digite **Reporting Services** e abra o **Gerenciador de Configuração do Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="319bd-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="319bd-318">Mantenha os valores padrão para **Nome do Servidor** e **Instância do Servidor de Relatório**.</span><span class="sxs-lookup"><span data-stu-id="319bd-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="319bd-319">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-319">Click **Connect**.</span></span>
5. <span data-ttu-id="319bd-320">No painel esquerdo, clique em **URL do Serviço Web**.</span><span class="sxs-lookup"><span data-stu-id="319bd-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="319bd-321">Por padrão, o RS está configurado para a porta HTTP 80 com IP "Todos Atribuídos".</span><span class="sxs-lookup"><span data-stu-id="319bd-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="319bd-322">Para adicionar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="319bd-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="319bd-323">Em **Certificado SSL**: selecione o certificado que você deseja usar, por exemplo, [nome da VM].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="319bd-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="319bd-324">Se não houver um certificado listado, consulte a seção **Etapa 2: Criar um Certificado do Servidor** para obter informações sobre como instalar e confiar no certificado na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="319bd-325">Em **Porta SSL**: escolha 443.</span><span class="sxs-lookup"><span data-stu-id="319bd-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="319bd-326">Se você tiver configurado o ponto de extremidade HTTPS privado na VM com uma porta privada diferente, use esse valor aqui.</span><span class="sxs-lookup"><span data-stu-id="319bd-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="319bd-327">Clique em **Aplicar** e aguarde a conclusão da operação.</span><span class="sxs-lookup"><span data-stu-id="319bd-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="319bd-328">No painel esquerdo, clique em **Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="319bd-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="319bd-329">Clique em **Alterar Banco de Dado**s.</span><span class="sxs-lookup"><span data-stu-id="319bd-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="319bd-330">Clique em **Criar um novo banco de dados do servidor de relatório** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="319bd-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="319bd-331">Mantenha o **Nome do Servidor** padrão: como o nome da VM e mantenha o **Tipo de Autenticação** padrão como **Usuário Atual** – **Segurança Integrada**.</span><span class="sxs-lookup"><span data-stu-id="319bd-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="319bd-332">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-332">Click **Next**.</span></span>
   4. <span data-ttu-id="319bd-333">Mantenha o **Nome do Banco de Dados** padrão como **ReportServer** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="319bd-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="319bd-334">Mantenha o **Tipo de Autenticação** padrão como **Credenciais do Serviço** e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="319bd-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="319bd-335">Clique em **Próximo** on the **Resumo** .</span><span class="sxs-lookup"><span data-stu-id="319bd-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="319bd-336">Quando a configuração estiver concluída, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="319bd-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="319bd-337">No painel esquerdo, clique em **URL do Gerenciador de Relatórios**.</span><span class="sxs-lookup"><span data-stu-id="319bd-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="319bd-338">Mantenha o **Diretório Virtual** padrão como **Relatórios** e clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="319bd-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="319bd-339">Clique em **Sair** para fechar o Gerenciador de Configuração do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="319bd-340">Etapa 4: abrir a porta do Firewall do Windows</span><span class="sxs-lookup"><span data-stu-id="319bd-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="319bd-341">Se você tiver usado um dos scripts para configurar o servidor de relatório, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="319bd-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="319bd-342">O script incluiu uma etapa para abrir a porta do firewall.</span><span class="sxs-lookup"><span data-stu-id="319bd-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="319bd-343">A porta padrão era 80 para HTTP e 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="319bd-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="319bd-344">Para se conectar remotamente ao Gerenciador de Relatórios ou ao Servidor de Relatório na máquina virtual, será necessário ter um ponto de extremidade TCP na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="319bd-345">É necessário abrir a mesma porta no firewall da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="319bd-346">O ponto de extremidade foi criado durante o provisionamento da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="319bd-347">Esta seção fornece informações básicas sobre como abrir a porta do firewall.</span><span class="sxs-lookup"><span data-stu-id="319bd-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="319bd-348">Para saber mais, consulte [Configurar um firewall para acesso ao servidor de relatório](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="319bd-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="319bd-349">Se você tiver usado o script para configurar o servidor de relatório, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="319bd-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="319bd-350">O script incluiu uma etapa para abrir a porta do firewall.</span><span class="sxs-lookup"><span data-stu-id="319bd-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="319bd-351">Se você tiver configurado uma porta privada para HTTPS diferente de 443, modifique o script a seguir adequadamente.</span><span class="sxs-lookup"><span data-stu-id="319bd-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="319bd-352">Para abrir a porta **443** no Firewall do Windows, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="319bd-353">Abra uma janela do Windows PowerShell com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="319bd-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="319bd-354">Se você tiver usado uma porta diferente de 443 ao configurar o ponto de extremidade HTTPS na VM, atualize a porta no comando a seguir e execute o comando:</span><span class="sxs-lookup"><span data-stu-id="319bd-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="319bd-355">Após a conclusão do comando, **Ok** será exibido no prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="319bd-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="319bd-356">Para verificar se a porta está aberta, abra uma janela do Windows PowerShell e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="319bd-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="319bd-357">Verificar a configuração</span><span class="sxs-lookup"><span data-stu-id="319bd-357">Verify the configuration</span></span>
<span data-ttu-id="319bd-358">Para verificar se a funcionalidade básica do servidor de relatório está funcionando, abra seu navegador com privilégios administrativos e navegue até as seguintes URLs do servidor de relatório e do gerenciador de relatório:</span><span class="sxs-lookup"><span data-stu-id="319bd-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="319bd-359">Na VM, navegue até a URL do servidor de relatório:</span><span class="sxs-lookup"><span data-stu-id="319bd-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="319bd-360">Na VM, navegue até a URL do gerenciador de relatório:</span><span class="sxs-lookup"><span data-stu-id="319bd-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="319bd-361">No computador local, navegue até o Gerenciador de relatório **remoto** na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="319bd-362">Atualize o nome DNS no exemplo a seguir, conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="319bd-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="319bd-363">Quando receber uma solicitação por uma senha, use as credenciais de administrador que você criou durante o provisionamento da VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="319bd-364">O nome de usuário está no formato [Domínio]\[nome de usuário], em que o domínio é o nome de computador da VM, por exemplo, ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="319bd-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="319bd-365">Se você não estiver usando HTTP**S**, remova o **s** da URL.</span><span class="sxs-lookup"><span data-stu-id="319bd-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="319bd-366">Consulte a próxima seção para saber mais sobre como criar usuários adicionais na VM.</span><span class="sxs-lookup"><span data-stu-id="319bd-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="319bd-367">No computador local, navegue até a URL do servidor de relatório remoto.</span><span class="sxs-lookup"><span data-stu-id="319bd-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="319bd-368">Atualize o nome DNS no exemplo a seguir, conforme apropriado.</span><span class="sxs-lookup"><span data-stu-id="319bd-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="319bd-369">Se você não estiver usando HTTPS, remova o s da URL.</span><span class="sxs-lookup"><span data-stu-id="319bd-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="319bd-370">Criar usuários e atribuir funções</span><span class="sxs-lookup"><span data-stu-id="319bd-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="319bd-371">Após a configuração e verificação do servidor de relatório, uma tarefa administrativa comum é criar um ou mais usuários e atribuir usuários às funções do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="319bd-372">Para saber mais, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-372">For more information, see the following:</span></span>

* [<span data-ttu-id="319bd-373">Criar uma conta de usuário local</span><span class="sxs-lookup"><span data-stu-id="319bd-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="319bd-374">[Conceder ao Usuário Acesso a um Servidor de Relatório (Gerenciador de Relatórios)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="319bd-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="319bd-375">Criar e gerenciar atribuições de função</span><span class="sxs-lookup"><span data-stu-id="319bd-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="319bd-376">Para criar e publicar relatórios na máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="319bd-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="319bd-377">A tabela a seguir resume algumas opções disponíveis para publicação de relatórios existentes de um computador local para o servidor de relatório hospedado na Máquina Virtual do Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="319bd-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="319bd-378">**Script RS.exe**: use o script RS.exe para copiar itens de relatório de um servidor de relatório existente para sua Máquina Virtual do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="319bd-379">Para saber mais, consulte a seção "Modo nativo para Modo nativo – Máquina Virtual do Microsoft Azure" em [Exemplo de Script rs.exe do Reporting Services para Migrar o Conteúdo entre os Servidores de Relatório](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="319bd-380">**Construtor de Relatórios**: a máquina virtual inclui a versão de um clique do Construtor de Relatórios do Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="319bd-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="319bd-381">Para iniciar o Construtor de relatórios pela primeira vez na máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="319bd-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="319bd-382">Inicie o navegador com privilégios administrativos.</span><span class="sxs-lookup"><span data-stu-id="319bd-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="319bd-383">Navegue até o gerenciador de relatórios na máquina virtual e clique em **Construtor de Relatórios** na faixa de opções.</span><span class="sxs-lookup"><span data-stu-id="319bd-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="319bd-384">Para saber mais, consulte [Instalando, Desinstalando e Dando Suporte ao Construtor de Relatórios](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="319bd-385">**SQL Server Data Tools: VM**: se você criou a VM com o SQL Server 2012, o SQL Server Data Tools estará instalado na máquina virtual e poderá ser usado para criar **Projetos do Servidor de Relatório** e relatórios na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="319bd-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="319bd-386">O SQL Server Data Tools pode publicar os relatórios no servidor de relatório na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="319bd-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="319bd-387">Se você tiver criado a VM com o SQL Server 2014, instale o SQL Server Data Tools - BI para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="319bd-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="319bd-388">Para saber mais, confira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="319bd-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="319bd-389">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="319bd-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="319bd-390">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="319bd-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="319bd-391">SQL Server Data Tools e SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="319bd-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="319bd-392">**SQL Server Data Tools: Remoto**: no computador local, crie um projeto do Reporting Services no SQL Server Data Tools que contenha os relatórios do Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="319bd-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="319bd-393">Configure o projeto para conectar-se à URL do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="319bd-393">Configure the project to connect to the web service URL.</span></span>
  
    ![propriedades de projeto ssdt para projeto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="319bd-395">**Usar script**: use o script para copiar o conteúdo do servidor de relatório.</span><span class="sxs-lookup"><span data-stu-id="319bd-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="319bd-396">Para saber mais, consulte [Exemplo de Script rs.exe do Reporting Services para Migrar o Conteúdo entre os Servidores de Relatório](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="319bd-397">Minimizar o custo se você não estiver usando a VM</span><span class="sxs-lookup"><span data-stu-id="319bd-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="319bd-398">Para minimizar os encargos de suas Máquinas Virtuais do Azure quando elas não estiverem em uso, finalize a VM no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="319bd-399">Se você usar as opções de energia do Windows em uma VM para desligá-la, ainda receberá a cobrança do mesmo valor para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="319bd-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="319bd-400">Para reduzir os encargos, é necessário finalizar a VM no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="319bd-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="319bd-401">Se você não precisar mais da VM, lembre-se de excluí-la e também os arquivos .vhd associados para evitar os encargos de armazenamento. Para saber mais, consulte a seção de perguntas frequentes em [Detalhes de Preços das Máquinas Virtuais](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="319bd-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="319bd-402">Mais informações</span><span class="sxs-lookup"><span data-stu-id="319bd-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="319bd-403">Recursos</span><span class="sxs-lookup"><span data-stu-id="319bd-403">Resources</span></span>
* <span data-ttu-id="319bd-404">Para obter um conteúdo semelhante relacionado a uma implantação de servidor único do Business Intelligence do SQL Server e do SharePoint 2013, consulte [Usar o Windows PowerShell para Criar uma VM do Azure com o BI do SQL Server e o SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="319bd-405">Para obter um conteúdo semelhante relacionado a uma implantação com vários servidores do Business Intelligence do SQL Server e do SharePoint 2013, consulte [Implantar o Business Intelligence do SQL Server nas Máquinas Virtuais do Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="319bd-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="319bd-406">Para obter informações gerais relacionadas às implantações do Business Intelligence do SQL Server nas Máquinas Virtuais do Azure, consulte [Business Intelligence do SQL Server nas Máquinas Virtuais do Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="319bd-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="319bd-407">Para saber mais sobre o custo dos encargos de computação do Azure, consulte a guia Máquinas Virtuais da [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="319bd-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="319bd-408">Conteúdo da comunidade</span><span class="sxs-lookup"><span data-stu-id="319bd-408">Community Content</span></span>
* <span data-ttu-id="319bd-409">Para obter instruções detalhadas sobre como criar um servidor de relatório em modo nativo do Reporting Services sem usar script, consulte [Hospedando o serviço Relatórios SQL na máquina virtual Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="319bd-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="319bd-410">Links para outros recursos para SQL Server em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="319bd-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="319bd-411">Visão geral do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="319bd-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)


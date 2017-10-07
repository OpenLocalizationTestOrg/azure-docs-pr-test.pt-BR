---
title: "problemas de gerenciamento e aaaConfiguration para perguntas frequentes sobre serviços de nuvem do Azure Microsoft | Microsoft Docs"
description: "Este artigo lista Olá perguntas frequentes sobre a configuração e gerenciamento de serviços de nuvem do Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problemas de configuração e gerenciamento para Serviços de Nuvem do Azure: perguntas frequentes

Este artigo inclui perguntas frequentes sobre a configuração e o gerenciamento de [Serviços de Nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Como adicionar o site de toomy "nosniff"?
clientes tooprevent de detecção de tipos MIME hello, adicionar uma configuração em seu *Web. config* arquivo.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

Ela também pode ser adicionada como uma configuração no IIS. Comando a seguir de saudação Use com hello [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artigo.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Como fazer para personalizar o IIS para uma função web?
Usar script de inicialização IIS Olá da saudação [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artigo.

## <a name="i-cannot-scale-beyond-x-instances"></a>Não consigo dimensionar além de X instâncias
Sua assinatura do Azure tem um limite no número de saudação de núcleos que você pode usar. Dimensionamento não funcionará se você tiver usado todos os núcleos Olá disponíveis. Por exemplo, se você tiver um limite de 100 núcleos, isso significa você poderia ter 100 instâncias de máquina virtual A1 dimensionadas para seu serviço de nuvem ou 50 instâncias de máquina virtual A2.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Como implementar Acesso Baseado em Função para Serviços de Nuvem?
Serviços de nuvem não dá suporte a modelo de controle de acesso baseado em função (RBAC) hello, pois não é um serviço de Gerenciador de recursos do Azure com base.

Consulte [RBAC do Azure versus administradores de assinatura clássica](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Como definir o tempo limite de ociosidade Olá balanceador de carga do Azure?
Você pode especificar o tempo limite de saudação no arquivo de definição (csdef) do serviço como este:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Consulte [Novo: tempo limite de ociosidade configurável para o Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) para obter mais informações.

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>É possível engenheiros internos da Microsoft instâncias de serviço do RDP toocloud sem permissão?
Maneira de Microsoft tooRDP os engenheiros de um processo estrito que não permitirá interno em seu serviço de nuvem sem permissão (email ou outras comunicações escritas) por escrito do proprietário hello ou seu responsável.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Por que a cadeia de certificados de saudação do meu certificado SSL do serviço de nuvem está incompleto?
É recomendável que os clientes instalem Olá cadeia de certificados completa (certificado de folha, certificados intermediários e certificado raiz) em vez de apenas certificado de folha de saudação. Quando você instala o certificado de folha Olá apenas, você confiar na cadeia de certificados do Windows toobuild Olá percorrendo Olá CTL. Se intermitentes de rede ou problemas de DNS ocorrerem no Azure ou o Windows Update quando o Windows tenta toovalidate certificado de hello, certificado Olá pode ser considerado inválido. Instalando a cadeia de certificados completa hello, esse problema pode ser evitado. Olá blog em [como tooinstall um certificado encadeado SSL](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) mostra como toodo isso.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Como associar o um serviço de nuvem do toomy de endereço IP estático?
tooset um endereço IP estático, você precisa toocreate um IP reservado. Esse IP reservado pode ser associado tooa novo serviço ou tooan existente implantação em nuvem. Consulte Olá documentos para obter detalhes a seguir:
* [Como toocreate um endereço IP reservado](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Reservar um endereço IP de saudação de um serviço de nuvem existente](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Associar um reservado IP tooa novo serviço de nuvem](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Associar um tooa IP reservado executando a implantação](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Associar um serviço de nuvem tooa IP reservado por meio de um arquivo de configuração de serviço](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>O que é o limite de cota de saudação para meu serviço de nuvem?
Consulte [Limites específicos do serviço](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Por que a unidade Olá no meu serviço de nuvem VM Mostrar muito pouco espaço livre em disco?
Esse comportamento é esperado e não deve fazer com que qualquer aplicativo de tooyour do problema. Registro em log está ativado para Olá % uproot % unidade em máquinas virtuais de PaaS do Azure, que consome basicamente double Olá quantidade de espaço que arquivos normalmente ocupam. No entanto, há várias coisas toobe atento que essencialmente transformar isso em um problema.

Olá % approot % unidade tamanho é calculado como < tamanho do cspkg + tamanho máximo do diário > + uma margem de espaço livre, ou 1,5 GB, o que for maior. tamanho de saudação da VM não possui esse cálculo. (Olá tamanho da VM só afeta o tamanho de Olá de unidade temporária de c: Olá.) 

É a unidade sem suporte toowrite toohello % approot %. Se você estiver escrevendo toohello VM do Azure, você deve fazer isso em um recurso LocalStorage temporário (ou outra opção, como o armazenamento de Blob, arquivos do Azure, etc.). Portanto a quantidade de saudação de espaço livre na pasta Olá % approot % não é significativa. Se você não tiver certeza se seu aplicativo estiver gravando toohello % approot % unidade, você sempre pode deixar seu serviço execute por alguns dias e, em seguida, compare hello "antes" e "depois" tamanhos. 

Azure não gravará nada toohello % approot % unidade. Depois de hello VHD é criado a partir de seu cspkg e montado em Olá VM do Azure, Olá única coisa que pode gravar toothis unidade é seu aplicativo. 

configurações do diário Olá são não configuráveis, não é possível desligá-lo.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Quais são Olá recursos e as funcionalidades que fornece IPS/IDS básico do Azure e DDOS?
O Azure tem IPS/IDS no datacenter servidores físicos toodefend contra ameaças. Além disso, os clientes podem implantar soluções de segurança de terceiros, como firewalls de aplicativo Web, firewalls de rede, antimalware, IDS/IPS (sistema de detecção de intrusão/sistema de prevenção de intrusão) e muito mais. Para obter mais informações, consulte [Proteger seus dados e ativos e cumprir padrões de segurança globais](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft monitora continuamente a ameaças de toodetect de servidores, redes e aplicativos. A abordagem de gerenciamento de ameaças multipronged do Azure usa a detecção de intrusões, distribuída negação de serviço (DDoS) ataques prevenção, teste de penetração, análise comportamental, detecção de anomalias e aprendizado de máquina tooconstantly Fortaleça sua proteção e reduzir riscos. O Microsoft Antimalware para Azure protege os serviços de nuvem e as máquinas virtuais do Azure. Você tem soluções de segurança de terceiros Olá opção toodeploy Além disso, como paredes de incêndio de aplicativo web, os firewalls de rede, antimalware, detecção e prevenção de sistemas de intrusões (IDS/IPS) e muito mais.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Por que o IIS parar a gravação toohello diretório de log?
Cota de armazenamento local Olá para gravar o diretório de log toohello ter esgotado. Para corrigir isso, você pode executar uma destas três ações:
* Habilitar o diagnóstico para o IIS e diagnóstico Olá movidos periodicamente tooblob armazenamento.
* Remova manualmente os arquivos de log do hello diretório de log.
* Aumentar os limite de cota para recursos locais.

Para obter mais informações, consulte Olá documentos a seguir:
* [Armazenar e exibir dados de diagnóstico no Armazenamento do Azure](cloud-services-dotnet-diagnostics-storage.md)
* [Logs do IIS param de gravar no serviço de nuvem](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Qual é a finalidade de saudação do hello "Windows Azure ferramentas de criptografia para extensões de certificado"?
Esses certificados são criados automaticamente sempre que uma extensão é adicionada toohello serviço de nuvem. Normalmente, isso é Olá extensão WAD ou hello extensão RDP, mas é possível que outras pessoas, como Olá extensão Antimalware ou coletor de Log. Esses certificados são usados apenas para criptografar e descriptografar a configuração privada Olá para extensão de saudação. Data de expiração de saudação nunca é verificada, portanto, não importa se Olá certificado expirou. 

Você pode ignorar esses certificados. Se você quiser limpar Olá certificados, você pode tentar excluí-los todos. Azure emitirá um erro se você tentar toodelete um certificado que está em uso.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Como pode gerar uma assinatura solicitação certificado (CSR) sem "Ndo RDP" na instância de toohello?
Consulte Olá documento diretrizes a seguir:

>[Como obter um certificado para uso com o WAWS (Sites do Microsoft Azure)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Observe que uma CSR é apenas um arquivo de texto. Ele não tem toobe criado na máquina Olá onde certificado hello, por fim, será usado. Embora este documento foi escrito para um aplicativo de serviço, Olá criação CSR é genérico e também se aplicam para serviços de nuvem.

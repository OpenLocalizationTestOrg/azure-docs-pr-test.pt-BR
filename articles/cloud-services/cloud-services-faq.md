---
title: "funções de serviços de nuvem aaaAzure perguntas Frequentes | Microsoft Docs"
description: "Perguntas frequentes sobre os Serviços de Nuvem do Azure. Encontre respostas para algumas perguntas comuns sobre certificados, funções da Web e funções de trabalho."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Perguntas frequentes sobre Serviços de Nuvem
Este artigo responde a algumas perguntas frequentes sobre os Serviços de Nuvem do Microsoft Azure. Você também pode visitar Olá [perguntas frequentes sobre o Azure suporte](http://go.microsoft.com/fwlink/?LinkID=185083) para informações gerais de suporte e preços do Azure. Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

## <a name="certificates"></a>Certificados
### <a name="where-should-i-install-my-certificate"></a>Onde devo instalar o certificado?
* **Meu**  
  Certificado do aplicativo com a chave privada (\*. pfx, \*. p12).
* **AC**  
  Todos os certificados intermediários ficam neste repositório (política e Sub ACs).
* **RAIZ**  
  autoridade de certificação de raiz de saudação armazenar, para que seu certificado de autoridade de certificação raiz principal deve ser inserido aqui.

### <a name="i-cant-remove-expired-certificate"></a>Não é possível remover o certificado expirado
Azure impede a remoção de um certificado enquanto ele está em uso. Você precisará tooeither Olá a implantação de exclusão que usa o certificado de saudação ou implantação de atualização de saudação com um certificado diferente ou renovada.

### <a name="delete-an-expired-certificate"></a>Excluir um certificado expirado
Como Olá certificado não estiver em uso, você pode usar o hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) tooremove de cmdlet do PowerShell um certificado.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Tenho certificados expirados denominados Gerenciamento de Serviço do Microsoft Azure para Extensões
Esses certificados são criados sempre que uma extensão é adicionada toohello serviço em nuvem como Olá extensão da área de trabalho remota. Esses certificados são usados apenas para criptografar e descriptografar a configuração privada Olá da extensão de saudação. Não importa se esses certificados expiram. Data de expiração de saudação não é verificada.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Certificados que excluí continuam reaparecendo
Eles continuam reaparecendo muito provavelmente devido a uma ferramenta que você está usando, como o Visual Studio. Sempre que você se reconectar com uma ferramenta que está usando um certificado, ele será novamente tooAzure carregado.

### <a name="my-certificates-keep-disappearing"></a>Meus certificados continuam desaparecendo
Quando a instância de máquina virtual de saudação for reciclado, todas as alterações locais serão perdidas. Use um [tarefa de inicialização](cloud-services-startup-tasks.md) tooinstall certificados toohello virtual machine cada vez Olá função for iniciada.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Não consigo localizar meu certificados de gerenciamento no portal de saudação
[Certificados de gerenciamento](../azure-api-management-certs.md) só estão disponíveis em Olá Portal clássico do Azure. portal do Azure atual de saudação não usa certificados de gerenciamento. 

### <a name="how-can-i-disable-a-management-certificate"></a>Como desabilitar um certificado de gerenciamento?
[certificados de gerenciamento](../azure-api-management-certs.md) não podem ser desabilitados. Você excluí-los por meio de saudação Portal clássico do Azure quando você não deseja toobe mais usado.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Como criar um certificado SSL para um endereço IP específico?
Siga as instruções de Olá Olá [criar um tutorial do certificado](cloud-services-certs-create.md). Use o endereço IP de saudação como Olá nome DNS.

## <a name="security"></a>Segurança
### <a name="disable-ssl-30"></a>Desabilitar SSL 3.0
toodisable SSL 3.0 e TLS de usar segurança, crie uma tarefa de inicialização que está documentada nesta postagem de blog: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Adicionar **nosniff** tooyour site
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

### <a name="customize-iis-for-a-web-role"></a>Personalizar o IIS para uma função web
Usar script de inicialização IIS Olá da saudação [tarefas comuns de inicialização](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artigo.

## <a name="scaling"></a>Dimensionamento
### <a name="i-cannot-scale-beyond-x-instances"></a>Não consigo dimensionar além de X instâncias
Sua assinatura do Azure tem um limite no número de saudação de núcleos que você pode usar. Dimensionamento não funcionará se você tiver usado todos os núcleos Olá disponíveis. Por exemplo, se você tiver um limite de 100 núcleos, isso significa você poderia ter 100 instâncias de máquina virtual A1 dimensionadas para seu serviço de nuvem ou 50 instâncias de máquina virtual A2.

## <a name="networking"></a>Rede
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Eu não consigo reservar um IP em um serviço de nuvem de vários VIPs
Primeiro, verifique se essa instância de máquina virtual Olá que você está tentando tooreserve Olá IP para está ativada. Em segundo lugar, certifique-se de que você está usando IPs reservados para implantações de preparo e produção de hello incômodo. **Não** alterar configurações de saudação enquanto implantação hello está sendo atualizado.

## <a name="remote-desktop"></a>Área de trabalho remota
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Como acesso a área de trabalho remota quando tenho um NSG?
Adicionar regras toohello NSG que permitam o tráfego em portas **3389** e **20000**.  A Área de Trabalho Remota usa a porta **3389**.  Instâncias de serviço de nuvem têm a carga balanceada, portanto diretamente, você não pode controlar quais tooconnect de instância para.  Olá *RemoteForwarder* e *RemoteAccess* agentes gerenciar o tráfego RDP e permitir Olá cliente toosend um cookie RDP e especifique um tooconnect instância individual para.  Olá *RemoteForwarder* e *RemoteAccess* agentes exigem essa porta **20000*** aberto, que pode ser bloqueado se você tiver um NSG.

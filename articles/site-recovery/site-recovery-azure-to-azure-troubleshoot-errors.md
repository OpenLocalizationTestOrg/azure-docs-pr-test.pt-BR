---
title: "aaaAzure Solucionando problemas de recuperação de Site para erros e problemas de replicação do Azure para o Azure | Microsoft Docs"
description: "Solucionando problemas de erros e problemas durante a replicação de máquinas virtuais do Azure para recuperação de desastres"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Solucionar problemas de replicação de VM do Azure para o Azure

Este artigo descreve os problemas comuns no Azure Site Recovery Quando a replicação e a recuperação de máquinas virtuais do Azure da região de tooanother de uma região hello e explica como tootroubleshoot-los. Para obter mais informações sobre configurações com suporte, consulte Olá [matriz de suporte para replicar máquinas virtuais do Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problemas de cota de recursos do Azure (código de erro 150097)
Sua assinatura deve ser habilitado toocreate VMs do Azure na região de destino Olá que você planeje toouse como a região de recuperação de desastres. Além disso, sua assinatura deve ter suficiente cota habilitada toocreate VMs de tamanho específico. Por padrão, as escolhas de recuperação de Site Olá mesmo tamanho de destino Olá VM como Olá VM de origem. Se o tamanho de saudação correspondente não estiver disponível, o tamanho mais próximo de possíveis Olá é escolhido automaticamente. Se não houver nenhum tamanho correspondente que dá suporte à configuração de VM de origem, essa mensagem de erro será exibida:

**Código de erro** | **Possíveis causas:** | **Recomendações**
--- | --- | ---
150097<br></br>**Mensagem**: não foi possível habilitar a replicação de máquina virtual de saudação VmName. | -A assinatura que ID não pode ser habilitada toocreate todas as máquinas virtuais no local de região de destino hello.</br></br>-Sua ID de assinatura não pode ser habilitada ou não tem suficientes cota toocreate específicos tamanhos de VM no local de região de destino hello.</br></br>-Um tamanho VM de destino adequado que corresponda a origem de saudação contagem NIC de VM (2) não foi encontrado para a ID de assinatura de saudação no local de região de destino hello.| Entre em contato com [suporte de cobrança do Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable criação de VM para Olá necessário tamanhos de VM no local de destino Olá para sua assinatura. Depois que ele é habilitado, a repetição Olá Falha na operação.

### <a name="fix-hello-problem"></a>Corrija o problema de saudação
Você pode contatar [suporte de cobrança do Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable toocreate sua assinatura VMs de tamanhos necessários no local de destino hello.

Se o local de destino Olá tem uma restrição de capacidade, desabilite a replicação e habilitá-lo tooa outro local onde sua assinatura tem suficiente cota toocreate VMs de tamanhos de saudação necessário.

## <a name="trusted-root-certificates-error-code-151066"></a>Certificados de raiz confiável (código de erro 151066)

Se todos os certificados raiz confiáveis hello mais recentes não estão presentes na Olá VM, o trabalho "habilitar replicação" pode falhar. Sem certificados hello, Olá autenticação e autorização de serviço de recuperação de Site falha nas chamadas de saudação VM. mensagem de saudação do erro para o trabalho de recuperação de Site "habilitar replicação" hello falhado será exibida:

**Código de erro** | **Possível causa** | **Recomendações**
--- | --- | ---
151066<br></br>**Mensagem**: Falha na configuração do Site Recovery. | Olá necessários certificados de raiz confiável usados para autorização e autenticação não estão presentes no computador de saudação. | -Para uma VM executando o sistema de operacional do Windows hello, certifique-se de que Olá confiáveis de certificados raiz estão presentes no computador de saudação. Para obter informações, consulte [Configurar raízes confiáveis e certificados não permitidos](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Para uma VM executando o sistema de operacional Linux hello, siga as orientações de saudação para certificados raiz confiáveis publicado pelo distribuidor de versão de sistema operacional Olá Linux.

### <a name="fix-hello-problem"></a>Corrija o problema de saudação
**Windows**

Instale todas as atualizações do Windows mais recentes Olá em Olá VM para que todos os certificados de raiz confiável do hello estão presentes no computador de saudação. Se você estiver em um ambiente desconectado, siga o saudação padrão processo do Windows update em certificados organização tooget hello. Se Olá necessários certificados não estão presentes na Olá VM, Olá chamadas toohello serviço de recuperação de Site falhar por razões de segurança.

Siga Olá gerenciamento típico do Windows update ou o processo de gerenciamento de atualização de certificado em seu tooget organização listam todos os certificados de raiz mais recentes hello e revogação de certificado Olá atualizado Olá VMs.

tooverify que Olá problema for resolvido, vá toologin.microsoftonline.com em um navegador em sua VM.

**Linux**

Siga Olá orientações fornecidas pelo seu Linux distribuidor tooget hello mais recentes certificados raiz confiáveis e hello mais recente lista de certificados revogados no hello VM.

Como o SuSE Linux usa links simbólicos toomaintain uma lista de certificados, siga estas etapas:

1.  Entre como um usuário raiz.

2.  Execute este comando:

      ``# cd /etc/ssl/certs``

3.  toosee se o certificado de autoridade de certificação de raiz Olá Symantec está presente ou não, execute este comando:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Se o arquivo hello não for encontrado, execute estes comandos:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  toocreate um symlink com b204d74a.0 -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, execute este comando:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Verifique toosee se esse comando tem Olá saída a seguir. Caso contrário, você tem toocreate um symlink:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Se symlink 653b494a.0 não estiver presente, use este comando toocreate um symlink:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Conectividade de saída para intervalos de IP ou URLs de recuperação de Site (código de erro 151037 ou 151072)

Para toowork de replicação de recuperação de Site, conectividade de saída toospecific intervalos de IP ou URLs é necessária da saudação VM. Se a VM estiver atrás de um firewall ou usa conectividade de grupo (NSG) regras toocontrol saída segurança de rede, talvez você veja uma das seguintes mensagens de erro:

**Códigos de erro** | **Possíveis causas:** | **Recomendações**
--- | --- | ---
151037<br></br>**Mensagem**: falha tooregister máquina virtual do Azure com o Site Recovery. | -Você está usando o acesso de saída do NSG toocontrol na Olá VM e Olá necessário IP intervalos não estão na lista de permissões para acesso de saída.</br></br>-Você está usando ferramentas de firewall de terceiros e Olá necessário URLs/intervalos IP não estão na lista de permissões.</br>| -Se você estiver usando a conectividade de rede de saída do firewall proxy toocontrol em Olá VM, certifique-se de que Olá URLs de pré-requisito ou intervalos IP de datacenter estão na lista de permissões. Para obter informações, consulte [orientação de proxy do firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Se você estiver usando a conectividade de rede de saída do NSG regras toocontrol em Olá VM, certifique-se de que os intervalos IP de datacenter pré-requisito Olá estão na lista de permissões. Para obter mais informações, veja [Grupo de Segurança de Rede](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Mensagem**: Falha na configuração do Site Recovery. | Conexão não pode ser estabelecida tooSite pontos de extremidade de serviço de recuperação. | -Se você estiver usando a conectividade de rede de saída do firewall proxy toocontrol em Olá VM, certifique-se de que Olá URLs de pré-requisito ou intervalos IP de datacenter estão na lista de permissões. Para obter informações, consulte [orientação de proxy do firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Se você estiver usando a conectividade de rede de saída do NSG regras toocontrol em Olá VM, certifique-se de que os intervalos IP de datacenter pré-requisito Olá estão na lista de permissões. Para obter mais informações, veja [Grupo de Segurança de Rede](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Corrija o problema de saudação
toowhitelist [Olá necessário URLs](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) ou hello [necessário intervalos IP](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), siga as etapas de Olá Olá [documento de diretrizes de rede](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Disco não encontrado na máquina de saudação (código de erro 150039)

Um novo disco anexado toohello que VM deve ser inicializada.

**Código de erro** | **Possíveis causas:** | **Recomendações**
--- | --- | ---
150039<br></br>**Mensagem**: (DiskName) (DiskURI) de disco de dados do Azure com número de unidade lógica (LUN) (LUNValue) não foi mapeada tooa disco correspondente que está sendo informado no hello VM que tenha Olá mesmo valor LUN. | -Um novo disco de dados foi anexado toohello VM, mas ele não foi inicializado.</br></br>-disco de dados hello dentro Olá VM não está relatando valor LUN Olá em qual Olá disco foi anexado toohello VM corretamente.| Certifique-se de que os discos de dados Olá são inicializados e, em seguida, repita a operação de saudação.</br></br>Para Windows: [Anexar e inicializar um novo disco](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Para Linux: [Inicializar um novo disco de dados no Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Corrija o problema de saudação
Certifique-se de que os discos de dados Olá foram inicializados e, em seguida, repita a operação de saudação:

- Para Windows: [Anexar e inicializar um novo disco](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Para Linux: [Inicializar um novo disco de dados no Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Se Olá problema persistir, contate o suporte.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Olá toosee não é possível VM do Azure para seleção "habilitar a replicação"

Talvez você não veja sua VM do Azure para seleção na [habilitar a replicação: etapa 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Esse problema pode ser devido a configuração de recuperação de Site toostale à esquerda na Olá VM do Azure. configuração obsoleta Olá pode ser deixada em uma VM do Azure no hello casos a seguir:

- A replicação habilitada para Olá VM do Azure usando a recuperação de Site e excluídas Cofre de recuperação de Site Olá sem explicitamente a desabilitação da replicação em Olá VM.
- Replicação habilitada para Olá VM do Azure usando a recuperação de Site e, em seguida, excluiu o grupo de recursos de saudação contendo o Cofre de recuperação de Site Olá sem explicitamente a desabilitação da replicação em Olá VM.

### <a name="fix-hello-problem"></a>Corrija o problema de saudação

Você pode usar [remover o script de configuração de ASR obsoleto](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) e remover a configuração de recuperação de Site obsoleta Olá em Olá VM do Azure. Você deve ver Olá VM em [habilitar a replicação: etapa 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) depois de remover a configuração obsoleta hello.


## <a name="next-steps"></a>Próximas etapas
[Replicar as máquinas virtuais do Azure](site-recovery-replicate-azure-to-azure.md)

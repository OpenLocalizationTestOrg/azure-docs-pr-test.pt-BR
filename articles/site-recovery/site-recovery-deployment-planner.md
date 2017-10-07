---
title: "Planejador de implantação de recuperação de Site aaaAzure de VMware para o Azure | Microsoft Docs"
description: "Este é o guia de usuário do hello Azure Site Recovery implantação planejador."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/28/2017
ms.author: nisoneji
ms.openlocfilehash: a8c13cd47850575769e0186528807bc525bdeec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-deployment-planner"></a>Planejador de implantação do Azure Site Recovery
Este artigo é o guia do usuário do Planejador de implantação do Azure Site Recovery Olá VMware para o Azure para implantações de produção.

## <a name="overview"></a>Visão geral

Antes de começar a proteger quaisquer máquinas virtuais do VMware (VMs) usando o Site Recovery, alocar largura de banda suficiente, com base em sua taxa de alteração de dados diariamente, toomeet seu objetivo de ponto de recuperação desejado (RPO). Ser toodeploy se Olá certo número de servidores de configuração e servidores de processo no local.

Você também precisa tipo certo de saudação toocreate e o número de contas de armazenamento do Azure de destino. Você cria contas de armazenamento standard ou premium, acrescentando o crescimento nos servidores de produção de origem devido ao aumento no uso ao longo do tempo. Escolher tipo de armazenamento Olá por VM, com base em características de carga de trabalho (por exemplo, operações de e/s de leitura/gravação por segundo [IOPS] ou rotatividade de dados) e limites de recuperação de Site.

visualização pública do planejador Olá recuperação de Site implantação é uma ferramenta de linha de comando que está disponível somente para o cenário de VMware para o Azure hello. Remotamente, você pode criar o perfil de suas VMs VMware usando essa ferramenta (sem nenhum impacto de produção natureza) toounderstand Olá da largura de banda e os requisitos de armazenamento do Azure para replicação com êxito e failover de teste. Você pode executar a ferramenta de saudação sem instalar qualquer Site Recovery componentes no local. No entanto, tooget precisa obtida resultados de taxa de transferência, recomendamos que você execute o Planejador de saudação em um servidor Windows que atenda Olá requisitos mínimos Olá recuperação de Site do servidor de configuração que você precisaria eventualmente toodeploy como uma das primeiras etapas de saudação na implantação de produção.

ferramenta de saudação fornece Olá detalhes a seguir:

**Avaliação de compatibilidade**

* Avaliação de qualificação de uma VM com base no número de discos, no tamanho do disco, no IOPS, variação e tipo de inicialização (EFI/BIOS)
* Olá estimado de largura de banda necessária para a replicação delta

**Largura de banda de rede necessária versus avaliação de RPO**

* Olá estimado de largura de banda necessária para a replicação delta
* taxa de transferência de saudação recuperação de Site pode obter de tooAzure local
* número de saudação de VMs toobatch, com base em Olá estimado toocomplete a replicação inicial da largura de banda em uma determinada quantidade de tempo

**Requisitos de infraestrutura do Azure**

* requisito de tipo (conta de armazenamento padrão ou premium) de armazenamento Olá para cada VM
* número total de saudação do toobe de contas de armazenamento standard e premium configurado para replicação
* Sugestões de nomes de contas de armazenamento com base na orientação do Armazenamento do Azure
* posicionamento de conta de armazenamento Olá para todas as máquinas virtuais
* configurar vários Olá toobe núcleos do Azure antes de failover de teste ou failover na assinatura Olá
* Olá tamanho recomendado de VM do Azure para cada VM local

**Requisitos de infraestrutura local**
* Olá o número de servidores de configuração necessários e toobe de servidores de processo implantado no local

>[!IMPORTANT]
>
>Como uso é provavelmente tooincrease ao longo do tempo, todos os Olá anterior ferramenta cálculos são realizados supondo um fator de crescimento de 30 por cento de características de carga de trabalho e usando um valor 95º percentil Olá todas as métricas de criação de perfil (variação de IOPS, leitura/gravação e isso assim por diante). Esses dois elementos (fator de crescimento e cálculo de percentil) são configuráveis. toolearn mais sobre o fator de crescimento, consulte a seção de "Considerações sobre o fator de crescimento" hello. toolearn mais sobre o valor percentual, consulte a seção de "Valor percentual usado para cálculo hello" Olá.
>

## <a name="requirements"></a>Requisitos
ferramenta de saudação tem duas fases principais: criação de perfil e geração de relatórios. Há também uma terceira opção toocalculate taxa de transferência somente. requisitos de saudação para o servidor de saudação do qual Olá medida de taxa de transferência e de criação de perfil é iniciada são apresentados em Olá a tabela a seguir:

| Requisito de servidor | Descrição|
|---|---|
|Medida de taxa de transferência e criação de perfil| <ul><li>Sistema operacional: Microsoft Windows Server 2012 R2<br>(pelo menos idealmente correspondência Olá [tamanho recomendações para o servidor de configuração de saudação](https://aka.ms/asr-v2a-on-prem-components))</li><li>Configuração de máquina: 8 vCPUs, 16 GB de RAM, 300 GB de disco rígido</li><li>[Microsoft .NET Framework 4.5](https://aka.ms/dotnet-framework-45)</li><li>[VMware vSphere PowerCLI 6.0 R3](https://aka.ms/download_powercli)</li><li>[Microsoft Visual C++ redistribuível para Visual Studio 2012](https://aka.ms/vcplusplus-redistributable)</li><li>TooAzure de acesso de Internet deste servidor</li><li>Conta de Armazenamento do Azure</li><li>Acesso de administrador no servidor de saudação</li><li>Mínimo de 100 GB de espaço livre em disco (supondo que haja 1000 VMs com uma média de três discos em cada, com criação de perfil por 30 dias)</li><li>Configurações de nível de estatísticas do VMware vCenter devem ser definidas too2 ou alto nível</li><li>Permitir que a porta 443: ASR Planejador de implantação usa este host de servidor/ESXi porta tooconnect toovCenter</ul></ul>|
| Geração de relatórios | Um PC Windows ou Windows Server com o Microsoft Excel 2013 ou posterior |
| Permissões de usuário | Permissão somente leitura Olá conta de usuário que tenha usado o host de ESXi tooaccess Olá VMware vCenter server/VMware vSphere durante a criação de perfil |

> [!NOTE]
>
>ferramenta de saudação perfil somente máquinas virtuais com discos VMDK e o RDM. Ela não pode criar o perfil de VMs com discos iSCSI ou NFS. Recuperação de site oferece suporte a iSCSI e discos NFS para servidores do VMware, mas, como Planejador de implantação de saudação não está dentro de convidado hello e perfis de usando contadores de desempenho do vCenter, Olá ferramenta não tem visibilidade esses tipos de disco.
>

## <a name="download-and-extract-hello-public-preview"></a>Baixe e extraia a visualização pública Olá
1. Baixar a versão mais recente Olá de saudação [visualização pública do Site Recovery implantação Planejador](https://aka.ms/asr-deployment-planner).  
ferramenta de saudação é empacotada em uma pasta de arquivos. zip. versão atual de saudação da ferramenta de saudação suporta apenas o cenário de VMware para o Azure hello.

2. Copie hello. ZIP pasta toohello do Windows server do qual você deseja toorun ferramenta de saudação.  
Você pode executar a ferramenta saudação do Windows Server 2012 R2 se o servidor de saudação tiver acesso tooconnect toohello vCenter server/vSphere ESXi host de rede que contém a saudação VMs toobe atribuído. No entanto, recomendamos que você execute a ferramenta de saudação em um servidor cuja configuração de hardware atende Olá [diretriz de dimensionamento do servidor de configuração](https://aka.ms/asr-v2a-on-prem-components). Se você já tiver implantado os componentes de recuperação de Site no local, execute a ferramenta de saudação do servidor de configuração de saudação.

 Recomendamos que você tenha Olá mesma configuração de hardware de servidor de configuração de saudação (que tem um servidor de processo interno) no servidor de saudação onde você executa a ferramenta de saudação. Essa configuração garante que throughput Olá obtida que Olá ferramenta relatórios correspondências Olá real throughput que recuperação de Site podem obter durante a replicação. cálculo de taxa de transferência Olá depende da largura de banda disponível no servidor de saudação e configuração de hardware (CPU, armazenamento e assim por diante) do servidor de saudação. Se você executar a ferramenta de saudação de qualquer outro servidor, taxa de transferência de saudação é calculada a partir desse tooMicrosoft do servidor do Azure. Além disso, porque a configuração de hardware de saudação do servidor de saudação pode diferir da que saudação do servidor de configuração, taxa de transferência Olá obtida que Olá ferramenta relatórios talvez não sejam precisas.

3. Extraia a pasta do hello. zip.  
pasta de saudação contém vários arquivos e subpastas. arquivo executável Olá é ASRDeploymentPlanner.exe na pasta pai de saudação.

    Exemplo:  
    Copiar tooE de arquivo. zip Olá: \ unidade e extraia-o.
   E:\ASR Deployment Planner-Preview_v1.2.zip

    E:\ASR Deployment Planner-Preview_v1.2\ ASR Deployment Planner-Preview_v1.2\ ASRDeploymentPlanner.exe

## <a name="capabilities"></a>Funcionalidades
Você pode executar a ferramenta de linha de comando hello (ASRDeploymentPlanner.exe) em qualquer um dos Olá três modos a seguir:

1. Criação de perfil  
2. Geração de relatórios
3. Obter taxa de transferência

Primeiro, execute a ferramenta de saudação na criação de perfil de rotatividade de dados do modo toogather VM e IOPS. Em seguida, execute relatório de Olá Olá ferramenta toogenerate requisitos de armazenamento e largura de banda de rede de saudação do toofind.

## <a name="profiling"></a>Criação de perfil
No modo de criação de perfil, ferramenta de planejamento de implantação Olá conecta toohello vCenter server/vSphere ESXi host toocollect dados de desempenho Olá VM.

* Criação de perfil não afeta o desempenho de saudação de produção de hello VMs, porque nenhuma conexão direta é feita toothem. Todos os dados de desempenho são coletados de saudação vCenter server/ESXi host vSphere.
* tooensure que há um impacto irrelevante no servidor de saudação devido a criação de perfil, Olá ferramenta consultas Olá vCenter server/ESXi host vSphere uma vez a cada 15 minutos. Esse intervalo de consulta não comprometer a precisão de criação de perfil, como ferramenta Olá armazena dados de contador de desempenho de cada minuto.

### <a name="create-a-list-of-vms-tooprofile"></a>Criar uma lista de VMs tooprofile
Primeiro, você precisa de uma lista de saudação VMs toobe atribuído. Você pode obter todos os nomes de saudação de VMs em um host de ESXi do vCenter server/vSphere usando comandos do hello VMware vSphere PowerCLI em Olá procedimento a seguir. Como alternativa, você pode listar em um arquivo hello amigável os nomes ou endereços IP de Olá VMs que você deseja tooprofile manualmente.

1. Entrar toohello VM que VMware vSphere PowerCLI é instalado em.
2. Abra o console de PowerCLI Olá VMware vSphere.
3. Certifique-se de que a política de execução hello está habilitada para script hello. Se ele estiver desabilitado, inicie Olá VMware vSphere PowerCLI console no modo de administrador e, em seguida, habilite-o executando o comando a seguir de saudação:

            Set-ExecutionPolicy –ExecutionPolicy AllSigned

4. Você pode só necessidade toorun Olá comando a seguir se conectar VIServer não é reconhecido como nome de saudação do cmdlet.
 
            Add-PSSnapin VMware.VimAutomation.Core 

5. tooget todos os nomes de saudação de VMs em um servidor de vCenter/ESXi vSphere hospedam e armazenam a lista de saudação em um arquivo. txt, dois comandos de execução Olá listados aqui.
Substitua &lsaquo;nome do servidor&rsaquo;, &lsaquo;nome de usuário&rsaquo;, &lsaquo;senha&rsaquo; e &lsaquo;outputfile.txt&rsaquo;; por suas entradas.

            Connect-VIServer -Server <server name> -User <user name> -Password <password>

            Get-VM |  Select Name | Sort-Object -Property Name >  <outputfile.txt>

6. Abra o arquivo de saída de hello no bloco de notas e copie os nomes de todas as VMs que você deseja tooprofile tooanother arquivo (por exemplo, ProfileVMList.txt), um nome VM por linha hello. Esse arquivo é usado como entrada toohello *- VMListFile* parâmetro da ferramenta de linha de comando hello.

    ![Lista de nomes VM no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/profile-vm-list.png)

### <a name="start-profiling"></a>Iniciar criação de perfil
Depois de ter lista de saudação de VMs toobe criado o perfil, você pode executar a ferramenta de saudação em modo de criação de perfil. Aqui está a lista de saudação parâmetros obrigatórios e opcionais do hello ferramenta toorun no modo de criação de perfil.

ASRDeploymentPlanner.exe -Operation StartProfiling /?

| Nome do parâmetro | Descrição |
|---|---|
| -Operation | StartProfiling |
| -Server | nome de domínio totalmente qualificado de saudação ou endereço IP do host de ESXi Olá vCenter server/vSphere cujas VMs são toobe atribuído.|
| -User | Olá usuário nome tooconnect toohello vCenter server/ESXi host vSphere. usuário de saudação precisa as acesso toohave somente leitura, no mínimo.|
| -VMListFile | arquivo de Olá que contém a lista de saudação de VMs toobe atribuído. caminho do arquivo Hello pode ser absoluta ou relativa. arquivo de saudação deve conter um endereço IP/nome VM por linha. Nome da máquina virtual especificado no arquivo hello deve ser Olá igual ao nome VM Olá no host de ESXi Olá vCenter server/vSphere.<br>Por exemplo, o arquivo hello VMList.txt contém Olá máquinas virtuais a seguir:<ul><li>máquina_virtual_A</li><li>10.150.29.110</li><li>máquina_virtual_B</li><ul> |
| -NoOfDaysToProfile | Olá número de dias nos quais perfis estará toobe execute. É recomendável que você execute a criação de perfil para mais de 15 dias tooensure que Olá padrão de carga de trabalho em seu ambiente por Olá especificado período é observado e usado tooprovide uma recomendação precisa. |
| -Directory | Saudação (opcional) convenção universal de nomenclatura (UNC) ou toostore de caminho do diretório local gerados durante a criação de perfil de dados de criação de perfil. Se não for fornecido um nome de diretório, diretório de saudação chamado 'ProfiledData' no caminho atual Olá será usado como diretório de padrão de saudação. |
| -Password | Saudação (opcional) senha toouse tooconnect toohello vCenter server/ESXi host vSphere. Se você não especificar um agora, você será solicitado para ele quando Olá comando é executado.|
| -StorageAccountName | Nome da conta de armazenamento hello (opcional) que é a taxa de transferência de saudação do toofind usado viável para replicação de dados de tooAzure no local. Olá ferramenta carregamentos teste toothis armazenamento conta toocalculate transferência de dados.|
| -StorageAccountKey | Chave de conta de armazenamento hello (opcional) que tenha usado a conta de armazenamento tooaccess hello. Vá toohello portal do Azure > contas de armazenamento ><*nome da conta de armazenamento*>> Configurações > chaves de acesso > Key1 (ou chave de acesso primária para a conta de armazenamento clássico). |
| -Ambiente | (opcional) Este é o seu ambiente de conta do Armazenamento do Azure de destino. Isso pode ser um dos três valores: AzureCloud, AzureUSGovernment ou AzureChinaCloud. O padrão é AzureCloud. Use o parâmetro de saudação quando o destino da região do Azure é nuvens Azure US Government ou do Azure na China. |


É recomendável que você analisar suas VMs para pelo menos 15 dias de too30. Durante a saudação período de criação de perfil, ASRDeploymentPlanner.exe continua em execução. ferramenta Olá leva a entrada de tempo de criação de perfil em dias. Se você quiser tooprofile por algumas horas ou minutos para um teste rápido da ferramenta, a saudação em visualização pública Olá, será necessário tempo de saudação tooconvert em medidas equivalente de saudação de dias. Por exemplo, tooprofile por 30 minutos, Olá entrada deve ser 30/(60*24) = 0.021 dias. Olá mínimo permitido de tempo de criação de perfil é de 30 minutos.

Durante a criação de perfil, você poderá opcionalmente passar um nome de conta de armazenamento e a taxa de transferência de saudação de chave toofind que recuperação de Site pode obter em tempo de saudação de replicação do servidor de configuração de saudação ou tooAzure de servidor de processo. Se a chave e o nome de conta de armazenamento de saudação não são passadas durante a criação de perfil, ferramenta de saudação não calcular a taxa de transferência possível.

Você pode executar várias instâncias da ferramenta Olá para vários conjuntos de VMs. Certifique-se de que os nomes de VM Olá não sejam repetidos em qualquer um dos conjuntos de criação de perfil de saudação. Por exemplo, se você tiver criado o perfil de dez VMs (VM1 por meio de VM10) e depois de alguns dias você deseja tooprofile outro cinco VMs (VM11 por meio de VM15), você pode executar a ferramenta de saudação do outro console de linha de comando para o segundo conjunto de VMs de saudação (VM11 por meio de VM15). Certifique-se de que segundo conjunto Olá de VMs não tem quaisquer nomes VM da primeira instância de criação de perfil de saudação ou usar um diretório de saída diferente de saudação segundo executar. Se duas instâncias da ferramenta hello são usadas para criação de perfil hello mesmo VMs e use Olá mesmo diretório de saída, relatório Olá gerado estarão incorreto.

Configurações de VM são capturadas uma vez no início de saudação do hello operação de criação de perfil e armazenadas em um arquivo chamado VMDetailList.xml. Essas informações são usadas quando Olá relatório é gerado. Qualquer alteração na configuração da VM (por exemplo, um número maior de núcleos, discos ou NICs) de saudação início toohello final da criação de perfil não é capturada. Se uma configuração de VM com perfil foi alterada durante saudação de criação de perfil, em visualização pública do Olá, aqui é detalhes VM mais recentes do hello solução alternativa tooget ao gerar o relatório de saudação:

* Fazer backup VMdetailList.xml e excluir o arquivo de saudação do seu local atual.
* Passe - usuário e - Password argumentos em tempo de saudação de geração de relatórios.

saudação de comando de criação de perfil gera vários arquivos no hello diretório de criação de perfil. Não exclua nenhum dos arquivos hello, porque fazer assim afeta a geração de relatórios.

#### <a name="example-1-profile-vms-for-30-days-and-find-hello-throughput-from-on-premises-tooazure"></a>Exemplo 1: Perfil VMs para 30 dias e localizar taxa de transferência de saudação do local tooAzure
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  30  -User vCenterUser1 -StorageAccountName  asrspfarm1 -StorageAccountKey Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

#### <a name="example-2-profile-vms-for-15-days"></a>Exemplo 2: criar o perfil de VMs por 15 dias

```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  15  -User vCenterUser1
```

#### <a name="example-3-profile-vms-for-1-hour-for-a-quick-test-of-hello-tool"></a>Exemplo 3: Perfil VMs por 1 hora para um teste rápido da ferramenta Olá
```
ASRDeploymentPlanner.exe -Operation StartProfiling -Directory “E:\vCenter1_ProfiledData” -Server vCenter1.contoso.com -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -NoOfDaysToProfile  0.04  -User vCenterUser1
```

>[!NOTE]
>
>* Se servidor de saudação ferramenta Olá estiver em execução no é reinicializada ou falhou, Olá ou se você fechar a ferramenta usando Ctrl + C, dados saudação atribuído é preservado. No entanto, há uma chance de saudação ausente últimos 15 minutos de dados analisados. Na instância, execute novamente a ferramenta Olá no modo de criação de perfil após a reinicialização do servidor de saudação.
>* Quando Olá nome de conta de armazenamento e a chave são passadas, taxa de transferência do hello ferramenta medidas Olá na última etapa Olá de criação de perfil. Se a ferramenta de saudação é fechada antes da conclusão da criação de perfil, taxa de transferência de saudação não é calculada. Olá a taxa de transferência toofind Olá antes da geração de relatório, é possível executar a operação de GetThroughput de saudação do console de linha de comando hello. Caso contrário, o relatório de Olá gerado não conterá informações de taxa de transferência de saudação.


## <a name="generate-a-report"></a>Gerar um relatório
ferramenta de Hello gera um habilitado para macros do Microsoft Excel (arquivo XLSM) como saída de relatório hello, que resume todas as recomendações de implantação de saudação. relatório de saudação é denominado DeploymentPlannerReport_ <*identificador numérico exclusivo*>. xlsm e colocada no hello especificou o diretório.

Após a criação de perfil estiver concluída, você pode executar a ferramenta de saudação no modo de geração de relatórios. Olá, a tabela a seguir contém uma lista de toorun de parâmetros obrigatórios e opcionais ferramenta no modo de geração de relatórios.

`ASRDeploymentPlanner.exe -Operation GenerateReport /?`

|Nome do parâmetro | Descrição |
|-|-|
| -Operation | GenerateReport |
| -Server |  Olá vCenter/vSphere totalmente qualificado do servidor nome de domínio ou endereço IP (use Olá mesmo nome ou endereço IP que você usou em tempo de criação de perfil de saudação) onde Olá atribuído VMs cujo relatório é gerado de toobe estão localizados. Observe que, se você usou um servidor do vCenter ao tempo de saudação de criação de perfil, você não pode usar um servidor vSphere para geração de relatórios e vice-versa.|
| -VMListFile | arquivo Hello contém Olá lista de VMs com perfil que Olá relatório é toobe gerado para. caminho do arquivo Hello pode ser absoluta ou relativa. arquivo de saudação deve conter um nome VM ou o endereço IP por linha. nomes de VM Olá que são especificados no arquivo hello deve ser Olá mesmo que os nomes de VM Olá Olá vCenter server/ESXi host vSphere e correspondência que foi usado durante a criação de perfil.|
| -Directory | (Opcional) Olá UNC ou caminho do diretório local onde Olá atribuído (arquivos gerados durante a criação de perfil) de dados é armazenado. Esses dados são necessários para gerar o relatório de saudação. Se não for especificado um nome, será usado o diretório 'ProfiledData'. |
| -GoalToCompleteIR | Hello (opcional) o número de horas no qual Olá a replicação inicial da saudação atribuído VMs precisa toobe concluída. relatório de saudação gerado fornece Olá número de VMs para os quais a replicação inicial pode ser concluída em Olá especificado tempo. padrão de saudação é 72 horas. |
| -User | Servidor da vCenter/vSphere do toohello de tooconnect da toouse do nome de usuário hello (opcional). nome de saudação é toofetch usado Olá últimas informações de configuração de saudação VMs, como o número de saudação de discos, o número de núcleos e o número de NICs, toouse no relatório de saudação. Se o nome de saudação não for fornecido, informações de configuração de saudação coletadas no início de saudação da saudação inicial de criação de perfil são usadas. |
| -Password | Saudação (opcional) senha toouse tooconnect toohello vCenter server/ESXi host vSphere. Se a senha de saudação não for especificada como um parâmetro, você deverá para ela mais tarde quando Olá comando é executado. |
| -DesiredRPO | Saudação (opcional) desejado ponto de recuperação objetivo, em minutos. padrão de saudação é de 15 minutos.|
| -Bandwidth | Largura de banda em Mbps. Olá parâmetro toouse toocalculate Olá RPO que pode ser obtido para Olá especificado da largura de banda. |
| -StartDate | Saudação (opcional) data e hora de início em MM-DD-YYYY:HH:MM (formato de 24 horas). *StartDate* deve ser especificado junto com *EndDate*. Quando StartDate for especificado, o relatório de Olá é gerado para dados Olá atribuído coletados entre StartDate e EndDate. |
| -EndDate | Data de término da saudação (opcional) e a hora em MM-DD-YYYY:HH:MM (formato de 24 horas). *EndDate* deve ser especificado junto com *StartDate*. Quando a data de término for especificada, o relatório de Olá é gerado para dados Olá atribuído coletados entre StartDate e EndDate. |
| -GrowthFactor | Fator de crescimento hello (opcional), expressado como uma porcentagem. padrão de saudação é 30 por cento. |
| -UseManagedDisks | (Opcional) UseManagedDisks - Sim/Não. O padrão é Sim. número de saudação de máquinas virtuais que podem ser colocados em uma única conta de armazenamento é calculado considerando se failover/teste de Failover de máquinas virtuais é feito em um disco gerenciado em vez de disk não gerenciado. |

#### <a name="example-1-generate-a-report-with-default-values-when-hello-profiled-data-is-on-hello-local-drive"></a>Exemplo 1: Gerar um relatório com valores padrão quando dados saudação perfil criado na unidade local Olá
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-2-generate-a-report-when-hello-profiled-data-is-on-a-remote-server"></a>Exemplo 2: Gerar um relatório quando dados saudação analisado em um servidor remoto
Você deve ter acesso de leitura/gravação no diretório remoto hello.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “\\PS1-W2K12R2\vCenter1_ProfiledData” -VMListFile “\\PS1-W2K12R2\vCenter1_ProfiledData\ProfileVMList1.txt”
```

#### <a name="example-3-generate-a-report-with-a-specific-bandwidth-and-goal-toocomplete-ir-within-specified-time"></a>Exemplo 3: Gerar um relatório com um específico da largura de banda e a meta toocomplete IR no tempo especificado
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -Bandwidth 100 -GoalToCompleteIR 24
```

#### <a name="example-4-generate-a-report-with-a-5-percent-growth-factor-instead-of-hello-default-30-percent"></a>Exemplo 4: Gerar um relatório com um fator de crescimento de 5 por cento, em vez da saudação padrão 30 por cento
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -GrowthFactor 5
```

#### <a name="example-5-generate-a-report-with-a-subset-of-profiled-data"></a>Exemplo 5: gerar um relatório com um subconjunto dos dados de criação de perfil
Por exemplo, você tem 30 dias de dados analisados e deseja toogenerate um relatório de apenas 20 dias.
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt” -StartDate  01-10-2017:12:30 -EndDate 01-19-2017:12:30
```

#### <a name="example-6-generate-a-report-for-5-minute-rpo"></a>Exemplo 6: gerar um relatório para o RPO de cinco minutos
```
ASRDeploymentPlanner.exe -Operation GenerateReport -Server vCenter1.contoso.com -Directory “E:\vCenter1_ProfiledData” -VMListFile “E:\vCenter1_ProfiledData\ProfileVMList1.txt”  -DesiredRPO 5
```

## <a name="percentile-value-used-for-hello-calculation"></a>Valor percentual usado para cálculo de saudação
**Qual é o valor de percentil padrão Olá de métricas de desempenho coletados durante faz Olá ferramenta uso de criação de perfil ao gerar um relatório?**

Olá ferramenta toohello 95º percentil os valores padrão de leitura/gravação IOPS, escreva IOPS e rotatividade de dados que são coletados durante a criação de perfil de todas as VMs de saudação. Essa métrica garante que pico de percentual de 100 vezes Olá poderá ver suas VMs devido a eventos temporários é usado não toodetermine seus requisitos de conta de armazenamento e largura de banda da fonte de destino. Por exemplo, um evento temporário pode ser um trabalho de backup executado uma vez por dia, uma indexação de um banco de dados periódica ou uma atividade de geração de relatórios de análise ou outros eventos pontuais semelhantes de curta duração.

Fornece que uma imagem real de características de carga de trabalho real e lhe usando valores de 95º percentil Olá melhor desempenho quando as cargas de trabalho Olá estão em execução no Azure. Não é nossa intenção que seria necessário toochange esse número. Se você alterar o valor de saudação (toohello 90º percentil, por exemplo), você pode atualizar o arquivo de configuração de saudação *ASRDeploymentPlanner.exe.config* em Olá pasta padrão e salvá-lo toogenerate um novo relatório Olá existente atribuído dados.
```
<add key="WriteIOPSPercentile" value="95" />      
<add key="ReadWriteIOPSPercentile" value="95" />      
<add key="DataChurnPercentile" value="95" />
```

## <a name="growth-factor-considerations"></a>Considerações sobre o fator de crescimento
**Por que deve considerar o fator de crescimento ao planejar implantações?**

É crítico tooaccount de crescimento em suas características de carga de trabalho, supondo que um potencial aumento no uso ao longo do tempo. Depois de proteção está em vigor, se alterar suas características de carga de trabalho, você não pode alternar tooa outra conta de armazenamento para a proteção sem desabilitando e reabilitando a proteção de saudação.

Por exemplo, digamos que hoje a VM esteja em uma conta de replicação de armazenamento standard. Sobre Olá próximos três meses, várias alterações são provavelmente toooccur:

* Olá número de usuários do aplicativo hello que é executado em Olá VM aumentará.
* variação de aumento resultante Olá em Olá VM exigirá armazenamento do hello VM toogo toopremium para que a replicação de recuperação de Site pode acompanhar o ritmo.
* Consequentemente, você terá toodisable e habilitar novamente a conta de armazenamento proteção tooa premium.

É altamente recomendável que você planeje durante o planejamento da implantação e enquanto o valor padrão de saudação é 30% de crescimento. São Olá especialista em seu aplicativo uso padrão e projeções de crescimento e você pode alterar esse número ao gerar um relatório. Além disso, você pode gerar vários relatórios com vários fatores de crescimento com hello mesmo criado o perfil de dados e determinar quais recomendações de largura de banda de armazenamento e a fonte de destino funcionam melhor para você.

relatório do Microsoft Excel Olá gerado contém Olá informações a seguir:

* [Input](site-recovery-deployment-planner.md#input)
* [Recomendações](site-recovery-deployment-planner.md#recommendations-with-desired-rpo-as-input)
* [Entrada de Recommendations-Bandwidth](site-recovery-deployment-planner.md#recommendations-with-available-bandwidth-as-input)
* [VM<->Posicionamento de Armazenamento](site-recovery-deployment-planner.md#vm-storage-placement)
* [VMs compatíveis](site-recovery-deployment-planner.md#compatible-vms)
* [VMs incompatíveis](site-recovery-deployment-planner.md#incompatible-vms)

![Planejador de implantação](./media/site-recovery-deployment-planner/dp-report.png)

## <a name="get-throughput"></a>Obter taxa de transferência

taxa de transferência de saudação de tooestimate que a recuperação de Site pode obter do local tooAzure durante a replicação, execute a ferramenta Olá no modo GetThroughput. ferramenta de saudação calcula a taxa de transferência de saudação do servidor de saudação que Olá ferramenta está em execução no. Idealmente, esse servidor baseia-se na guia dimensionamento do servidor de configuração de hello. Se você já tiver implantado o Site Recovery infraestrutura componentes no local, execute a ferramenta de saudação no servidor de configuração de saudação.

Abra um console de linha de comando e vá toohello pasta da ferramenta de planejamento de implantação de recuperação de Site. Execute ASRDeploymentPlanner.exe com os parâmetros a seguir.

`ASRDeploymentPlanner.exe -Operation GetThroughput /?`

|Nome do parâmetro | Descrição |
|-|-|
| -Operation | GetThroughput |
| -Directory | (Opcional) Olá UNC ou caminho do diretório local onde Olá atribuído (arquivos gerados durante a criação de perfil) de dados é armazenado. Esses dados são necessários para gerar o relatório de saudação. Se não for especificado um nome de diretório, será usado o diretório 'ProfiledData'. |
| -StorageAccountName | nome da conta de armazenamento Olá que tenha usado toofind Olá da largura de banda consumida para replicação de dados de tooAzure local. Olá ferramenta carregamentos teste dados toothis armazenamento conta toofind Olá largura de banda consumida. |
| -StorageAccountKey | chave de conta de armazenamento Olá que usou a conta de armazenamento tooaccess hello. Vá toohello portal do Azure > contas de armazenamento ><*nome da conta de armazenamento*>> Configurações > chaves de acesso > Key1 (ou uma chave de acesso primária para uma conta de armazenamento clássico). |
| -VMListFile | arquivo Hello que contém a lista de saudação de VMs toobe atribuído para calcular Olá da largura de banda consumida. caminho do arquivo Hello pode ser absoluta ou relativa. arquivo de saudação deve conter um endereço IP/nome VM por linha. nomes de VM Olá especificados no arquivo hello deve ser Olá mesmo que os nomes de VM Olá no host de ESXi Olá vCenter server/vSphere.<br>Por exemplo, o arquivo hello VMList.txt contém Olá máquinas virtuais a seguir:<ul><li>VM_A</li><li>10.150.29.110</li><li>VM_B</li></ul>|
| -Ambiente | (opcional) Este é o seu ambiente de conta do Armazenamento do Azure de destino. Isso pode ser um dos três valores: AzureCloud, AzureUSGovernment ou AzureChinaCloud. O padrão é AzureCloud. Use o parâmetro de saudação quando o destino da região do Azure é nuvens Azure US Government ou do Azure na China. |

ferramenta de saudação cria várias asrvhdfile de 64 MB. vhd <> # arquivos (onde "#" é o número de saudação de arquivos) no diretório especificado hello. ferramenta de saudação carrega Olá arquivos toohello armazenamento conta toofind Olá taxa de transferência. Depois de taxa de transferência de saudação é medida, o ferramenta Olá exclui todos os arquivos de Olá Olá da conta de armazenamento e de servidor de local de saudação. Se ferramenta Olá for encerrada por qualquer motivo, enquanto ele está calculando a taxa de transferência, arquivos de saudação não é excluído do armazenamento de saudação ou de servidor de local de saudação. Você terá que toodelete-los manualmente.

Olá taxa de transferência é medida em um momento específico no tempo e é a taxa de transferência máxima do hello que recuperação de Site podem obter durante a replicação, desde que todos os outros fatores permanecem Olá mesmo. Por exemplo, se qualquer aplicativo começa a consumir mais largura de banda na mesma rede, a taxa de transferência real Olá varia durante a replicação de saudação. Se você estiver executando o comando GetThroughput de saudação de um servidor de configuração, a ferramenta de hello está ciente de todas as VMs protegidas e replicação em andamento. Hello a resultados de taxa de transferência medido Olá é diferente se Olá GetThroughput operação é executada quando a saudação protegida VMs tiver dados alta rotatividade. É recomendável que você execute ferramenta Olá em vários pontos no tempo durante a criação de perfil toounderstand quais níveis podem ser obtidos em vários momentos de taxa de transferência. No relatório Olá, ferramenta Olá mostra Olá última medida taxa de transferência de.

### <a name="example"></a>Exemplo
```
ASRDeploymentPlanner.exe -Operation GetThroughput -Directory  E:\vCenter1_ProfiledData -VMListFile E:\vCenter1_ProfiledData\ProfileVMList1.txt  -StorageAccountName  asrspfarm1 -StorageAccountKey by8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

>[!NOTE]
>
> Execute a ferramenta de saudação em um servidor que tem Olá mesmo armazenamento e as características da CPU como servidor de configuração de saudação.
>
> Para replicação, defina Olá Olá recomendado de largura de banda toomeet RPO 100 por cento do tempo de saudação. Depois de definir saudação à direita da largura de banda, se você não vir um aumento na produtividade dos Olá obtida relatado pela ferramenta hello, Olá a seguir:
>
>  1. Verifique toodetermine se houver qualquer rede qualidade de serviço (QoS) que é limitar a taxa de transferência de recuperação de Site.
>
>  2. Verifique toodetermine se seu Cofre de recuperação de Site está em hello mais próximo com suporte fisicamente latência de rede do Microsoft Azure região toominimize.
>
>  3. Verifique seu toodetermine de características de armazenamento local se você pode melhorar o hardware da saudação (por exemplo, unidade de disco rígido tooSSD).
>
>  4. Alterar as configurações de recuperação de Site de Olá no servidor de processo Olá muito[aumentar Olá quantidade de largura de banda de rede usada para replicação](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

## <a name="recommendations-with-desired-rpo-as-input"></a>Recomendações com RPO desejado como entrada

### <a name="profiled-data"></a>Dados de criação de perfil

![modo de exibição de dados criado o perfil de saudação no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/profiled-data-period.png)

**Período de dados analisados**: período Olá durante o qual Olá de criação de perfil foi executada. Por padrão, ferramenta Olá inclui todos os dados analisados em cálculo Olá, a menos que ele gera o relatório de saudação para um período específico usando opções StartDate e EndDate durante a geração de relatório.

**Nome do servidor**: nome de saudação ou endereço IP do host de ESXi relatório cujo VMs é gerado ou Olá VMware vCenter.

**Desejado RPO**: objetivo de ponto de recuperação Olá para sua implantação. Por padrão, a saudação necessária largura de banda de rede é calculada para valores RPO de 15, 30 e 60 minutos. Com base na seleção de Olá, valores hello afetada são atualizados na folha de saudação. Se você tiver usado o hello *DesiredRPOinMin* parâmetro ao gerar relatório Olá, o valor mostrado no resultado de RPO desejado Olá.

### <a name="profiling-overview"></a>Visão geral da criação de perfil

![Resultados da criação de perfil no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/profiling-overview.png)

**Total de máquinas de virtuais atribuído**: Olá número total de máquinas virtuais cujos dados de perfil estão disponíveis. Se Olá VMListFile tem nomes de todas as máquinas virtuais que não foram analisados, essas VMs não são consideradas na geração de relatório hello e são excluídas dos Olá total analisada contagem de máquinas virtuais.

**Máquinas de virtuais compatíveis**: Olá número de máquinas virtuais que podem ser protegido tooAzure usando a recuperação de Site. É Olá o número total de VMs compatíveis para qual Olá largura de banda necessária, o número de contas de armazenamento, o número de núcleos do Azure e o número de servidores de configuração e servidores de processo adicional são calculados. detalhes de saudação de cada VM compatível estão disponíveis no hello "VMs compatível" seção.

**Máquinas de virtuais incompatíveis**: Olá número de VMs com perfil que são incompatíveis para proteção com a recuperação de Site. motivos Olá para incompatibilidade são indicados na hello "VMs incompatível" seção. Se Olá VMListFile tem nomes de todas as máquinas virtuais que não foram analisados, essas VMs serão excluídas da contagem de VMs incompatível hello. Essas VMs são listados como "Dados não encontrada" no final de saudação da seção hello "VMs incompatível".

**RPO Desejado**: seu objetivo de ponto de recuperação desejado, em minutos. relatório de saudação é gerado para três valores RPO: 15 (padrão), 30 e 60 minutos. recomendação de largura de banda Olá no relatório de saudação é alterada com base em sua seleção na lista de Olá RPO desejado lista suspensa na parte superior de saudação à direita da folha de saudação. Se você tiver gerado relatório hello usando Olá *- DesiredRPO* parâmetro com um valor personalizado, este valor personalizado será exibido como o padrão de saudação na lista de saudação suspensa RPO desejado.

### <a name="required-network-bandwidth-mbps"></a>Largura de banda necessária (Mbps)

![Largura de banda necessária no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/required-network-bandwidth.png)

**toomeet RPO 100 por cento do tempo de saudação:** Olá recomendado de largura de banda em Mbps toobe alocada toomeet o RPO desejado 100 por cento do tempo de saudação. Essa quantidade de largura de banda deve ser dedicada para a replicação de estado estacionário delta de todos os seu tooavoid VMs compatível quaisquer violações de RPO.

**toomeet RPO 90 por cento do tempo de saudação**: devido a banda larga de preços ou por qualquer outro motivo, se você não pode definir toomeet de largura de banda necessária Olá o RPO desejado 100 por cento do tempo de saudação, você pode escolher toogo com uma configuração de banda baixa pode atender às suas RPO 90 por cento do tempo de saudação desejado. implicações de saudação toounderstand de definir essa largura de banda inferior, Olá relatório fornece uma análise hipotética número hello e a duração do RPO violações tooexpect.

**Taxa de transferência obtida:** taxa de transferência de saudação do servidor de saudação no qual você executou região Olá GetThroughput comando toohello Microsoft Azure onde a conta de armazenamento hello está localizada. Esse número de taxa de transferência indica o nível de saudação estimada que você pode obter ao proteger Olá compatíveis VMs usando a recuperação de Site, desde que o servidor de configuração ou características de armazenamento e de rede do servidor de processo permanecem Olá mesmo que servidor de saudação do qual você executou a ferramenta de saudação.

Para replicação, você deve definir Olá Olá recomendado de largura de banda toomeet RPO 100 por cento do tempo de saudação. Depois que você definir a largura de banda Olá, se você não vir um aumento na taxa de transferência Olá obtida, conforme relatado pela ferramenta hello, faça Olá a seguir:

1. Verifique toosee se houver qualquer rede qualidade de serviço (QoS) que é limitar a taxa de transferência de recuperação de Site.

2. Verifique toosee se seu Cofre de recuperação de Site está em hello mais próximo com suporte fisicamente latência de rede do Microsoft Azure região toominimize.

3. Verifique seu toodetermine de características de armazenamento local se você pode melhorar o hardware da saudação (por exemplo, unidade de disco rígido tooSSD).

4. Alterar as configurações de recuperação de Site de Olá no servidor de processo Olá muito[aumentar Olá quantidade largura de banda usada para replicação](./site-recovery-plan-capacity-vmware.md#control-network-bandwidth).

Se você estiver executando a ferramenta de saudação em um servidor de configuração ou o servidor de processo que já tenha protegido VMs, execute a ferramenta de saudação algumas vezes. Olá obtida taxa de transferência número muda dependendo da quantidade de saudação de variação está sendo processada no momento.

Para todas as implantações do Site Recovery corporativo, é recomendável usar o [ExpressRoute](https://aka.ms/expressroute).

### <a name="required-storage-accounts"></a>Contas de armazenamento necessárias
Olá seguinte gráfico mostra a contas de número total de saudação de armazenamento (standard e premium) que são necessária tooprotect todos os Olá VMs compatíveis. toolearn qual armazenamento toouse de conta para cada VM, consulte a seção de "posicionamento de armazenamento de máquina virtual" de saudação.

![Contas de armazenamento necessária no planejador de implantação de saudação](./media/site-recovery-deployment-planner/required-azure-storage-accounts.png)

### <a name="required-number-of-azure-cores"></a>Número necessário de núcleos do Azure
Esse resultado é o número total de saudação de núcleos toobe configurar antes de failover de teste ou failover de todos os Olá VMs compatíveis. Se houver muito pequeno de núcleos na assinatura Olá, recuperação de Site falha toocreate VMs em tempo de saudação de failover ou failover de teste.

![Número necessário de núcleos do Azure no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/required-number-of-azure-cores.png)

### <a name="required-on-premises-infrastructure"></a>Infraestrutura local necessária
Esse valor é o número total de saudação de servidores de configuração e toobe de servidores de processo adicional configurado que seria suficiente tooprotect todos Olá VMs compatíveis. Dependendo da saudação suportada [tamanho recomendações para o servidor de configuração de saudação](https://aka.ms/asr-v2a-on-prem-components), ferramenta Olá pode recomendar servidores adicionais. Olá recomendação é baseada em Olá maior de variação do hello por dia ou número máximo de saudação de VMs protegidas (supondo que uma média de três discos por VM), o que for atingido primeiro no servidor de configuração de saudação ou Olá processo adicional. Você encontrará detalhes de saudação da variação total por dia e o número total de discos protegidos no hello "Entrada" seção.

![Infraestrutura local necessária no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/required-on-premises-infrastructure.png)

### <a name="what-if-analysis"></a>Teste de hipóteses
Essa análise descreve violações quantos podem ocorrer durante a saudação perfis período quando você define que uma largura de banda inferior para Olá desejado RPO toobe atendidos somente 90% do tempo de saudação. Uma ou mais violações de RPO podem ocorrer em qualquer dia. Olá gráfico mostra o horário de pico Olá RPO de dia de saudação.
Com base nesta análise, você pode decidir se o número de saudação de violações de RPO em todos os dias e RPO visitas por dia de pico é aceitável com hello especificado menos largura de banda. Se for aceitável, que você pode alocar largura de banda inferior Olá para replicação, ou alocar Olá maior largura de banda toomeet sugerido Olá 100 por cento do tempo de saudação RPO desejado.

![Análise e-se no planejamento de implantação de saudação](./media/site-recovery-deployment-planner/what-if-analysis.png)

### <a name="recommended-vm-batch-size-for-initial-replication"></a>Tamanho de lote de VMs recomendado para a replicação inicial
Nesta seção, é recomendável sugerido de número de saudação de máquinas virtuais que podem ser protegidos de replicação inicial do hello toocomplete paralelo dentro de 72 horas com hello toomeet de largura de banda desejado RPO 100 por cento do tempo de saudação que está sendo definido. Esse valor é configurável. toochange-lo em tempo de geração de relatórios, use Olá *GoalToCompleteIR* parâmetro.

Olá, aqui o gráfico mostra um intervalo de valores de largura de banda e uma calculado VM lote tamanho contagem toocomplete a replicação inicial de 72 horas, com base na média Olá detectado VM Olá de tamanho em todas as VMs compatíveis.

Em visualização pública do hello, relatório de saudação não especifica quais VMs devem ser incluídas em um lote. Você pode usar tamanho de disco Olá mostrado no hello "VMs compatível" seção toofind tamanho de cada VM e selecioná-las para um lote, ou você pode selecionar Olá VMs com base em características de carga de trabalho conhecidos. tempo de conclusão de saudação de alterações de replicação inicial de saudação proporcionalmente, com base no tamanho de disco VM real hello, usado espaço em disco e taxa de transferência de rede disponível.

![Tamanho de lote de VM recomendado](./media/site-recovery-deployment-planner/recommended-vm-batch-size.png)

### <a name="growth-factor-and-percentile-values-used"></a>Fator de crescimento e valores de percentil usados
Esta seção na parte inferior de saudação do hello mostra o valor de percentil de saudação usado para todos os contadores de desempenho de saudação de VMs Olá atribuído (o padrão é de 95 ° percentil) da folha e Olá fator de crescimento (o padrão é 30 por cento) que é usado em todos os cálculos de saudação.

![Fator de crescimento e valores de percentil usados](./media/site-recovery-deployment-planner/max-iops-and-data-churn-setting.png)

## <a name="recommendations-with-available-bandwidth-as-input"></a>Recomendações com largura de banda disponível como entrada

![Recomendações com largura de banda disponível como entrada](./media/site-recovery-deployment-planner/profiling-overview-bandwidth-input.png)

Pode haver uma situação em que você saiba que não é possível definir uma largura de banda de mais de x Mbps para replicação do Site Recovery. Olá ferramenta permite que você tooinput largura de banda disponível (usando Olá - parâmetro de largura de banda durante a geração de relatórios) e get hello atingível RPO em minutos. Com esse valor RPO atingível, você pode decidir se é necessário tooset a largura de banda adicional ou estiver Okey com ter uma solução de recuperação de desastres com este RPO.

![O RPO possível para a largura de banda de 500 Mbps](./media/site-recovery-deployment-planner/achievable-rpos.png)

## <a name="input"></a>Entrada
planilha de entrada Hello fornece que uma visão geral da saudação atribuído ambiente VMware.

![Visão geral da saudação atribuído ambiente VMware](./media/site-recovery-deployment-planner/Input.png)

**Data de início** e **data de término**: Olá datas de início e término de saudação considerados para geração de relatórios de dados de criação de perfil. Por padrão, a data de início da saudação é data hello quando de criação de perfil é iniciada, e a data de término Olá Olá data em que a criação de perfil para. Isso pode ser hello 'StartDate' e 'Data de término' valores se Olá relatório é gerado com esses parâmetros.

**Número total de dias de criação de perfil**: número total de saudação de dias de criação de perfil entre hello datas inicial e final para o qual Olá relatório é gerado.

**Número de máquinas de virtuais compatíveis**: Olá total de VMs compatíveis para qual largura de banda de rede Olá necessários, o número necessário de armazenamento contas, núcleos do Microsoft Azure, servidores de configuração e são servidores de processo adicional calculado.

**Número total de discos em todas as máquinas virtuais compatíveis**: número de saudação que é usado como uma saudação entradas toodecide Olá quantos servidores de configuração e toobe de servidores de processo adicional usados na implantação de saudação.

**Número médio de discos por máquina virtual compatíveis**: média de saudação de discos calculada entre todas as VMs compatíveis.

**Média de tamanho de disco (GB)**: tamanho de média de disco Olá calculado em todas as VMs compatíveis.

**Desejado RPO (minutos)**: O saudação padrão valor ponto de recuperação objetivo ou hello passado para o parâmetro de 'DesiredRPO' de saudação em tempo de saudação do tooestimate de geração de relatório necessários largura de banda.

**Desejado de largura de banda (Mbps)**: Olá valor passado para o parâmetro de 'Largura de banda' hello em tempo de saudação do tooestimate de geração de relatório RPO viável.

**Variação de dados típico observados por dia (GB)**: variação nos dados médio Olá observado em criação de perfil todos os dias. Esse número é usado como uma saudação entradas toodecide Olá quantos servidores de configuração e toobe de servidores de processo adicional usados na implantação de saudação.


## <a name="vm-storage-placement"></a>Posicionamento de VM-Storage

![Posicionamento de VM-Storage](./media/site-recovery-deployment-planner/vm-storage-placement.png)

**Tipo de armazenamento de disco**: uma conta de armazenamento padrão ou premium, que é usado tooreplicate todos Olá correspondentes VMs mencionadas Olá **VMs tooPlace** coluna.

**Sugerido prefixo**: prefixo três caracteres sugeridos Olá que pode ser usado para nomear a conta de armazenamento hello. Você pode usar seu próprio prefixo, mas sugestões da ferramenta Olá segue Olá [convenção de nomenclatura para contas de armazenamento da partição](https://aka.ms/storage-performance-checklist).

**Sugerido nome da conta**: nome de conta de armazenamento Olá após incluir o prefixo sugerido hello. Substitua o nome de saudação colchetes angulares hello (< e >) com a entrada personalizada.

**Conta de armazenamento de log**: todos os logs de replicação de saudação são armazenados em uma conta de armazenamento padrão. Para máquinas virtuais que replicam tooa conta de armazenamento premium, configurar uma conta de armazenamento padrão para armazenamento de log. Uma conta de armazenamento de log standard pode ser usada por várias contas de armazenamento de replicação premium. Máquinas virtuais que são replicados toostandard usam contas de armazenamento Olá a mesma conta de armazenamento para logs.

**Sugerido nome da conta de Log**: O nome da conta armazenamento log depois de incluir o prefixo sugerido hello. Substitua o nome de saudação colchetes angulares hello (< e >) com a entrada personalizada.

**Resumo de posicionamento**: um resumo da saudação total de carregamento de VMs na conta de armazenamento Olá no tempo de saudação de replicação e failover ou failover de teste. Ele inclui o número total de saudação VMs toohello mapeada da conta de armazenamento, total de leitura/gravação IOPS em todas as máquinas virtuais que estão sendo colocadas nesta conta de armazenamento, total de gravação (replicação) IOPS, tamanho total de instalação em todos os discos e o número total de discos.

**Máquinas virtuais tooPlace**: uma lista de todos os Olá VMs que devem ser colocados em Olá considerando a conta de armazenamento para melhor desempenho e uso.

## <a name="compatible-vms"></a>VMs compatíveis
![Planilha do Excel de VMs compatíveis](./media/site-recovery-deployment-planner/compatible-vms.png)

**Nome da VM**: Olá nome da VM ou o endereço IP que é usado em Olá VMListFile quando um relatório é gerado. Essa coluna também lista Olá discos (VMDKs) toohello anexado VMs. toodistinguish vCenter VMs com nomes duplicados ou endereços IP, nomes de saudação incluem nome de host de ESXi hello. Olá host de ESXi listado é hello um onde hello VM foi colocada quando a ferramenta Olá descobertos durante a saudação período de criação de perfil.

**Compatibilidade de VM**: os valores são **Sim** e **Sim**\*. **Sim** \* para instâncias no qual Olá VM é uma opção para [armazenamento Premium do Azure](https://aka.ms/premium-storage-workload). Aqui, Olá atribuído rotatividade alta ou disco de IOPS se ajusta a saudação P20 ou categoria P30, mas Olá tamanho de disco Olá faz com que ele toobe tooa P10 ou P20 mapeado. conta de armazenamento Olá decide qual disco de armazenamento premium digite toomap um disco, com base em seu tamanho. Por exemplo:
* <128 GB é P10.
* 128 GB too512 GB é um P20.
* 512 GB too1024 GB é um P30.
* 1025 GB too2048 GB é um P40.
* 2049 GB too4095 GB é um P50.

Se características de carga de trabalho de saudação de um disco colocá-la em Olá P20 ou categoria P30, mas o tamanho de saudação mapeia para o tipo de disco de armazenamento do tooa inferior premium, a ferramenta Olá marca VM como **Sim**\*. ferramenta de saudação também recomenda que você altere Olá toofit de tamanho de disco de origem em Olá recomendado o tipo de disco de armazenamento premium ou alterar Olá destino disco tipo após o failover.

**Tipo de armazenamento**: standard ou premium.

**Sugerido prefixo**: prefixo de conta de armazenamento de três caracteres hello.

**Conta de armazenamento**: nome de saudação que usa o prefixo de conta de armazenamento sugerido Olá.

**R/W IOPS (com o fator de crescimento)**: Olá pico cargas de trabalho somente leitura IOPS no disco de saudação (o padrão é 95 ° percentil), incluindo o fator de crescimento futuro da saudação (o padrão é 30 por cento). Observe que Olá total leitura/gravação IOPS de uma máquina virtual não é sempre soma de saudação do IOPS de leitura/gravação dos discos da VM Olá individuais, como Olá pico leitura/gravação IOPS de saudação VM é pico de saudação de soma Olá dos seus discos individuais leitura/gravação IOPS durante cada minuto de saudação período de criação de perfil.

**Variação de dados em Mbps (com o fator de crescimento)**: taxa de rotatividade de pico Olá no disco de saudação (o padrão é 95 ° percentil), incluindo o fator de crescimento futuro da saudação (o padrão é 30 por cento). Observe que Olá variação do total de dados de saudação VM não está sempre soma de saudação de rotatividade de dados dos discos individuais da VM Olá, porque rotatividade de dados de pico Olá de saudação VM pico de saudação de soma de saudação de variação dos seus discos individuais durante a cada minuto de saudação período de criação de perfil.

**Tamanho da VM do Azure**: Olá ideal mapeada de tamanho de máquina virtual de serviços de nuvem do Azure para esse local VM. mapeamento de saudação baseia-se a memória da VM do local do hello, número de núcleos/discos/NICs e IOPS de leitura/gravação. recomendação de saudação é sempre Olá menor tamanho da VM Azure que corresponde a todas as características VM do local de saudação.

**Número de discos**: Olá número total de discos de máquina virtual (VMDKs) no hello VM.

**Tamanho (GB) de disco**: Olá tamanho total de instalação de todos os discos de VM de saudação. ferramenta Olá também mostra o tamanho do disco Olá para discos individuais Olá no hello VM.

**Núcleos**: o número de CPUs Olá núcleos na VM de saudação.

**Memória (MB)**: Olá RAM em Olá VM.

**NICs**: Olá número de NICs em Olá VM.

**Tipo de inicialização**: ele é o tipo de inicialização de saudação VM. Pode ser o BIOS ou EFI. Atualmente o Azure Site Recovery dá suporte apenas ao tipo de inicialização BIOS. Todas as máquinas virtuais de saudação do tipo de inicialização EFI são listadas na planilha de VMs incompatível.

**Tipo de SO**: Olá é o tipo de SO do hello VM. Ele pode ser Windows, Linux ou outros.

## <a name="incompatible-vms"></a>VMs incompatíveis

![Planilha do Excel de VMs incompatíveis](./media/site-recovery-deployment-planner/incompatible-vms.png)

**Nome da VM**: Olá nome da VM ou o endereço IP que é usado em Olá VMListFile quando um relatório é gerado. Essa coluna também lista VMDKs Olá que toohello anexado VMs. toodistinguish vCenter VMs com nomes duplicados ou endereços IP, nomes de saudação incluem nome de host de ESXi hello. Olá host de ESXi listado é hello um onde hello VM foi colocada quando a ferramenta Olá descobertos durante a saudação período de criação de perfil.

**Compatibilidade de VM**: indica por que Olá dada VM é incompatível com a recuperação de Site. Hello motivos descritos para cada disco incompatível da saudação VM e, com base na publicação [limites de armazenamento](https://aka.ms/azure-storage-scalbility-performance), pode ser qualquer um dos seguintes hello:

* O tamanho do disco é > 4095 GB. Atualmente, o Armazenamento do Azure não dá suporte a tamanhos de disco de dados maiores que 4095 GB.
* O disco do sistema operacional é >2048 GB. Atualmente, o Armazenamento do Azure não dá suporte a tamanhos de disco do sistema operacional maiores que 2048 GB.
* O tipo de inicialização é EFI. O Azure Site Recovery atualmente dá suporte apenas a máquinas virtuais com tipo de inicialização BIOS.

* Tamanho total da VM (replicação + TFO) excede o limite de tamanho de conta de armazenamento de saudação com suporte (35 TB). Essa incompatibilidade ocorre normalmente quando um único disco no hello VM tem uma característica de desempenho que excede Olá limites máximos com suporte do Azure ou recuperação de Site para o armazenamento padrão. Uma instância envia Olá VM na zona de armazenamento premium Olá. No entanto, Olá máximo tamanho com suporte de uma conta de armazenamento premium é 35 TB e protegido de uma única VM não pode ser protegido entre várias contas de armazenamento. Além disso, observe que quando um failover de teste é executado em uma máquina virtual protegida, ele é executado no hello mesma conta de armazenamento em que a replicação está em andamento. Nesse caso, configure 2 vezes o tamanho de saudação do disco de saudação para replicação tooprogress e toosucceed de failover de teste em paralelo.
* O IOPS de origem excede o limite de IOPS de armazenamento com suporte de 5000 por disco.
* O IOPS de origem excede o limite de IOPS de armazenamento com suporte de 80.000 por VM.
* Variação de média de dados excede o limite do variação de dados de recuperação de Site com suporte de 10 MBps para tamanho médio de e/s de disco de saudação.
* Variação do total de dados em todos os discos em Olá VM excede Olá máximo com suporte recuperação de Site variação de limite de 54 MBps por VM.
* IOPS de gravação efetivo médio excede o limite de IOPS de recuperação de Site de saudação com suporte de 840 para disco.
* Armazenamento de instantâneos calculado excede o limite de armazenamento de instantâneo Olá suportada de 10 TB.

**R/W IOPS (com o fator de crescimento)**: carga de trabalho do hello pico IOPS no disco hello (o padrão é 95 ° percentil), incluindo o fator de crescimento futuro da saudação (o padrão é 30 por cento). Observe que Olá total leitura/gravação IOPS de saudação VM não é sempre soma de saudação do IOPS de leitura/gravação dos discos da VM Olá individuais, como Olá pico leitura/gravação IOPS de saudação VM é pico de saudação de soma Olá dos seus discos individuais leitura/gravação IOPS durante cada minuto de saudação período de criação de perfil.

**Variação de dados em Mbps (com o fator de crescimento)**: taxa de rotatividade de pico Olá no disco de saudação (95 ° Percentil padrão) incluindo o fator de crescimento futuro da saudação (padrão 30 por cento). Observe que Olá variação do total de dados de saudação VM não está sempre soma de saudação de rotatividade de dados dos discos individuais da VM Olá, porque rotatividade de dados de pico Olá de saudação VM pico de saudação de soma de saudação de variação dos seus discos individuais durante a cada minuto de saudação período de criação de perfil.

**Número de discos**: Olá número total de VMDKs em Olá VM.

**Tamanho (GB) de disco**: Olá tamanho total de instalação de todos os discos de VM de saudação. ferramenta Olá também mostra o tamanho do disco Olá para discos individuais Olá no hello VM.

**Núcleos**: o número de CPUs Olá núcleos na VM de saudação.

**Memória (MB)**: quantidade de saudação de RAM no hello VM.

**NICs**: Olá número de NICs em Olá VM.

**Tipo de inicialização**: ele é o tipo de inicialização de saudação VM. Pode ser o BIOS ou EFI. Atualmente o Azure Site Recovery dá suporte apenas ao tipo de inicialização BIOS. Todas as máquinas virtuais de saudação do tipo de inicialização EFI são listadas na planilha de VMs incompatível.

**Tipo de SO**: Olá é o tipo de SO do hello VM. Ele pode ser Windows, Linux ou outros.


## <a name="site-recovery-limits"></a>Limites da Recuperação de Site

**Destino de armazenamento de replicação** | **Tamanho de E/S de disco de origem médio** |**Variação nos dados média do disco de origem** | **Total de variação de dados de disco de origem por dia**
---|---|---|---
Armazenamento Standard | 8 KB | 2 Mbps | 168 GB por disco
Disco Premium P10 | 8 KB | 2 Mbps | 168 GB por disco
Disco Premium P10 | 16 KB | 4 Mbps | 336 GB por disco
Disco Premium P10 | 32 KB ou maior | 8 Mbps | 672 GB por disco
Disco Premium P20 ou P30 | 8 KB  | 5 Mbps | 421 GB por disco
Disco Premium P20 ou P30 | 16 KB ou maior |10 Mbps | 842 GB por disco

Esses são números médios, pressupondo uma sobreposição de E/S de 30%. O Site Recovery pode lidar com uma maior taxa de transferência com base na taxa de sobreposição, em tamanhos maiores de gravação e em comportamento de E/S de carga de trabalho real. Olá anteriores números presumem uma lista de pendências típica de aproximadamente cinco minutos. Ou seja, depois que os dados são carregados, eles são processados, e um ponto de recuperação é criado dentro de cinco minutos.

Esses limites são baseados em nossos testes, mas eles não podem abranger todas as combinações possíveis de E/S de aplicativos. Os resultados reais podem variar dependendo da combinação de E/S do aplicativo. Para obter melhores resultados, mesmo depois de planejamento de implantação, é sempre recomendável que você execute testes usando uma imagem de desempenho verdadeiro teste failover tooget Olá extensiva de aplicativos.

## <a name="updating-hello-deployment-planner"></a>Atualizando o Planejador de implantação Olá
Planejador de implantação do tooupdate hello, Olá a seguir:

1. Baixar a versão mais recente Olá de saudação [Planejador de implantação do Azure Site Recovery](https://aka.ms/asr-deployment-planner).

2. Cópia hello. zip tooa servidor da pasta que você deseja toorun-la no.

3. Extraia a pasta do hello. zip.

4. Siga um destes procedimentos hello:
 * Se a versão mais recente da saudação não contém uma correção de criação de perfil e criação de perfil já está em andamento na sua versão atual do Planejador de hello, continue a saudação de criação de perfil.
 * Se a versão mais recente do hello contêm uma correção de criação de perfil, é recomendável que você parar criação de perfil na sua versão atual e reinicie a saudação de criação de perfil com a nova versão de hello.

  >[!NOTE]
  >
  >Quando você inicia a criação de perfil com hello nova versão, Olá passagem que mesmo caminho de diretório de saída para que hello ferramenta acrescenta dados de perfil no hello arquivos existentes. Um conjunto completo de dados analisados será usado o relatório de saudação toogenerate. Se você passar um diretório de saída diferente, novos arquivos são criados e antigo criado o perfil de dados não será usado toogenerate relatório de saudação.
  >
  >Cada nova Planejador de implantação é uma atualização cumulativa do arquivo. zip de saudação. Você não precisa toocopy hello mais recentes arquivos toohello pasta anterior. Você pode criar e usar uma nova pasta.


## <a name="version-history"></a>Histórico de versão

### <a name="131"></a>1.3.1
Atualização: 19 de julho de 2017

O novo recurso a seguir foi adicionado:

* Suporte adicionado para discos grandes (> 1TB) na geração de relatório. Agora você pode usar a replicação de tooplan do Planejador de implantação de máquinas virtuais com tamanhos de disco maiores que 1 TB (até 4095 GB).
Leia mais sobre [Suporte a discos grandes no Azure Site Recovery](https://azure.microsoft.com/en-us/blog/azure-site-recovery-large-disks/)


### <a name="13"></a>1,3
Atualização: 9 de maio de 2017

O novo recurso a seguir foi adicionado:

* Foi adicionado suporte de disco gerenciado na geração de relatórios. Olá número de máquinas virtuais pode ser colocado armazenamento único tooa conta é calculada com base em se gerenciado disco foi selecionada para failover de teste/Failover.        


### <a name="12"></a>1.2
Última atualização: 7 de abril de 2017

Adicionadas as seguintes correções:

* Inicialização adicionada digite seleção (BIOS ou EFI) para cada máquina virtual toodetermine se a máquina virtual de saudação são compatíveis ou incompatíveis para proteção de saudação.
* Tipo de SO adicionados informações para cada máquina virtual em Olá VMs compatíveis e incompatíveis VMs planilhas.
* Olá GetThroughput operação agora tem suporte em regiões de saudação governo dos EUA e China Microsoft Azure.
* Algumas outras verificações de pré-requisitos foram adicionadas para vCenter e Servidor ESXi.
* Relatório incorreto foi sendo gerado quando as configurações de localidade está definida toonon inglês.


### <a name="11"></a>1,1
Atualização: 9 de março de 2017

Olá fixa problemas a seguir:

* ferramenta de saudação não é possível perfil VMs se Olá vCenter tem duas ou mais VMs com o mesmo nome ou endereço IP hello em vários hosts de ESXi.
* Copiar e pesquisar está desabilitada para planilhas de VMs compatíveis e incompatíveis VMs hello.

### <a name="10"></a>1.0
Atualização: 23 de fevereiro de 2017

Visualização pública de planejamento de implantação de recuperação de Site do Azure 1.0 tem o seguinte hello (toobe abordada em atualizações futuras) de problemas conhecidos:

* ferramenta de saudação funciona somente para cenários de VMware para o Azure, não para implantações de Hyper-V para Azure. Para cenários de Hyper-V para Azure, use Olá [ferramenta do Planejador de capacidade de Hyper-V](./site-recovery-capacity-planning-for-hyper-v-replication.md).
* Olá GetThroughput operação não é suportado em regiões de saudação governo dos EUA e China Microsoft Azure.
* ferramenta Olá não é possível criar o perfil de VMs se o servidor do vCenter Olá tem duas ou mais VMs com o mesmo nome ou endereço IP hello em vários hosts de ESXi. Nesta versão, ferramenta Olá ignora a criação de perfil para nomes duplicados de VM ou endereços IP em Olá VMListFile. solução alternativa de saudação é tooprofile Olá VMs usando um host de ESXi em vez do servidor do vCenter hello. Você deve executar uma instância de cada host ESXi.

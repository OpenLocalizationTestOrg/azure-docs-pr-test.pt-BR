Este artigo descreve um conjunto de práticas comprovadas para executar uma máquina virtual (VM) do Windows no Azure, prestando atenção tooscalability, disponibilidade, capacidade de gerenciamento e segurança.

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes: [Azure Resource Manager][resource-manager-overview] e clássico. Este artigo usa o Gerenciador de Recursos, recomendado pela Microsoft para novas implantações.
>
>

Não recomendamos usar uma única VM para cargas de trabalho críticas, pois elas criam um ponto único de falha. Para obter maior disponibilidade, é necessário implantar várias VMs em um [conjunto de disponibilidade][availability-set]. Para saber mais, confira [Executando várias VMs no Azure][multi-vm].

## <a name="architecture-diagram"></a>Diagrama da arquitetura

O provisionamento de uma VM no Azure envolve mais partes móveis de Olá apenas a própria máquina virtual. Há elementos de computação, de rede e de armazenamento.

> Um documento do Visio que inclui esse diagrama de arquitetura está disponível para download de saudação [Centro de download da Microsoft][visio-download]. Este diagrama é em hello "Computação - VM única" página.
>
>

![[0]][0]

* **Grupo de recursos.** Um [*grupo de recursos*][resource-manager-overview] é um contêiner que armazena os recursos relacionados. Crie um recurso de recursos do grupo toohold Olá para essa VM.
* **VM**. Você pode provisionar uma VM em uma lista de imagens publicadas ou de um arquivo de disco rígido virtual (VHD) que você carregue tooAzure armazenamento de Blob.
* **Disco do sistema operacional.** disco Olá sistema operacional é um VHD armazenado em [armazenamento do Azure][azure-storage]. Isso significa que persistir mesmo se a máquina de host Olá fica inoperante.
* **Disco temporário.** Olá VM é criada com um disco temporário (Olá `D:` unidade no Windows). Esse disco é armazenado em uma unidade física na máquina de host de saudação. *Não* é salvo no Armazenamento do Azure e pode ser excluído durante a reinicialização e outros eventos de ciclo de vida da VM. Use esse disco somente para dados temporários, como arquivos de paginação ou de permuta.
* **Discos de dados.** Um [disco de dados][data-disk] é um VHD persistente usado para dados de aplicativo. Discos de dados são armazenados no armazenamento do Azure, como disco Olá sistema operacional.
* **Rede Virtual e sub-rede.** Cada VM no Azure é implantada em uma Rede Virtual, que é dividida em sub-redes.
* **Endereço IP público.** Um endereço IP público é necessário toocommunicate com hello VM&mdash;por exemplo, pela área de trabalho remota (RDP).
* **NIC (adaptador de rede)**. Olá NIC permite Olá toocommunicate VM com a rede virtual hello.
* **NSG (grupo de segurança de rede)**. Olá [NSG] [ nsg] é usado tooallow/negar sub-rede toohello de tráfego de rede. É possível associar um NSG a uma NIC individual ou a uma sub-rede. Se você a associa a uma sub-rede, as regras NSG Olá aplicam tooall VMs na sub-rede.
* **Diagnósticos.** Log de diagnóstico é essencial para gerenciar e solucionar problemas Olá VM.

## <a name="recommendations"></a>Recomendações

Olá, as recomendações a seguir se aplicam para a maioria dos cenários. Siga estas recomendações, a menos que você tenha um requisito específico que as substitua.

### <a name="vm-recommendations"></a>Recomendações de VM

O Azure oferece vários tamanhos de máquina virtual diferente, mas é recomendável hello e GS-série DS porque esses tamanhos de máquina suportam [armazenamento Premium][premium-storage]. Selecione um desses tamanhos de máquina, a menos que você tenha uma carga de trabalho especializada, como a computação de alto desempenho. Para obter detalhes, confira [tamanhos das máquinas virtuais][virtual-machine-sizes].

Se você estiver movendo um tooAzure de carga de trabalho existente, comece com tamanho de VM de Olá Olá tooyour de correspondência mais próxima servidores locais. Em seguida, Olá medir o desempenho da carga de trabalho real com respeitar tooCPU, memória e operações de entrada/saída de disco por segundo (IOPS) e ajustar o tamanho da saudação se necessário. Se você precisar de várias NICs para sua VM, lembre-se de que o número máximo de saudação de NICs é uma função de saudação [tamanho da VM][vm-size-tables].   

Quando você provisiona hello VM e outros recursos, você deve especificar uma região. Em geral, escolha uma região mais próximos usuários internos de tooyour ou clientes. No entanto, nem todos os tamanhos de VM estão disponíveis em todas as regiões. Para obter detalhes, confira [serviços por região][services-by-region]. toosee uma lista de saudação de tamanhos VM disponível em uma determinada região, executar hello Azure interface de linha de comando (CLI) comando a seguir:

```
azure vm sizes --location <location>
```

Para obter informações sobre como escolher uma imagem da VM publicada, confira [Navegar e selecionar imagens de máquinas virtuais do Windows no Azure com o Powershell ou CLI][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Recomendações de disco e de armazenamento

Para um melhor desempenho de E/S de disco, recomendamos o [Armazenamento Premium][premium-storage], que armazena dados em SSDs (unidades de estado sólido). Custo é baseado no tamanho de saudação do disco provisionado hello. O IOPS e a taxa de transferência também dependem do tamanho do disco. Portanto, ao provisionar um disco, considere todos os três fatores (capacidade, IOPS e taxa de transferência).

Crie contas de armazenamento do Azure separado para cada VM toohold Olá discos rígidos virtuais (VHDs) em ordem tooavoid atingindo os limites de IOPS Olá para contas de armazenamento.

Adicione um ou mais discos de dados. Quando você cria um novo VHD, ele não está formatado. Faça logon no disco de Olá Olá VM tooformat. Se você tiver um grande número de discos de dados, esteja ciente dos limites de e/s total Olá Olá da conta de armazenamento. Para saber mais, confira [limites de disco da máquina virtual][vm-disk-limits].

Quando possível, instale aplicativos em um disco de dados, o disco do sistema operacional não hello. No entanto, alguns aplicativos herdados talvez seja necessário tooinstall componentes Olá unidade c. Nesse caso, você pode [redimensionar disco Olá SO] [ resize-os-disk] usando o PowerShell.

Para melhor desempenho, crie uma conta de armazenamento separada toohold logs de diagnóstico. Uma conta LRS (armazenamento com redundância local) padrão é suficiente para os logs de diagnóstico.

### <a name="network-recommendations"></a>Recomendações de rede

endereço IP público de saudação pode ser estático ou dinâmico. padrão de saudação é dinâmico.

* Reserva um [endereço IP estático] [ static-ip] se é necessário um endereço IP fixo que não serão alteradas &mdash; por exemplo, se você precisar toocreate um um registro no DNS, ou precisa Olá a lista de endereços toobe tooa adicionado segurança IP.
* Você também pode criar um nome de domínio totalmente qualificado (FQDN) para o endereço IP hello. Você pode registrar um [registro CNAME] [ cname-record] no DNS que aponte toohello FQDN. Para obter mais informações, consulte [criar um nome de domínio totalmente qualificado no portal do Azure de saudação][fqdn].

Todos os NSGs contêm um conjunto de [regras padrão][nsg-default-rules], incluindo uma regra que bloqueia todo o tráfego de Internet de entrada. as regras de saudação padrão não podem ser excluídas, mas outras regras podem substituí-las. tooenable tráfego da Internet, criar regras que permitam o tráfego de entrada portas toospecific &mdash; por exemplo, a porta 80 para HTTP.  

tooenable RDP, adicione uma regra NSG que permite que o tráfego de entrada tooTCP porta 3389.

## <a name="scalability-considerations"></a>Considerações sobre escalabilidade

Você pode dimensionar uma VM para cima ou para baixo por [alterar tamanho da VM Olá](../articles/virtual-machines/windows/sizes.md). tooscale out horizontalmente, coloque duas ou mais VMs em um conjunto atrás de um balanceador de carga de disponibilidade. Para obter detalhes, confira [Várias VMs em execução no Azure para escalabilidade e disponibilidade][multi-vm].

## <a name="availability-considerations"></a>Considerações sobre disponibilidade

Para obter maior disponibilidade, é necessário implantar várias VMs em um conjunto de disponibilidade. Isso também fornece um maior [contrato de nível de serviço][vm-sla] (SLA).

Sua VM pode ser afetada por uma [manutenção planejada][planned-maintenance] ou [manutenção não planejada][manage-vm-availability]. Você pode usar [logs de reinicialização de VM] [ reboot-logs] toodetermine se uma VM reinicialização foi causada pela manutenção planejada.

VHDs são armazenados no [armazenamento do Azure][azure-storage] e o armazenamento do Azure é replicado para durabilidade e disponibilidade.

tooprotect contra perda acidental de dados durante operações normais (por exemplo, devido a erro de usuário), você também deve implementar backups point-in-time, usando [instantâneos de blob] [ blob-snapshot] ou outra ferramenta.

## <a name="manageability-considerations"></a>Considerações sobre capacidade de gerenciamento

**Grupos de recursos.** Colocar recursos agrupados que Olá de compartilhamento de ciclo de vida do mesmo em Olá mesmo [grupo de recursos][resource-manager-overview]. Grupos de recursos permitem que você toodeploy e monitor de recursos como um grupo e acumular custos por grupo de recursos de cobrança. Também é possível excluir recursos como um conjunto, o que é muito útil para implantações de teste. Dê nomes significativos aos recursos. Isso torna mais fácil toolocate um recurso específico e entender sua função. Confira [Convenções de nomenclatura recomendadas para recursos do Azure][naming conventions].

**Diagnóstico da VM.** Habilite o monitoramento e diagnóstico, incluindo métricas de integridade básicas, logs de infraestrutura de diagnóstico e [diagnóstico de inicialização][boot-diagnostics]. O diagnóstico de inicialização poderá ajudar a diagnosticar uma falha de inicialização se sua VM entrar em um estado não inicializável. Para saber mais, confira [Habilitar monitoramento e diagnóstico][enable-monitoring]. Saudação de uso [coleta de Log do Azure] [ log-collector] toocollect extensão plataforma Windows Azure logs e carregá-los tooAzure armazenamento.   

Olá CLI comando a seguir permite o diagnóstico:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Interrompendo uma VM.** O Azure faz uma distinção entre os estados "parado" e "desalocado". Você é cobrado quando Olá status da VM é interrompido, mas não quando Olá VM é desalocada.

Use Olá CLI comando toodeallocate uma máquina virtual a seguir:

```
azure vm deallocate <resource-group> <vm-name>
```

No portal do Azure de Olá, Olá **parar** botão desaloca Olá VM. No entanto, se você desligar por meio de saudação SO enquanto estiver conectado, hello VM for interrompida, mas *não* desalocada, portanto você ainda será cobrado.

**Excluindo uma VM.** Se você excluir uma máquina virtual, Olá VHDs não são excluídos. Isso significa que você pode excluir com segurança Olá VM sem perda de dados. No entanto, você ainda será cobrado pelo armazenamento. Olá toodelete VHD, exclua o arquivo de saudação de [armazenamento de Blob][blob-storage].

a exclusão acidental tooprevent, use um [bloqueio de recurso] [ resource-lock] toolock Olá recursos inteiro bloqueio ou grupo de recursos individuais, como Olá VM.

## <a name="security-considerations"></a>Considerações de segurança

Use [Central de segurança do Azure] [ security-center] tooget uma visão central do estado de segurança Olá seus recursos do Azure. Central de segurança monitora problemas potenciais de segurança e fornece uma visão abrangente da integridade de segurança de saudação da sua implantação. A Central de Segurança é configurada por assinatura do Azure. Habilite a coleta de dados de segurança, conforme descrito em [Usar a Central de Segurança]. Depois que a coleta de dados for habilitada, a Central de Segurança examinará automaticamente todas as VMs criadas nessa assinatura.

**Gerenciamento de patch.** Se for habilitada, a Central de Segurança verificará se atualizações críticas e de segurança estão ausentes. Use [configurações de política de grupo] [ group-policy] Olá VM tooenable automática do sistema atualizações.

**Antimalware.** Se for habilitada, a Central de Segurança verificará se o software antimalware está instalado. Você também pode usar o software de antimalware de tooinstall Central de segurança de dentro de Olá portal do Azure.

**Operações.** Use [controle de acesso baseado em função] [ rbac] toohello de acesso (RBAC) toocontrol Azure recursos que você implanta. RBAC permite que você atribua toomembers de funções de autorização de sua equipe de DevOps. Por exemplo, a função de leitor Olá pode exibir os recursos do Azure, mas não criar, gerenciar ou excluí-los. Algumas funções são tipos de recursos do Azure tooparticular específico. Por exemplo, função de Colaborador de máquina Virtual de saudação pode reiniciar ou desalocar uma máquina virtual, redefinir a senha de administrador hello, crie uma nova VM e assim por diante. Outras [funções RBAC internas][rbac-roles] que podem ser úteis para esta arquitetura de referência incluem [Usuário de DevTest Labs][rbac-devtest] e [Colaborador de Rede][rbac-network]. Um usuário pode ser atribuído a funções toomultiple, e você pode criar funções personalizadas para permissões refinadas ainda mais.

> [!NOTE]
> RBAC não limita as ações de saudação que um usuário conectado em uma VM pode executar. Essas permissões são determinadas pelo tipo de conta Olá no sistema operacional convidado de saudação.   
>
>

senha do administrador local Olá tooreset, execute Olá `vm reset-access` comando CLI do Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Use [logs de auditoria] [ audit-logs] toosee provisionamento de ações e outros eventos VM.

**Criptografia de dados.** Considere [criptografia de disco do Azure] [ disk-encryption] se você precisar tooencrypt Olá SO e discos de dados.

## <a name="solution-deployment"></a>Implantação da solução

Uma implantação para essa arquitetura de referência está disponível no [GitHub][github-folder]. Ele inclui uma VNet, NSG e uma única VM. toodeploy Olá arquitetura, siga estas etapas:

1. Botão direito Olá abaixo e selecione a "Abrir link em nova guia" ou "Abrir link em nova janela".  
   [![Implantar tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Depois que o link Olá abriu no hello portal do Azure, você deve inserir valores para algumas das configurações de saudação:

   * Olá **grupo de recursos** nome já está definido no arquivo de parâmetro hello, portanto, selecione **criar novo** e digite `ra-single-vm-rg` na caixa de texto de saudação.
   * Região Olá Select de saudação **local** caixa suspensa.
   * Não edite Olá **modelo raiz Uri** ou hello **parâmetro raiz Uri** caixas de texto.
   * Selecione **windows** em Olá **tipo de SO** caixa suspensa.
   * Examine Olá termos e condições, clique em Olá **concordo toohello termos e condições declaradas acima** caixa de seleção.
   * Clique em Olá **compra** botão.
3. Aguarde Olá toocomplete de implantação.
4. arquivos de parâmetro Hello incluem um nome de usuário administrador embutida e uma senha, e é altamente recomendável que você altere imediatamente ambos. Clique em Olá VM denominada `ra-single-vm0 `no hello portal do Azure. Em seguida, clique em **Redefinir senha** em Olá **suporte + solução de problemas** folha. Selecione **Redefinir senha** em Olá **modo** caixa de lista suspensa, selecione um novo **nome de usuário** e **senha**. Clique em Olá **atualização** botão toopersist Olá novo nome de usuário e senha.

Para obter informações sobre outras maneiras toodeploy esta arquitetura de referência, consulte o arquivo Leiame de saudação em Olá [orientação de único de vm][github-folder]] pasta GitHub.

## <a name="customize-hello-deployment"></a>Personalizar a implantação de saudação
Se você precisar toochange Olá implantação toomatch suas necessidades, siga as instruções de Olá Olá [Leiame][github-folder].

## <a name="next-steps"></a>Próximas etapas
Para maior disponibilidade, implante duas ou mais VMs atrás de um balanceador de carga. Para saber mais, confira [Executando várias VMs no Azure][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Usar a Central de Segurança]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Única arquitetura de VM do Windows no Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks

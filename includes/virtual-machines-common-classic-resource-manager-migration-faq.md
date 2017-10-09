# <a name="frequently-asked-questions-about-classic-tooazure-resource-manager-migration"></a>Perguntas frequentes sobre o Gerenciador de recursos de migração de clássico tooAzure

## <a name="does-this-migration-plan-affect-any-of-my-existing-services-or-applications-that-run-on-azure-virtual-machines"></a>Este plano de migração afeta qualquer um de meus serviços existentes ou aplicativos executados em máquinas virtuais do Azure? 

Não. Olá VMs (clássicas) são totalmente suportados serviços na disponibilidade geral. Você pode continuar toouse tooexpand esses recursos o volume no Microsoft Azure.

## <a name="what-happens-toomy-vms-if-i-dont-plan-on-migrating-in-hello-near-future"></a>O que acontece toomy VMs se eu não planeja migração em Olá futuro próximo? 

Não podemos são reprovando Olá clássico APIs e recursos modelo existente. Queremos toomake migração fácil, considerando Olá recursos avançados que estão disponíveis no modelo de implantação do Gerenciador de recursos de saudação. É altamente recomendável que você examine [alguns dos avanços Olá](../articles/azure-resource-manager/resource-manager-deployment-model.md) que fazem parte do IaaS no Gerenciador de recursos.

## <a name="what-does-this-migration-plan-mean-for-my-existing-tooling"></a>O que este plano de migração significa para minhas ferramentas existentes? 

Atualizar seu modelo de implantação do Gerenciador de recursos de toohello ferramentas é uma das alterações mais importantes de saudação com tooaccount nos planos de migração.

## <a name="how-long-will-hello-management-plane-downtime-be"></a>Quanto tempo será o tempo de inatividade do hello plano de gerenciamento? 

Depende do número de saudação de recursos que estão sendo migrados. Para implantações menores (algumas dezenas de máquinas virtuais), a migração de todo Olá deve levar menos de uma hora. Para implantações de grande escala (centenas de máquinas virtuais), a migração de saudação pode levar algumas horas.

## <a name="can-i-roll-back-after-my-migrating-resources-are-committed-in-resource-manager"></a>Poderei reverter depois que meus recursos de migração forem confirmados no Gerenciador de Recursos? 

Você pode anular sua migração enquanto há recursos de Olá Olá preparado estado. A reversão não tem suporte depois recursos Olá foram migrados com êxito por meio de uma operação de confirmação hello.

## <a name="can-i-roll-back-my-migration-if-hello-commit-operation-fails"></a>Pode, reverter a minha migração se a operação de confirmação Olá falhar? 

Não é possível anular migração, se a operação de confirmação Olá falhar. Todas as operações de migração, incluindo a operação de confirmação de saudação são idempotentes. Portanto, recomendamos que você repetir a operação de saudação após um curto período de tempo. Se você ainda encontrar erro, crie um tíquete de suporte ou crie uma postagem no fórum com hello ClassicIaaSMigration marca em nosso [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows).

## <a name="do-i-have-toobuy-another-express-route-circuit-if-i-have-toouse-iaas-under-resource-manager"></a>É necessário toobuy outro circuito de rota expressa se eu tiver toouse no Gerenciador de recursos de IaaS? 

Não. Habilitamos recentemente [movendo circuitos ExpressRoute de modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../articles/expressroute/expressroute-move.md). Você não tem um novo circuito de rota expressa de toobuy se você já tiver um.

## <a name="what-if-i-had-configured-role-based-access-control-policies-for-my-classic-iaas-resources"></a>E se eu tiver configurado políticas de Controle de Acesso Baseado em Função para meus recursos clássicos de IaaS? 

Durante a migração, os recursos de saudação transformam de clássico tooResource Manager. Portanto, é recomendável que você planejar atualizações de política RBAC Olá que precisam toohappen após a migração.

## <a name="i-backed-up-my-classic-vms-in-a-backup-vault-can-i-migrate-my-vms-from-classic-mode-tooresource-manager-mode-and-protect-them-in-a-recovery-services-vault"></a>Fiz backup de minhas VMs clássicas em um cofre de Backup. É possível migrar Minhas VMs de modo do Gerenciador de tooResource de modo clássico e protegê-los em um cofre de serviços de recuperação? 

Pontos de recuperação clássicos VM em um cofre de backup não migrar automaticamente tooa Cofre de serviços de recuperação quando você move Olá VM de tooResource clássico modo do Gerenciador. Siga estas etapas tootransfer seus backups VM:

1. No cofre de Backup hello, acesse toohello **itens protegidos** guia e selecione Olá VM. Clique em [Parar Proteção](../articles/backup/backup-azure-manage-vms-classic.md#stop-protecting-virtual-machines). Deixe a opção *Excluir dados de backup associados***desmarcada**.
2. Exclua a extensão de backup/instantâneo de saudação da saudação VM.
3. Migre máquina virtual de saudação do modo do Gerenciador de tooResource de modo clássico. Certifique-se de informações de rede e armazenamento de saudação máquina de virtual toohello correspondente também é migrado tooResource Manager modo.
4. Criar um cofre de serviços de recuperação e configurar backup em Olá migrados máquina virtual usando **Backup** ação na parte superior do painel do cofre. Para obter informações detalhadas sobre como fazer backup dos serviços de recuperação de tooa VM cofre, consulte o artigo hello, [proteger máquinas virtuais do Azure com um cofre de serviços de recuperação](../articles/backup/backup-azure-vms-first-look-arm.md).

## <a name="can-i-validate-my-subscription-or-resources-toosee-if-theyre-capable-of-migration"></a>Eu Validar minha assinatura ou toosee recursos se eles são capazes de migração? 

Sim. Opção de migração com suporte para plataforma Olá, Olá primeira etapa na preparação para a migração é toovalidate que recursos Olá são capazes de migração. No caso de Olá validar a operação falhar, você receberá mensagens para todos os motivos Olá Olá migração não pode ser concluída.

## <a name="what-happens-if-i-run-into-a-quota-error-while-preparing-hello-iaas-resources-for-migration"></a>O que acontece se eu executar em um erro de cota ao preparar recursos de IaaS Olá migração? 

É recomendável que você anule a migração e, em seguida, log cotas de saudação de suporte da solicitação tooincrease na região Olá onde você está migrando Olá VMs. Após a aprovação de solicitação de cota Olá, você pode começar a executar etapas de migração de saudação novamente.

## <a name="how-do-i-report-an-issue"></a>Como faço para relatar um problema? 

Poste seus problemas e perguntas sobre migração tooour [fórum VM](https://social.msdn.microsoft.com/Forums/azure/home?forum=WAVirtualMachinesforWindows), com a palavra-chave Olá ClassicIaaSMigration. É recomendável postar todas as suas dúvidas neste fórum. Se você tiver um contrato de suporte, você está bem-vindo toolog um tíquete de suporte.

## <a name="what-if-i-dont-like-hello-names-of-hello-resources-that-hello-platform-chose-during-migration"></a>Se eu não gostar nomes Olá recursos Olá Olá plataforma escolhida durante a migração? 

Todos os recursos de saudação explicitamente fornecer nomes para no modelo de implantação clássico Olá são mantidos durante a migração. Em alguns casos, novos recursos são criados. Por exemplo: uma interface de rede é criada para cada VM. Atualmente não há suporte para Olá capacidade toocontrol Olá nomes desses novos recursos criados durante a migração. Faça seus votos para esse recurso em hello [Fórum de comentários do Azure](http://feedback.azure.com).

## <a name="can-i-migrate-expressroute-circuits-used-across-subscriptions-with-authorization-links"></a>Posso migrar circuitos de ExpressRoute usados em assinaturas com links de autorização? 

Os circuitos de ExpressRoute que usam links de autorização entre assinaturas não podem ser migrados automaticamente sem tempo de inatividade. Temos orientações sobre como eles podem ser migrados usando as etapas manuais. Consulte [ExpressRoute migrar circuitos e associadas a redes virtuais do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](../articles/expressroute/expressroute-migration-classic-resource-manager.md) para obter mais informações.

## <a name="i-got-a-message-vm-is-reporting-hello-overall-agent-status-as-not-ready-hence-hello-vm-cannot-be-migrated-ensure-that-hello-vm-agent-is-reporting-overall-agent-status-as-ready-or-vm-contains-extension-whose-status-is-not-being-reported-from-hello-vm-hence-this-vm-cannot-be-migrated-"></a>Recebi uma mensagem *"VM está relatando Olá status geral do agente como não pronto. Portanto, a saudação VM não pode ser migrada. Certifique-se de que o agente de VM hello está relatando status geral do agente como pronto"* ou *"VM contém a extensão cujo Status não está sendo informado de saudação VM. Portanto, esta VM não pode ser migrada." *

Essa mensagem é recebida quando Olá VM não tem conectividade de saída toohello internet. Olá VM agent usa a conta de armazenamento do Azure conectividade de saída tooreach Olá para atualizar o status do agente Olá a cada cinco minutos.

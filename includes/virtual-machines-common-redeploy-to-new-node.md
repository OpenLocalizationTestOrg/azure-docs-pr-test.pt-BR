## <a name="use-the-azure-portal"></a><span data-ttu-id="dde31-101">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dde31-101">Use the Azure portal</span></span>
1. <span data-ttu-id="dde31-102">Selecione a VM que você deseja reimplantar e clique no botão *Reimplantar* na folha *Configurações*.</span><span class="sxs-lookup"><span data-stu-id="dde31-102">Select the VM you wish to redeploy, then select the *Redeploy* button in the *Settings* blade.</span></span> <span data-ttu-id="dde31-103">Talvez seja necessário rolar para baixo a fim de ver a seção **Suporte e solução de problemas** que contém o botão 'Reimplantar' como no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="dde31-103">You may need to scroll down to see the **Support and Troubleshooting** section that contains the 'Redeploy' button as in the following example:</span></span>
   
    ![Folha VM do Azure](./media/virtual-machines-common-redeploy-to-new-node/vmoverview.png)
2. <span data-ttu-id="dde31-105">Para confirmar a operação, clique no botão *Reimplantar*:</span><span class="sxs-lookup"><span data-stu-id="dde31-105">To confirm the operation, select the *Redeploy* button:</span></span>
   
    ![Folha Reimplantar uma VM](./media/virtual-machines-common-redeploy-to-new-node/redeployvm.png)
3. <span data-ttu-id="dde31-107">O **Status** da VM muda para *Atualizando* à medida que a VM é preparada para a reimplantação, como mostrado no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="dde31-107">The **Status** of the VM changes to *Updating* as the VM prepares to redeploy, as shown in the following example:</span></span>
   
    ![VM atualizando](./media/virtual-machines-common-redeploy-to-new-node/vmupdating.png)
4. <span data-ttu-id="dde31-109">O **Status** mudará para *Iniciando* enquanto a VM é inicializada em um novo host do Azure, como mostrado no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="dde31-109">The **Status** then changes to *Starting* as the VM boots up on a new Azure host, as shown in the following example:</span></span>
   
    ![VM iniciando](./media/virtual-machines-common-redeploy-to-new-node/vmstarting.png)
5. <span data-ttu-id="dde31-111">Após a conclusão do processo de inicialização da VM, o **Status** retornará a *Em execução*, indicando que a VM foi reimplantada com êxito:</span><span class="sxs-lookup"><span data-stu-id="dde31-111">After the VM finishes the boot process, the **Status** then returns to *Running*, indicating the VM has been successfully redeployed:</span></span>
   
    ![VM em execução](./media/virtual-machines-common-redeploy-to-new-node/vmrunning.png)


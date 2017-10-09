## <a name="scenario"></a>Cenário
toobetter ilustram como toocreate UDRs, este documento usará cenário de saudação abaixo.

![DESCRIÇÃO DA IMAGEM](./media/virtual-network-create-udr-scenario-include/figure1.png)

Nesse cenário, você criará um UDR para Olá *sub-rede do Front end* e outro UDR para Olá *subrede Back end* , conforme descrito abaixo: 

* **UDR-FrontEnd**. Olá front-end UDR será aplicado toohello *front-end* sub-rede e conter uma rota:    
  * **RouteToBackend**. Essa rota enviará todos os tráfego toohello back-end subrede toohello **FW1** máquina virtual.
* **UDR-BackEnd**. back-end de saudação UDR será aplicado toohello *back-end* sub-rede e conter uma rota:    
  * **RouteToFrontend**. Essa rota enviará todos os tráfego toohello front-end subrede toohello **FW1** máquina virtual.

combinação de saudação dessas rotas garantirá que todo o tráfego destinado a partir de um tooanother de sub-rede será roteado toohello **FW1** máquina virtual, que está sendo usada como um dispositivo virtual. Você também precisa tooturn no encaminhamento IP para a VM, tooensure pode receber o tráfego destinado tooother VMs.


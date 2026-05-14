# Configurando Windows Server 2025 com VMware Workstation Pro

Este repositório documenta a criação e configuração inicial de uma máquina virtual com **Windows Server 2025** utilizando o **VMware Workstation Pro**.

A ideia deste laboratório é simular um ambiente de servidor em máquina virtual, deixando a instalação pronta para estudos posteriores de administração de sistemas, redes, Active Directory, DNS, DHCP, GPOs e hardening básico.

---

## Objetivo do laboratório

Criar uma máquina virtual com Windows Server 2025 no VMware Workstation Pro, realizando desde a criação da VM até as configurações iniciais do sistema operacional.

Ao final do laboratório, a máquina virtual estará instalada, atualizada, com VMware Tools instalado, nome de host definido, configuração de rede validada e snapshot criado.

---

## Ambiente utilizado

| Item | Descrição |
|---|---|
| Virtualizador | VMware Workstation Pro |
| Sistema operacional convidado | Windows Server 2025 |
| Tipo de instalação | Desktop Experience |
| Mídia de instalação | ISO oficial do Windows Server 2025 |
| Finalidade | Laboratório local |

---

## Estrutura do repositório

```text
configurando-windows-server-2025-com-vmware/
├── README.md
├── docs/
│   ├── 00-planejamento.md
│   ├── 01-criacao-da-maquina-virtual.md
│   ├── 02-instalacao-do-windows-server-2025.md
│   ├── 03-configuracoes-iniciais.md
│   ├── 04-vmware-tools-e-snapshot.md
│   ├── 05-troubleshooting.md
│   └── REFERENCIAS.md
└── assets/
    ├── prints/
    └── diagramas/
```

---

# Primeiro Passo

## Baixar a ISO do Windows Server 2025

Acesse o **Microsoft Evaluation Center** e baixe a ISO do Windows Server 2025.

A edição de avaliação permite instalar e testar o sistema por tempo limitado, sendo suficiente para laboratório.

> Referência: https://www.microsoft.com/pt-br/evalcenter/download-windows-server-2025

Após o download, mantenha o arquivo ISO em uma pasta de fácil acesso.

Exemplo:

```text
C:\ISOs\Windows_Server_2025.iso
```

---

# Segundo Passo

## Criar a máquina virtual no VMware Workstation Pro

No VMware Workstation Pro, clique em:

```text
File > New Virtual Machine
```

Selecione:

```text
Typical (recommended)
```

Em seguida, escolha a ISO do Windows Server 2025.

Caso o VMware não exiba a opção específica para Windows Server 2025, utilize a opção mais próxima disponível, como:

```text
Microsoft Windows Server 2022 (64-bit)
```

Isso não impede a instalação do Windows Server 2025 no laboratório.


---

# Terceiro Passo

## Definir os recursos da máquina virtual

Para um laboratório com interface gráfica, utilize uma configuração confortável:

| Recurso | Sugestão para laboratório |
|---|---|
| Processador | 2 núcleos |
| Memória RAM | 4 GB ou mais |
| Disco | 60 GB ou mais |
| Rede | NAT ou Bridged |
| Firmware | UEFI |
| Secure Boot | Opcional |
| TPM virtual | Opcional, caso queira testar recursos de segurança |

Configuração mínima demais pode deixar a instalação lenta ou até falhar em alguns cenários. Para uso com interface gráfica, 4 GB de RAM é uma escolha mais adequada.


---

# Quarto Passo

## Configurar a rede da máquina virtual

Escolha o modo de rede conforme o objetivo do laboratório.

## NAT

Use NAT quando quiser que a VM acesse a internet utilizando a conexão do host, sem aparecer diretamente na rede física.

Indicado para:

- Laboratórios simples
- Instalação de atualizações
- Testes isolados
- Ambientes em que não é necessário acessar a VM por outros dispositivos da rede

## Bridged

Use Bridged quando quiser que a VM receba um IP da mesma rede física do host.

Indicado para:

- Testes com acesso remoto
- Comunicação com outros dispositivos da rede
- Cenários com domínio, DNS, DHCP e serviços acessíveis externamente

Para este laboratório, NAT é suficiente no primeiro momento.


---

# Quinto Passo

## Instalar o Windows Server 2025

Inicie a máquina virtual e siga o assistente de instalação.

Selecione:

```text
Windows Server 2025 Standard Evaluation (Desktop Experience)
```

A opção **Desktop Experience** instala a interface gráfica, facilitando o uso em laboratório.

Depois, escolha:

```text
Custom: Install Microsoft Server Operating System only
```

Selecione o disco virtual criado anteriormente e prossiga com a instalação.

---

# Sexto Passo

## Criar a senha do Administrador

Após a instalação, o Windows Server solicitará a criação da senha do usuário local:

```text
Administrator
```

Use uma senha forte, principalmente se a VM estiver em modo Bridged ou for acessível na rede.

Exemplo de critérios:

- No mínimo 12 caracteres
- Letras maiúsculas e minúsculas
- Números
- Caracteres especiais
- Não utilizar senhas óbvias ou reutilizadas


---

# Sétimo Passo

## Instalar o VMware Tools

Com o Windows Server iniciado, no menu do VMware clique em:

```text
VM > Install VMware Tools
```

Dentro da VM, abra o instalador montado no drive virtual e siga o assistente.

O VMware Tools melhora a integração entre o host e a VM, incluindo:

- Melhor desempenho de vídeo
- Melhor controle do mouse
- Sincronização de horário
- Drivers otimizados
- Redimensionamento de tela
- Melhor integração com o ambiente virtual

Após instalar, reinicie a máquina virtual.


---

# Oitavo Passo

## Renomear o servidor

Após reiniciar, altere o nome do servidor.

Acesse:

```text
Server Manager > Local Server > Computer Name
```

Clique no nome atual da máquina e altere para algo mais identificável.

Exemplo:

```text
SRV-2025-LAB
```

Também é possível fazer pelo PowerShell:

```powershell
Rename-Computer -NewName "SRV-2025-LAB" -Restart
```

Após a reinicialização, valide o nome da máquina:

```powershell
hostname
```


---

# Nono Passo

## Validar conectividade de rede

Abra o PowerShell e execute:

```powershell
ipconfig
```

Verifique se a VM recebeu um endereço IP.

Depois teste conectividade:

```powershell
ping 8.8.8.8
```

Teste também resolução DNS:

```powershell
nslookup microsoft.com
```

Se o ping por IP funcionar, mas o nslookup falhar, o problema provavelmente está relacionado à configuração de DNS.


---

# Décimo Passo

## Executar Windows Update

Acesse:

```text
Settings > Windows Update
```

Instale as atualizações disponíveis.

Também é possível verificar pelo PowerShell:

```powershell
Get-HotFix
```

Manter o servidor atualizado é importante antes de instalar funções como Active Directory, DNS, DHCP ou serviços de aplicação.



---

# Décimo Primeiro Passo

## Criar um snapshot da máquina virtual

Com a instalação concluída e validada, desligue ou mantenha a VM em estado estável.

No VMware Workstation Pro, clique em:

```text
VM > Snapshot > Take Snapshot
```

Nome sugerido:

```text
Instalacao-limpa-Windows-Server-2025
```

Descrição sugerida:

```text
Windows Server 2025 instalado, VMware Tools configurado, rede validada e sistema atualizado.
```

Esse snapshot permite retornar ao estado inicial caso algum teste futuro quebre o ambiente.



---

# Validação Final

Ao final do laboratório, valide os seguintes pontos:

- [ ] A VM inicializa corretamente
- [ ] O Windows Server 2025 foi instalado com Desktop Experience
- [ ] A senha do Administrator foi definida
- [ ] O VMware Tools foi instalado
- [ ] O nome do servidor foi alterado
- [ ] A VM possui endereço IP
- [ ] A VM acessa a internet
- [ ] A resolução DNS funciona
- [ ] O Windows Update foi executado
- [ ] O snapshot inicial foi criado

---

# Resultado

A máquina virtual com Windows Server 2025 foi criada, instalada e preparada para laboratórios futuros.

A partir deste ponto, o ambiente pode ser utilizado para estudos de:

- Active Directory Domain Services
- DNS Server
- DHCP Server
- Group Policy Objects
- File Server
- Hardening de Windows Server
- Administração remota
- Monitoramento e logs
- Segurança em ambiente Windows

---

## Referências

- Microsoft Evaluation Center - Windows Server 2025  
  https://www.microsoft.com/pt-br/evalcenter/download-windows-server-2025

- Microsoft Learn - Requisitos de hardware do Windows Server  
  https://learn.microsoft.com/pt-br/windows-server/get-started/hardware-requirements

- Broadcom/VMware - Installing Windows Server 2025 on a VMware Virtual Machine  
  https://knowledge.broadcom.com/external/article/371350/installing-windows-server-2025-on-a-vmwa.html

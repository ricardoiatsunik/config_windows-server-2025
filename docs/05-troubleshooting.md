# 05 - Troubleshooting

## A VM não inicia pela ISO

Verifique:

- Se a ISO está conectada no drive virtual
- Se a opção `Connect at power on` está marcada
- Se a ordem de boot está correta
- Se a ISO não está corrompida

---

## Instalação muito lenta

Possíveis ações:

- Aumentar a memória RAM
- Aumentar a quantidade de núcleos
- Fechar aplicações pesadas no host
- Utilizar disco SSD/NVMe
- Evitar rodar muitas VMs ao mesmo tempo

---

## Sem internet na VM

Verifique:

- Se o adaptador de rede está conectado
- Se está em NAT ou Bridged
- Se a VM recebeu IP via DHCP
- Se o DNS está respondendo

Comandos úteis:

```powershell
ipconfig
ping 8.8.8.8
nslookup microsoft.com
```

---

## Tela pequena ou resolução incorreta

Instale ou reinstale o VMware Tools.

---

## VMware não mostra Windows Server 2025 na lista

Selecione:

```text
Windows Server 2022 (64-bit)
```

A instalação pode seguir normalmente usando a ISO do Windows Server 2025.

---

## Erro durante atualização

Tente:

```powershell
sfc /scannow
```

E depois:

```powershell
DISM /Online /Cleanup-Image /RestoreHealth
```

Reinicie a VM e execute o Windows Update novamente.

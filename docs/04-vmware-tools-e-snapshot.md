# 04 - VMware Tools e Snapshot

## Instalar VMware Tools

No menu do VMware Workstation Pro, clique em:

```text
VM > Install VMware Tools
```

Dentro do Windows Server, execute o instalador montado no drive virtual.

Após concluir, reinicie a VM.

---

## Por que instalar o VMware Tools?

O VMware Tools melhora a integração entre a máquina virtual e o host.

Principais benefícios:

- Melhor desempenho gráfico
- Melhor controle do mouse
- Drivers otimizados
- Sincronização de horário
- Redimensionamento de tela
- Melhor estabilidade da VM

---

## Criar snapshot

Com a VM instalada, atualizada e validada, crie um snapshot.

Caminho:

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

---

## Print sugerido

```md
![Snapshot inicial](../assets/prints/12-snapshot-inicial.png)
```

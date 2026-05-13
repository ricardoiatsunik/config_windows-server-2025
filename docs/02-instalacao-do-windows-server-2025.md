# 02 - Instalação do Windows Server 2025

Após criar a máquina virtual, inicie a VM.

O instalador do Windows Server será carregado pela ISO.

---

## Seleção da edição

Selecione a edição com interface gráfica:

```text
Windows Server 2025 Standard Evaluation (Desktop Experience)
```

A instalação com Desktop Experience facilita o uso em laboratório, principalmente para quem ainda está estudando administração de Windows Server.

---

## Tipo de instalação

Selecione:

```text
Custom: Install Microsoft Server Operating System only
```

Depois selecione o disco virtual criado no VMware.

---

## Senha do Administrator

Ao final da instalação, defina uma senha forte para o usuário local:

```text
Administrator
```

Evite senhas fracas, principalmente se a VM estiver em modo Bridged.

---

## Prints sugeridos

```md
![Seleção da edição](../assets/prints/05-selecao-edicao.png)
![Instalação em andamento](../assets/prints/06-instalacao-andamento.png)
![Primeiro login](../assets/prints/07-primeiro-login.png)
```

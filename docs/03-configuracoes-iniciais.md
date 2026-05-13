# 03 - Configurações Iniciais

Após o primeiro login, realize as configurações básicas do servidor.

---

## Renomear o servidor

Abra o PowerShell como administrador e execute:

```powershell
Rename-Computer -NewName "SRV-2025-LAB" -Restart
```

Após reiniciar, valide:

```powershell
hostname
```

---

## Verificar IP

Execute:

```powershell
ipconfig
```

Verifique se a VM recebeu endereço IP.

---

## Testar conectividade

Teste conexão por IP:

```powershell
ping 8.8.8.8
```

Teste resolução DNS:

```powershell
nslookup microsoft.com
```

Se o ping por IP funcionar e o nslookup falhar, o problema provavelmente está no DNS.

---

## Windows Update

Acesse:

```text
Settings > Windows Update
```

Instale as atualizações disponíveis.

Também é possível listar atualizações instaladas com:

```powershell
Get-HotFix
```

---

## Prints sugeridos

```md
![Nome do servidor](../assets/prints/09-nome-servidor.png)
![Teste de rede](../assets/prints/10-teste-rede.png)
![Windows Update](../assets/prints/11-windows-update.png)
```

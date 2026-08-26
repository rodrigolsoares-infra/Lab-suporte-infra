## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 9. `CGPO_SEC_Desativar_SMBv1`

- **Objetivo:** Desabilitar o protocolo legado SMBv1 para mitigar riscos de movimentação lateral de malwares.
    
- **Link da OU:** `OU=Computadores,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `Computer Configuration -> Preferences -> Windows Settings -> Registry`
    
- **Passo a Passo:**
    
    1. Criar novo item de Registro (Action: **Update**, Hive: `HKEY_LOCAL_MACHINE`).
        
    2. Key Path: `SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters`.
        
    3. Value Name: `SMB1`, Value Type: `REG_DWORD`, Value Data: `0`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência SMBv1 Desativado](.github/assets/gpo-cgpo-sec-smbv1-disabled.png)
    ```
    
    _(Sugestão de print: Saída do comando `Get-SmbServerConfiguration` demonstrando `EnableSMB1Protocol : False`)_
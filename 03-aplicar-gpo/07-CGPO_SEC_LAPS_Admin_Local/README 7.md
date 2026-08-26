## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 7. `CGPO_SEC_LAPS_Admin_Local`

- **Objetivo:** Rotacionar automaticamente senhas exclusivas para a conta de Administrador Local via LAPS.
    
- **Link da OU:** `OU=Computadores,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `Computer Configuration -> Policies -> Administrative Templates -> LAPS`
    
- **Passo a Passo:**
    
    1. Abrir `Password Settings` -> Marcar **Enabled** -> Ajustar tamanho (ex: 14) e expiração (30 dias).
        
    2. Abrir `Name of administrator account to manage` -> Informar o nome do usuário local personalizado (ex: `AdminLocalCorp`).
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Consulta LAPS PowerShell](.github/assets/gpo-cgpo-sec-laps-powershell.png)
    ```
    
    _(Sugestão de print: Execução do cmdlet `Get-LapsADPassword` no PowerShell exibindo a senha complexa retornada do AD)_
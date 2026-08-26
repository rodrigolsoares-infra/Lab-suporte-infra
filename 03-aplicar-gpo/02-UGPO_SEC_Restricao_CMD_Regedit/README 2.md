## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 2. `UGPO_SEC_Restricao_CMD_Regedit`

- **Objetivo:** Mitigar a execução de scripts não autorizados e edições nocivas no registro do Windows.
    
- **Link da OU:** `OU=Usuarios,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `User Configuration -> Policies -> Administrative Templates -> System`
    
- **Passo a Passo:**
    
    1. Abrir `Prevent access to the command prompt` -> Marcar **Enabled** -> Em _"Disable the command prompt script processing?"_ selecionar **No** (permite que scripts de logon rodem, mas bloqueia o terminal interativo).
        
    2. Abrir `Prevent access to registry editing tools` -> Marcar **Enabled**.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência CMD Bloqueado](.github/assets/gpo-ugpo-sec-restricao-cmd-disabled.png)
    ```
    
    *(Sugestão de print: Terminal do Prompt de Comando com a mensagem _"O prompt de comando foi desativado pelo administrador"_)
## 🛠️ Detalhamento e Passo a Passo da GPO

#### Implementação de Políticas de Grupo (GPOs) A infraestrutura foi configurada com um modelo de governança baseado em separação de escopos (`CGPO_` para Computador e `UGPO_` para Usuário). Para visualizar a **Matriz de GPOs Corporativos**, a arquitetura de linkagem nas OUs e acessar a documentação individual de cada uma das 10 políticas aplicadas, acesse: 
## 👉 **[Acessar a Matriz e Documentação de GPOs](./aplicar-gpo.md)** 

### 8. `UGPO_ENV_Redirecionamento_Pastas`

- **Objetivo:** Armazenar os arquivos da Área de Trabalho e Documentos no File Server para centralizar o backup.
    
- **Link da OU:** `OU=Usuarios,OU=Empresa_CORP`
    
- **Caminho no GPMC:** `User Configuration -> Policies -> Windows Settings -> Folder Redirection -> Desktop`
    
- **Passo a Passo:**
    
    1. Clicar com botão direito em _Desktop_ -> _Properties_.
        
    2. Setting: **Basic - Redirect everyone's folder to the same location**.
        
    3. Target folder location: **Create a folder for each user under the root path**.
        
    4. Root Path: `\\DC01\UserProfiles$`.
        
- **Evidência Visual (Link do Print):**
    
    Markdown
    
    ```
    ![Evidência Redirecionamento Pastas](.github/assets/gpo-ugpo-env-folder-redirect.png)
    ```
    
    _(Sugestão de print: Aba Propriedades da pasta "Área de Trabalho" no Windows Explorer mostrando o caminho de rede UNC)_
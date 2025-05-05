# dio-azure-database-lab
# Desafio: Configurando uma Instância de Banco de Dados no Azure

**Descrição:**

Este repositório documenta minha jornada na configuração de uma instância de Banco de Dados no Microsoft Azure.  O objetivo é consolidar os conhecimentos adquiridos durante o desafio, fornecendo um guia prático e acessível para futuros estudos e implementações na plataforma Azure.  Segui as vídeo-aulas e a documentação oficial para compreender os passos e os conceitos envolvidos.

---

## Conteúdo do Repositório:

*   **`README.md` (Este Arquivo):**
    *   Visão geral do desafio e do repositório.
    *   Lista de arquivos e informações contidas.
    *   Objetivos de aprendizagem alcançados.
    *   Guia passo a passo para a criação da instância.
    *   Considerações finais e próximos passos.
    *   Recursos adicionais relevantes.
    *   Referências às imagens de apoio (se houver).

*   **`images/` (Pasta de Imagens - Opcional):**
    *   Capturas de tela para ilustrar as etapas de configuração, facilitando a compreensão visual.  Organizadas por etapa (ex: `01_portal_azure.png`, `02_create_resource_group.png`, etc.).

*   **`anotacoes_dicas.md` (Arquivo de Anotações - Opcional):**
    *   Arquivo em formato Markdown com minhas anotações pessoais sobre os conceitos aprendidos.
    *   Dicas e melhores práticas para configurar e gerenciar instâncias de banco de dados no Azure.
    *   Exemplos de comandos e configurações úteis.

---

## Objetivos de Aprendizagem Alcançados:

*   Compreensão dos conceitos fundamentais da plataforma Microsoft Azure.
*   Familiaridade com a interface do portal Azure.
*   Conhecimento detalhado dos passos para configurar uma instância de Banco de Dados (SQL Managed Instance) no Azure.
*   Habilidade para documentar processos técnicos de maneira clara, concisa e estruturada.
*   Proficiência na utilização do GitHub como ferramenta para versionamento, colaboração e compartilhamento de documentação técnica.
*   Compreensão das considerações de segurança para instâncias de banco de dados no Azure, incluindo configuração de rede e regras de firewall.

---

## Passos para a Criação da Instância de Banco de Dados (Azure SQL Managed Instance):

Este guia resume os passos para criar uma instância gerenciada de SQL no Azure. Consulte a documentação oficial para obter informações mais detalhadas.

1.  **Acesso ao Portal Azure:**  Acesse o portal do Azure em [https://portal.azure.com/](https://portal.azure.com/) e faça login com sua conta.

2.  **Criação do Grupo de Recursos (Resource Group):**
    *   Pesquise por "Resource groups".
    *   Clique em "Create".
    *   Preencha:
        *   **Subscription:** Sua assinatura.
        *   **Resource group name:** Um nome descritivo (ex: `rg-sql-instance-dio`).
        *   **Region:** A região desejada (ex: `Brazil South`).
    *   Clique em "Review + create" e "Create".

3.  **Criação da Instância Gerenciada de SQL (SQL Managed Instance):**
    *   Pesquise por "SQL managed instances".
    *   Clique em "Create".
    *   Preencha (atenção aos custos!):
        *   **Subscription:** Sua assinatura.
        *   **Resource group:** O grupo criado no passo anterior.
        *   **Managed instance name:** Um nome único (ex: `sql-instance-dio`).
        *   **Region:** A mesma região do grupo de recursos.
        *   **Compute + storage:** Selecione uma configuração adequada para testes, considerando os custos (comece com opções mais baratas e dimensione depois).
        *   **Configure network:**
            *   **IMPORTANTE:** Configure a rede virtual para acesso.  Crie uma nova rede virtual e sub-rede (anote os nomes!).
            *   **IMPORTANTE:** A sub-rede deve ser delegada para `Microsoft.Sql/managedInstances`.
        *   **Admin account:** Crie um usuário administrador com uma senha forte.
        *   **Tags:** Adicione tags (opcional).
    *   Clique em "Review + create" e "Create".  Aguarde a implantação (pode demorar!).

4.  **Configuração de Rede (Acesso à Instância):**
    *   **Após a criação:** Acesse a instância no portal.
    *   **Rede Virtual:** Verifique a configuração da rede virtual e sub-rede.
    *   **Regras de Segurança de Rede (NSG):**
        *   **IMPORTANTE:** Configure o NSG da sub-rede para permitir o tráfego na porta 1433 (ou a porta configurada) do seu IP de origem.
        *   Adicione uma regra de entrada que permita o tráfego na porta 1433 vindo do seu endereço IP (ou faixa de IPs).
        *   Atualize a regra do NSG se seu IP for dinâmico e mudar.
    *   **Conectividade:**
        *   A instância está dentro da rede virtual.
        *   Conecte-se através de um servidor na mesma rede virtual ou por VPN (ou ExpressRoute).

5.  **Criação de um Banco de Dados (opcional):**
    *   Na instância, guia "Databases", clique em "New database".
    *   Defina o nome e as opções.
    *   Clique em "Create".

6.  **Considerações de Segurança:**
    *   **Firewall:** Configure regras no firewall da instância.
    *   **Autenticação:** Use a autenticação do Azure Active Directory (Azure AD) sempre que possível.
    *   **Auditoria:** Habilite a auditoria para monitorar atividades.
    *   **Criptografia:** Considere criptografia de dados em repouso e em trânsito.

7.  **Monitoramento:**
    *   Use as ferramentas de monitoramento do Azure para acompanhar o desempenho e a saúde da instância.
    *   Configure alertas para problemas.

---

## Conclusão:

Este repositório resume minha experiência na configuração de uma instância de Banco de Dados (SQL Managed Instance) no Azure.  O desafio me permitiu aplicar os conhecimentos teóricos, documentar o processo e criar um recurso valioso para futuras referências.

**Próximos Passos:**

*   Explorar recursos avançados do Azure SQL Managed Instance (backup/restore, replicação, etc.).
*   Estudar otimização de desempenho.
*   Praticar backups automáticos.
*   Automatizar a implantação com Azure CLI ou Terraform.

---

## Recursos Adicionais:

*   **Documentação Oficial Microsoft Azure:** [https://learn.microsoft.com/pt-br/azure/](https://learn.microsoft.com/pt-br/azure/)
*   **Início Rápido: criar Instância Gerenciada de SQL do Azure - Artigo no Microsoft Learning:** [https://learn.microsoft.com/pt-br/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql](https://learn.microsoft.com/pt-br/azure/azure-sql/managed-instance/instance-create-quickstart?view=azuresql)
*   **GitHub Quick Start - Repositório com Link para Aulas de Git e GitHub:** [https://github.com/digitalinnovationone/bootcamp-everis-cloud](https://github.com/digitalinnovationone/bootcamp-everis-cloud)
*   **GitBook: Formação GitHub Certification - Material textual sobre GitHub:** [https://www.gitbook.com/book/digitalinnovationone/formacao-github-certification/details](https://www.gitbook.com/book/digitalinnovationone/formacao-github-certification/details)
*   **Documentação do GitHub - Guia completo para uso do GitHub:** [https://docs.github.com/](https://docs.github.com/)
*   **GitHub Markdown - Guia específico para Markdown no GitHub:** [https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

---

## Anexos (Imagens - Opcional):

Se você criou a pasta `/images`, liste aqui as imagens com uma breve descrição:

*   `/images/01_portal_azure.png`: Captura de tela da interface do portal Azure.
*   `/images/02_create_resource_group.png`: Captura de tela do processo de criação do grupo de recursos.
*   `/images/03_sql_instance_creation.png`: Captura de tela da criação da instância SQL Managed Instance.
*   `/images/04_network_configuration.png`: Captura de tela da configuração da rede virtual.
*   `/images/05_ssms_connection.png`: Captura de tela da conexão com o SQL Server Management Studio (SSMS).

---

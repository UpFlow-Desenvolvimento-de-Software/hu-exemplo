![enter image description here](https://upflowme-my.sharepoint.com/:i:/g/personal/sergio_silva_upflow_me/IQD3MyNd5MCUQotN40etfFkPAc5Wh7ZMhxPi30LhmrYEMqM?e=ZxqmBn)

### 1. Descrição do Problema
É necessário acrescentar um novo formulário para registros de informações sobre o exame de **HPV**, porém, esta funcionalidade deveria ser implementada no conjunto de features do **e-SUS**, porém, como o processo de solicitação de desenvolvimento de recurso neste projeto necessita de um processo burocrático e que demoraria mais tempo, a Gerência de Desenvolvimento da **SES-DF** recebeu a missão de implementar este formulário de forma rápida e que não necessitasse salvar estes dados em nenhum stored ou base de dados, apenas preencher este formulário para que estes dados possam ser replicados para o **GAL** e resolver a questão dos dados do exame de coleta de material do colo do útero para **HPV** e guardar estes dados do paciente do sistema público.

### 2. Objetivo da Feature / Funcionalidade
Criação de uma extensão para o browser (google chrome e outros) com o objetivo de habilitar os campos do formulário caso a opção *COLETA DE MATERIAL DO COLO DO ÚTERO PARA EXAME MOLECULAR DE DETECÇÃO DE HPV* seja selecionada como sim.

  
Para habilitar os campos contidos no documento `SEI_196492454_Formulario_para_Solicitacao_de_Desenvolvimento_de_Sistemas_de_Informacao___SES_7.pdf` para preenchimento do profissional de saúde.

### 2. Gherkin (para o BDD)
**COMO** usuário com perfil de profissional de saúde do gov.br para acesso da plataforma Saude-Certa

**GOSTARIA** preencher as informações sobre COLETA DE MATERIAL DO COLO DO ÚTERO PARA EXAME MOLECULAR DE DETECÇÃO DE HPV

**PARA** que estas informações possam ser copiadas e replicadas no formulário do e-SUS com informações equivalentes.


### 4. Regras de Negócios
|  **Código**  |  **Descrição**  |
|      --      |--|
| **RN 1** | As informações preenchidas no formulário não serão salvas em nenhuma base de dados ou stored. |
| **RN 2** | É necessário que o usuário que irá preencher o formulário, tenha um perfil de profissional de saúde devidamente registrado na plataforma `[gov.br](https://www.gov.br/pt-br)` |
| **RN 3** | O profissional que preencherá o formulário deverá ter um perfil devidamente cadastrado na plataforma `[Saúde-Certa](https://estadiamentodengue.saude.df.gov.br/)` |
| **RN 4** | O formulário deverá ser criado como um novo tipo de formulário destinado a exame de HPV |
| **RN 5** | O uso da ferramenta está estritamente vinculado ao registro dos procedimentos de coleta (`0201020076`) ou exame molecular de HPV (`0202100251`). |
| **RN 6** | A ferramenta não substitui o prontuário oficial, servindo apenas como suporte para evitar retrabalho e padronizar dados. |
| **RN 7** | Os dados devem ser obrigatoriamente vinculados ao cidadão, atendimento/episódio, profissional, unidade e ao procedimento disparador. |

### 5. Requisitos Funcionais (RF)
| Código | Descrição                                                                                                               |
| ------ | ----------------------------------------------------------------------------------------------------------------------- |
| **RF01**   | O sistema deve permitir a captura dos dados não estruturados ou insuficientes no prontuário eletrônico (PEC e-SUS APS). |
| **RF02**   | O sistema deve possibilitar o preenchimento das informações contidas no documento em anexo através de um formulário.    |
| **RF03**   | O sistema deve descartar os dados do formulário quando a sessão for finalizada ou fechada.                              |
| **RF04**   | O sistema deve emitir um alerta avisando que aqueles dados do paciente que foram preenchidos serão perdidos.            |


### 6. Requisitos Não-Funcionais (RNF)
| Código | Tipo      | Descrição                                                                                        |
| ------ | --------- | ------------------------------------------------------------------------------------------------ |
| RNF01  | Segurança | Os dados do formulário do paciente devem ser protegidos pela LGPD.                               |
| RNF02  | Segurança | Somente um profissional com perfil de saúde no gov.br pode registrar as informações do paciente. |


### 7. Critérios de Aceitação (CA)
- [ ] **CA 1:** Os dados preenchidos no formulário do [SAÚDE-CERTA](https://estadiamentodengue.saude.df.gov.br/) deverão oferecer a opção de copiar os dados do formulário preenchido em texto plano (`.txt`) para replicação no **GAL** com um botão (COPIAR DADOS)
   - [ ] **CA 1.1:** Quando os botões de VOLTAR e LIMPAR forem acionados e existirem dados no formulário, avisar ao usuário que as informações serão perdidas.
      - [ ] **CA 1.1.1:** Botão [VOLTAR] - Mensagem: “Deseja apagar os dados do seu formulário? As informações serão permanentemente perdidas”.
      - [ ] **CA 1.1.2:** Botão [LIMPAR] - Mensagem: “Deseja apagar os dados do seu formulário? As informações serão permanentemente perdidas”.
   - [ ] **CA 1.2:** O botão VOLTAR servirá para voltar à tela anteriormente visitada.
   - [ ] **CA 1.3:** O botão LIMPAR servirá para efetuar a remoção dos dados preenchidos no formulário.
- [ ] **CA 2:** Os dados capturados devem ser suficientes para preencher os requisitos do GAL.
- [ ] **CA 3:** Os campos do formulário terá a seguinte estrutura:
   - [ ] **CA 3.1:** Fez exame preventivo anteriormente?<br>
         **Tipo do Campo:** `Radio Button` (Seleção Binária)<br>
         **Valores:** `Sim / Não / Não Sabe`<br><br>
         Se o valor for **Sim**:<br>
         Mostrar um `campo de texto livre` para informar a data do exame.<br>
- [ ] **CA 3.2:** Usa DIU?<br>
      **Tipo do Campo:** `Radio Button` (Seleção Binária)<br>
      **Valores:** `Sim / Não / Não Sabe`<br>


### 8. Legislação
#### 8.1. Garantia de Atendimento à Saúde

O direito de ser atendido é um pilar fundamental da cidadania brasileira:

-   **Constituição Federal (Art. 196):** Define a saúde como um "direito de todos e dever do Estado", garantindo acesso universal e igualitário.
    
-   **Lei Orgânica do Distrito Federal (LODF):** Em seu **Artigo 204**, reforça que a saúde é direito de todos e dever do DF, devendo ser garantida mediante políticas sociais e econômicas.
    
-   **Lei Federal nº 8.080/1990 (Lei do SUS):** Regula as ações de saúde em todo o país e estabelece os princípios de universalidade (atendimento para todos) e integralidade (atendimento completo).
    
-   **Carta dos Direitos dos Usuários da Saúde:** Uma portaria que detalha o direito ao atendimento digno, humanizado e livre de discriminação.

#### 8.2. Proteção de Dados e Privacidade

Seus prontuários, exames e histórico médico são considerados **dados sensíveis**, o que exige uma proteção rigorosa:

-   **Lei Geral de Proteção de Dados - LGPD (Lei nº 13.709/2018):** É a lei principal. Ela classifica informações sobre saúde como "dados sensíveis" (Art. 5º) e exige cuidados extras no tratamento dessas informações por hospitais, clínicas e pelo governo.
    
-   **Decreto Distrital nº 42.036/2021:** Este decreto regulamenta a aplicação da LGPD especificamente dentro dos órgãos da administração pública do **Distrito Federal**, incluindo a Secretaria de Saúde do DF.
    
-   **Constituição Federal (Art. 5º, LXXIX):** Incluído recentemente, este inciso eleva a proteção de dados pessoais à categoria de **direito fundamental**.
    
-   **Código de Ética Médica:** Proíbe o médico de revelar informações sobre o paciente sem consentimento, garantindo o sigilo profissional (salvo em casos específicos previstos em lei).

### 9. Comportamento no Produto
Assim que ativada a extensão, o SAÚDE-CERTA habilitará os campos do formulário de EXAME MOLECULAR DE DETECÇÃO DE HPV com os campos descritos nos critérios de aceitação (CA 3).

### 10. Impactos Técnicos

### 11. Informações de Banco de Dados

### 12. APIs Relacionadas

### 13. Integrações ou Consultas a Aplicações de Terceiros

### 14. Atividade de Negócio

### 15. Protótipo

### 16. Fórmulas / Cálculos

### 17. Documentos Relacionados

### 18. Ratreabilidade Parcial de RN x RF

### 19. Processo de Instalação de Extensão

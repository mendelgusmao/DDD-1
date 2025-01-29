# Dinâmica: Design Estratégico do Projeto

## Objetivo
Identificar os subdomínios do projeto, classificá-los (Core, Supporting, Generic) e desenhar os bounded contexts, incluindo suas interações. Esse exercício ajudará a criar uma visão clara e estratégica do domínio.

---

## 1. Nome do Projeto
**Revolucionando o Acesso a Saúde**

---

## 2. Objetivo Principal do Projeto
**[Explique o propósito do sistema em uma ou duas frases]**  
*Exemplo:* Diminuir a fricção nos cuidados de saúde e tratamentos.

---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio**         | **Descrição**                                                                                   | **Tipo**         |
|------------------------|-------------------------------------------------------------------------------------------------|------------------|
| Gestão de Consultas    | Gerencia o agendamento, consulta por vídeo e emissão de atestados e receitas.                   | Core Domain      |
| Gestão de Exames       | Gerencia os exames, tanto os anteriores às consultas como os pós-consulta                       | Core Domain      |
| Controle de Medicações | Realiza e acompanha compras de medicações                                                       | Core Domain      |
| Cadastro de Usuários   | Gerencia o login, cadastro e permissões dos médicos e pacientes.                                | Supporting       |
| Cadastro de Medicações | Gerencia o cadastro de medicações disponíveis.                                                  | Supporting       |
| Prontuário             | Armazena informações de consultas, exames, medicações e tratamentos do paciente                 | Supporting       |
| Pagamentos             | Processa pagamentos e repassa valores para médicos, farmácias, clínicas e laboratórios.         | Generic          |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context**           | **Responsabilidade**                                                                                | **Subdomínios Relacionados** |
|-------------------------------|-----------------------------------------------------------------------------------------------------|------------------------------|
| Contexto de Consultas         | Gerencia as consultas médicas, do agendamento à finalização, incluindo emissão de receitas.      | Gestão de Consultas             |
| Contexto de Exames            | Gerencia os pedidos de exames e faz acompanhamento com os laboratórios.                          | Gestão de Exames                |
| Contexto de Pagamentos        | Processa cobranças de consultas, repasses para médicos ou clínicas, exames e medicações.         | Pagamentos                      |
| Contexto de Medicações        | Cadastra medicamentos, processa pedidos de medicações, acompanha pedidos                         | Controle de Medicações           |
|                               |                                                                                                  | Cadastro de Medicações           |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)**              | **Para (Destino)**          | **Forma de Comunicação**    | **Exemplo de Evento/Chamada**                 |
|------------------------------|-----------------------------|-----------------------------|-----------------------------------------------|
| Contexto de Consultas        | Contexto de Pagamentos      | Mensageria (Evento)         | "Consulta Finalizada"                         |
| Contexto de Consultas        | Contexto de Exames          | Mensageria (Evento)         | "Solicitação de pré-exame"                    |
| Contexto de Consultas        | Contexto de Medicações      | Mensageria (Evento)         | "Receita emitida"                             |
| Contexto de Exames           | Contexto de Pagamentos      | Mensageria (Evento)         | "Exame finalizado"                            |
| Contexto de Cadastro         | Contexto de Consultas       | API                         | Obter informações de um Paciente pelo ID      |
| Contexto de Cadastro         | Contexto de Exames          | API                         | Obter exames de um Paciente pelo ID           |
| Contexto de Cadastro         | Contexto de Medicações      | API                         | Obter receitas de um Paciente pelo ID         |
| Contexto de Cadastro         | Contexto de Pagamentos      | API                         | Obter informação de pagamento de um Paciente pelo ID         |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Consulta                     | Sessão médica entre paciente e médico.                                                       |
| Paciente                     | Usuário que agenda e realiza consultas.                                                      |
| Receita                      | Prescrição médica gerada durante a consulta.                                                 |
| Medicamento                  | Medicamento que faz parte de uma prescrição.                                                 |
| Exame                        | Procedimento de investigação de saúde .                                                      |
| Cadastro de Usuário                     | Registro de um usuário no sistema.                                                           |
| Cadastro de Medicamento                     | Registro de um medicamento no sistema.                                                           |
| Médico                       | Usuário que realiza avaliação com um usuário paciente.                                                 |
| Clínica                       | Local segmentado ao atendimento do usuário paciente com um conjunto de médicos disponíveis.                                                 |
| Laboratório                       | Local segmentado onde se realizam exames                                                 |
| Farmácia                       | Local segmentado onde são distribuídos medicamentos.                                                 |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|---------------------------------------|-------------------------------------------|
| Gestão de Consultas         | Desenvolvimento interno               |                                           |
| Gestão de Exames            | Desenvolvimento interno               |                                           |
| Cadastro de Usuários        | Interno com uso de Auth0 para login   | Auth0                                     |
| Pagamentos                  | Terceirizar usando API Stripe         | Stripe                                    |

---

## 8. Diagrama Visual (Opcional, mas Recomendado)
Desenhe um diagrama que mostre:
- Os bounded contexts.
- Como eles se comunicam.
- A relação com os subdomínios.

Use ferramentas como **Miro**, **Lucidchart** ou mesmo papel e caneta para criar seu diagrama e adicionar ao projeto.

---

## Dicas para Apresentação
- Explique cada parte do design, focando no **Core Domain** (o coração do negócio).
- Justifique por que certos subdomínios foram classificados como Supporting ou Generic.
- Destaque como a comunicação entre bounded contexts foi pensada para ser escalável.

---

Boa sorte com a dinâmica! 🚀

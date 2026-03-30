# Integração Salesforce + ViaCEP (Flow Assíncrono) 🚀

Projeto desenvolvido para a **Clínica FisioCare** com o objetivo de automatizar o preenchimento de endereços de pacientes, reduzindo erros de digitação e otimizando o tempo de cadastro.

## 📌 O Problema
O cadastro manual de endereços gerava inconsistências nos dados e tomava tempo excessivo da equipe de recepção. Era necessária uma solução que buscasse os dados automaticamente a partir do CEP.

## 🛠️ Solução Técnica
Utilizei o **Salesforce Flow Builder** com um caminho **Assíncrono (Run Asynchronously)** para realizar chamadas externas (HTTP Callout) sem travar a interface do usuário.

### Destaques da Implementação:
* **External Services:** Configuração do Schema JSON para consumo da API ViaCEP.
* **Lógica de Gatilho Híbrida:** Configuração de critérios de entrada personalizados (`OR`) usando os operadores `Is Changed` e `Is Null` para garantir que a automação dispare tanto na **criação** quanto na **edição** do registro.
* **Performance:** Uso de processamento assíncrono para evitar erros de limite de tempo (Timeouts) e garantir uma melhor UX.
* **Data Quality:** Implementação de filtros para evitar loops de recursividade no banco de dados.

## 🚀 Como funciona
1. O usuário insere ou altera o campo `CEP__c` no objeto `Paciente__c`.
2. O Flow valida se o campo não está nulo e se houve alteração.
3. Uma Action de **HTTP Callout** envia o CEP para a API `https://viacep.com.br/ws/{cep}/json/`.
4. O retorno (Logradouro, Bairro, Localidade) é mapeado e atualiza o registro do Paciente automaticamente.

## 📸 Evidência
<img width="735" height="477" alt="image" src="https://github.com/user-attachments/assets/c3ca02a7-2509-46aa-9969-117a13f22161" />


---
**Desenvolvido por Luiz Felipe** *Salesforce Administrator Junior II | Estudante de Análise e Desenvolvimento de Sistemas (ADS)*

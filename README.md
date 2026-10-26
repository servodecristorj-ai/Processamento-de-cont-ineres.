# Análise Forense e Segurança em Processamento de Contêineres Aninhados em LLM de Grande Escala

Este repositório apresenta um estudo de caso técnico e uma Prova de Conceito (PoC) focada no parsing de arquivos binários, inspeção de *magic bytes* e validação de segurança na extração de contêineres aninhados em um **Ambiente de LLM de Grande Escala**.

## 📌 Escopo e Objetivos
* **Inspeção de Binários:** Identificação e descompactação recursiva de arquivos com assinaturas ausentes ou divergentes (ex.: extensões não reconhecidas nativamente contendo pacotes `.zip` encadeados).
* **Análise de Engenharia:** Avaliação do comportamento da aplicação durante a leitura de fluxos de dados desconhecidos em ambiente isolado (*sandbox*).
* **Avaliação de Segurança:** Análise conceitual da resistência a ataques de *Path Traversal* (*Zip Slip*) e manipulação de diretórios em rotinas de extração de arquivos.

## 🛠️ Metodologia Aplicada
1. **Inspeção por Magic Bytes:** Identificação das assinaturas dos arquivos nos primeiros *bytes* do cabeçalho (`PK\x03\x04`), contornando limitações de reconhecimento superficial por extensão.
2. **Extração e Desaninhamento Recursivo:** Processamento de contêineres complexos contendo estruturas compactadas encadeadas.
3. **Análise de Validação de Caminho:** Avaliação das travas do sistema operacional e da aplicação. Em cenários robustos, o bloqueio do caractere de separação de diretório (`/`) impede a navegação para fora do diretório de destino.

## 🛡️ Considerações de Segurança (Zip Slip & Path Traversal)
Embora rotinas de extração de arquivos possam ser vulneráveis ao ataque *Zip Slip* quando extraem caminhos arbitrários sem higienização, a implementação testada demonstrou defesas efetivas ao restringir caracteres especiais de navegação (`/` e `\`), garantindo a escrita apenas no diretório temporário pretendido.

## 📄 Licença e Uso Ético
Este material possui fins exclusivamente educacionais, de pesquisa em cibersegurança e demonstração de competências técnicas em auditoria e engenharia de software.

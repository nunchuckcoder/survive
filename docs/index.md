---
title: Política de Privacidade — SURVIVE
---

# Política de Privacidade — SURVIVE

[Português](./) · [English](./en/) · [Suporte](./support/) · [Eliminar dados](./delete-data/)

**Última atualização:** 28 de agosto de 2026  
**Responsável:** Osvaldo Cipriano (NunchuckCoder)  
**Contacto:** [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

Esta política explica de forma transparente como a aplicação Android **SURVIVE** trata os dados no dispositivo.

## 1. Responsável e âmbito

A SURVIVE é desenvolvida por Osvaldo Cipriano (NunchuckCoder). A aplicação funciona localmente no dispositivo Android e o programador não recebe nem mantém uma base de dados com os dados introduzidos na aplicação.

## 2. Dados guardados no dispositivo

A aplicação pode guardar localmente:

- primeiro e último nome e email do perfil;
- um derivado criptográfico da password, salt, algoritmo e número de iterações;
- dados do agregado familiar, incluindo nome, avatar, idade, sexo usado nos cálculos, peso, altura e atividade;
- produtos da despensa, quantidades, unidades, categorias, datas de compra e validade, informação nutricional, notas e histórico de consumos;
- medicamentos armazenados, incluindo nome comercial/dosagem introduzida, categoria, quantidade, unidade, data de compra, validade e notas; esta informação pode constituir dados de saúde;
- mochilas, atribuições aos membros do agregado, categorias, itens, prioridades, peso e estado da checklist;
- tema, antecedência configurada para os alertas e estado das notificações já apresentadas.

Estes dados são usados exclusivamente para disponibilizar as funcionalidades da SURVIVE no próprio equipamento.

A área **Medicamentos** serve apenas para controlar o stock e o prazo de validade de medicamentos armazenados. Não presta aconselhamento médico ou farmacêutico, não efetua diagnósticos ou prescrições e não cria lembretes nem instruções de toma.

## 3. Password e segurança local

A password não é guardada em texto simples. É guardado localmente um derivado criptográfico com salt e número de iterações.

A password bloqueia o acesso através da interface da aplicação, mas a base de dados Room **não é cifrada pela password**. A aplicação usa o armazenamento privado do Android, desativa as cópias automáticas do sistema e não envia credenciais para qualquer servidor.

## 4. Notificações e permissões Android

Se forem autorizadas, as notificações avisam sobre produtos e medicamentos próximos da validade. Conforme as definições de privacidade do Android, uma notificação de alimento pode mostrar o nome do produto no ecrã bloqueado. As notificações de medicamentos são genéricas: não mostram o nome do medicamento; esse detalhe fica apenas dentro da aplicação autenticada.

A aplicação utiliza apenas:

- **Notificações:** autorização opcional para apresentar os avisos de validade;
- **Arranque concluído:** permite repor a verificação diária depois de reiniciar ou atualizar o dispositivo.

A SURVIVE não pede acesso à localização, contactos, câmara, microfone, SMS ou armazenamento geral do dispositivo.

## 5. Cópias de segurança

A exportação só acontece quando o utilizador escolhe criar uma cópia através do seletor de ficheiros Android. O ficheiro JSON exportado:

- não inclui a password, o respetivo hash ou o salt;
- pode incluir os restantes dados do perfil, agregado, despensa, medicamentos, histórico e mochilas;
- não é cifrado pela aplicação.

O local escolhido e qualquer partilha posterior do ficheiro ficam sob controlo e responsabilidade do utilizador. Como a cópia pode conter informação sobre medicamentos, deve ser guardada num local privado. O restauro lê apenas o ficheiro que o utilizador selecionar explicitamente.

## 6. Internet, terceiros e publicidade

A SURVIVE:

- não possui permissão de Internet;
- não usa WebView, APIs remotas ou contas online;
- não contém publicidade ou analytics;
- não utiliza SDKs destinados a recolher dados;
- não vende, partilha ou transmite dados ao programador ou a terceiros.

## 7. Conservação e eliminação

Os dados permanecem no dispositivo até serem alterados ou eliminados pelo utilizador.

A opção **Perfil → Eliminar o meu perfil** apaga o perfil e os dados associados. Também é possível eliminar todos os dados através das definições Android ou desinstalando a aplicação.

Os ficheiros de cópia de segurança anteriormente exportados não são controlados pela aplicação e devem ser eliminados separadamente no local onde foram guardados.

## 8. Dados de menores

A SURVIVE não é dirigida a crianças. Um adulto pode introduzir localmente dados de membros menores do agregado para obter estimativas de planeamento. Esses dados não saem do dispositivo nem são recolhidos pelo programador.

## 9. Alterações à política

Esta política pode ser atualizada quando as funcionalidades da aplicação ou os requisitos aplicáveis mudarem. A versão publicada apresentará sempre a data da última atualização.

## 10. Contacto

Para questões relacionadas com esta política ou com a privacidade na SURVIVE:

**Email:** [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

---

A SURVIVE é uma aplicação independente de planeamento familiar e não representa qualquer organismo público, serviço de emergência ou entidade médica.

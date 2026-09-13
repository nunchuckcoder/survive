# SURVIVE para Android

[Português](README.md) · [English](README.en.md)

Aplicação Android nativa e autónoma. Não contém WebView, não abre o site para executar funções e não depende de PHP, MySQL, API ou Internet.

Versão pública do projeto: **1.0** (`versionName "1.0"`) em `debug` e `release`. O código interno de atualização é **2** (`versionCode 2`), permitindo substituir na Google Play a compilação anterior sem alterar a versão apresentada ao público.

A base Room usa agora a versão interna **6** para migrar instalações anteriores sem perda de dados, indexar a ligação das mochilas ao agregado, distinguir alimentos de medicamentos e guardar o peso de cada unidade. Este número é independente do `versionCode` da Google Play e da versão pública da aplicação, que continua a ser **1.0**.

## Arquitetura

- Kotlin e Jetpack Compose com Material 3.
- Room como base de dados local e única fonte de verdade.
- Um único perfil local, com nome, email e password editáveis.
- Passwords derivadas pela implementação nativa PBKDF2/HMAC-SHA-256, com salt aleatório, algoritmo/iterações guardados e comparação em tempo constante. Os hashes anteriores são atualizados depois de uma autenticação válida.
- Exportação e restauro de dados em JSON através do seletor de ficheiros do Android.
- Sem permissão `INTERNET`, publicidade, analytics, localização, câmara, microfone ou contactos. As únicas permissões funcionais são notificações e reposição do verificador diário depois de reiniciar o telemóvel.
- `minSdk 26`, `targetSdk 36`, `compileSdk 37` e JDK 17.

## Funcionalidades

- Identidade visual com o novo símbolo fornecido: versão teal sobre fundo branco no launcher/arranque/autenticação e menu claro; no menu escuro o símbolo é integralmente branco e transparente no restante espaço.
- Resumo com duração normal e por três fases de racionamento, calorias, macronutrientes, água e prontidão das mochilas.
- Despensa com pesquisa e filtros fixos, quatro indicadores no início da lista deslocável, categorias predefinidas em dropdown, calorias automáticas calculadas pelos macronutrientes, nutrição completa, marca explícita de reserva de água, validades escolhidas num calendário, utilização de stock e histórico. “Latas” deixou de ser uma unidade selecionável; quando se escolhe “unidades”, o formulário pede o peso de cada unidade em gramas e usa `quantidade × peso por unidade` nos totais nutricionais. Os cinco consumos recentes são consultados separadamente; “Ver histórico” carrega a lista completa agrupada por dia e permite limpá-la apenas depois de confirmação. Registos com nome normalizado, unidade e categoria iguais aparecem agrupados por produto, mantendo cada lote independente; um lote único mostra logo datas, notas e ações, enquanto vários lotes expandem e permitem consumo pela validade mais próxima, inclusive atravessando vários lotes numa única operação.
- Medicamentos num menu autónomo abaixo da Despensa, com pesquisa, categorias e unidades próprias, stock e validade escolhida num calendário. Um único lote mostra diretamente datas, notas e ações; lotes equivalentes aparecem num cartão expansível para editar ou eliminar cada registo. Esta área não entra nos cálculos nutricionais, não cria lembretes de toma e mostra um aviso explícito de que não substitui aconselhamento médico ou farmacêutico.
- Agregado criado com o Perfil; permite homem, mulher, rapaz, rapariga, cão e gato, com cálculos próprios para adultos e para crianças/adolescentes dos 3 aos 18 anos. As linhas de racionamento e os restantes pares rótulo/valor adaptam-se a ecrãs estreitos e a letra grande, colocando o valor numa segunda linha quando necessário sem o dividir por caracteres.
- Mochilas múltiplas, sempre acrescentadas no fim, com estado vazio corretamente posicionado abaixo da barra superior, categorias reordenáveis por pressão prolongada e arrasto, categorias recolhidas por defeito, instrução visível do gesto, edição à esquerda/eliminação à direita para categorias e itens, prioridades, checklist, peso e atribuição por UUID a um membro escolhido no dropdown.
- Formulários, filtros e diálogos essenciais sobrevivem à rotação; o gesto Voltar regressa ao Resumo a partir dos restantes separadores.
- Migração local não destrutiva para abrir corretamente dados criados por qualquer uma das variantes 1.0 anteriores.
- Alertas locais de validade, água, alimentos, medicamentos e itens críticos, com antecedência do aviso “A expirar” configurável. Cada produto ou medicamento pode gerar três notificações únicas: ao ativar o alerta, a meio desse período e cinco dias antes da validade. As notificações de medicamentos são genéricas e não expõem o nome no ecrã bloqueado.
- Perfil local, login, alteração de nome/email/password e seleção de tema Sistema, Claro ou Escuro no próprio dispositivo. No registo, os campos começam neutros, passam a verde apenas quando válidos e a vermelho somente depois de existir conteúdo inválido; os requisitos da password permanecem sempre visíveis.
- Interface integral em PT-PT e inglês. No primeiro arranque segue o idioma do Android (com PT-PT como fallback para idiomas não suportados); a seleção pelas bandeiras fica persistente e também aparece nas definições de idioma da aplicação no Android 13 ou superior.
- Cartões, caixas, campos, menus, popups, botões, navegação lateral e barras de progresso com linguagem visual reta. Os fundos, boxes e superfícies elevadas têm níveis de cor distintos e texto de alto contraste nos temas Claro e Escuro; ações irreversíveis de eliminação aparecem a vermelho.
- Política de privacidade completa consultável offline no Perfil e pronta para publicação através de GitHub Pages na pasta `docs/`.
- Cópia de segurança e restauro dos dados do perfil.

## Compilar

Abre a pasta no Android Studio atualizado ou usa:

```bash
./gradlew test lint connectedDebugAndroidTest assembleDebug
```

Para uma compilação pública assinada:

```bash
./gradlew clean test lint bundleRelease \
  -PSURVIVE_STORE_FILE=/caminho/privado/upload.jks \
  -PSURVIVE_STORE_PASSWORD='...' \
  -PSURVIVE_KEY_ALIAS='upload' \
  -PSURVIVE_KEY_PASSWORD='...'
```

O AAB fica em `app/build/outputs/bundle/release/`. Não guardes keystores, passwords ou `local.properties` no repositório.

Também podes usar **Build → Generate Signed App Bundle or APK** no Android Studio. Seleciona o ficheiro da chave que criaste e introduz exatamente o respetivo alias e passwords. A chave e as credenciais não estão incluídas neste projeto.

## Política de privacidade

A política completa está em português em `docs/index.md`, em inglês em `docs/en/index.md`, e também pode ser consultada nos dois idiomas dentro da aplicação em **Perfil → Consultar política de privacidade**. A versão integrada é nativa em Compose, funciona offline e não utiliza WebView. A pasta pública inclui ainda `docs/support/index.md`, com instruções de suporte, e `docs/delete-data/index.md`, com os passos para eliminar localmente o perfil e os respetivos dados.

Para a publicar da mesma forma que na Prevenção PT:

1. coloca o projeto num repositório público do GitHub;
2. abre **Settings → Pages**;
3. escolhe **Deploy from a branch**, a branch `main` e a pasta `/docs`;
4. depois da publicação, introduz o URL gerado no campo **Política de privacidade** da Play Console.

Se o repositório se chamar `survive`, o endereço esperado será `https://nunchuckcoder.github.io/survive/`. Se tiver outro nome, o caminho do URL muda para esse nome. Confirma que a página abre publicamente antes de submeter a aplicação.

## Testes obrigatórios antes da Google Play

- Executar `test`, `lint` e `bundleRelease` sem erros.
- Testar criação, edição e eliminação em todas as áreas com modo de avião ativo desde o primeiro arranque.
- Testar criação do perfil único, alteração do email, password incorreta, mudança de password e eliminação do perfil.
- Exportar uma cópia, alterar dados, restaurá-la e verificar todas as relações entre mochila/categoria/item.
- Criar várias mochilas e confirmar que a nova fica no fim; mover categorias, fechar a app e confirmar que a ordem foi preservada.
- Marcar e desmarcar itens de uma mochila e confirmar que os concluídos ficam riscados e mantêm um tamanho de texto legível.
- Manter uma categoria premida e arrastá-la verticalmente, fechar a app e confirmar que a nova ordem fica preservada.
- Deslizar parcialmente uma categoria/item e voltar atrás, confirmando que nenhuma ação abre; completar o deslize uma vez e confirmar que o editor/diálogo abre uma única vez. Para eliminar, confirmar que os dados só desaparecem depois de aceitar o diálogo.
- Inserir proteína, hidratos e gordura num produto e confirmar que as kcal são atualizadas automaticamente pela fórmula 4/4/9 e aparecem corretamente na lista.
- Escolher “unidades” num produto, indicar 5 unidades de 400 g e confirmar que os totais nutricionais correspondem a 2000 g; confirmar também que “latas” já não aparece no seletor e que o peso por unidade é preservado ao editar, exportar e restaurar.
- Escolher, escrever e limpar as datas de compra/validade no seletor da Despensa e dos Medicamentos, alternar entre calendário e teclado, rodar o dispositivo com o seletor aberto e confirmar que os valores guardados continuam corretos em português e inglês.
- Escrever nas Notas e no Motivo caracteres como `ç`, `á`, `à`, `ã`, `â`, `é`, `ê`, `í`, `ó`, `ô`, `õ` e `ú`; guardar, reabrir e confirmar também após exportar/restaurar uma cópia.
- Abrir a política de privacidade no Perfil, percorrer todo o conteúdo e confirmar a legibilidade nos temas Claro e Escuro.
- Percorrer todos os ecrãs nos temas Claro e Escuro e confirmar que o fundo geral, as boxes, os popups e as superfícies elevadas são visualmente distintos; confirmar também que não existem botões em forma de comprimido nem pontas redondas nas barras lineares.
- Alternar várias vezes entre `🇵🇹 Português` e `🇬🇧 English`, reiniciar a aplicação e confirmar a tradução de todos os ecrãs, validações, notificações, diálogos (incluindo a confirmação “Limpar”), unidades e acessibilidade.
- Abrir a aplicação sem perfil e confirmar que a explicação apresenta apenas o armazenamento local/offline, sem referir o antigo site; repetir a verificação em **Perfil → Privacidade**.
- Com a interface em inglês, criar produtos/membros/mochilas/categorias/notas chamados `Água`, `Mulher`, `Gato`, `Arroz 5 dias` e `Cópia dos Documentos`; confirmar que estes dados permanecem exatamente como foram escritos.
- Autorizar notificações e confirmar, com um período de 60 dias, os três avisos únicos de cada produto: aos 60 dias, aos 30 dias e aos 5 dias da validade, incluindo depois de reiniciar o telemóvel.
- Criar um medicamento em cada unidade disponível, confirmar que aparece apenas em Medicamentos/Alertas, que nunca altera calorias ou sobrevivência e que as três notificações não mostram o seu nome fora da app.
- Registar dois lotes de `Arroz Agulha` com a mesma unidade/categoria e validades diferentes, confirmar que aparecem num único cartão expansível e que consumir mais do que o primeiro lote retira o restante do lote seguinte, deixando dois eventos no histórico.
- Registar um produto e um medicamento com apenas um lote e confirmar que compra, validade, notas e ações ficam visíveis sem expansão; confirmar também que todas as datas são apresentadas no formato do idioma da aplicação, embora continuem guardadas em ISO.
- Expandir um produto com dois lotes, eliminar ou consumir totalmente um deles e confirmar que o cartão passa ao modo de lote único sem conservar uma expansão invisível; repetir nos Medicamentos.
- Na Despensa, confirmar que apenas a pesquisa e os filtros permanecem fixos durante o scroll; abrir “Ver histórico”, verificar que o carregamento nunca apresenta falsamente “Sem consumos”, confirmar o agrupamento por dia, cancelar a confirmação de limpeza e confirmar depois que “Limpar histórico” remove os registos sem alterar o stock atual.
- Registar o mesmo alimento com unidade ou categoria diferente e confirmar que permanece num grupo separado; repetir o teste com duas caixas do mesmo medicamento e confirmar a expansão individual dos lotes.
- Alterar a data de validade de um produto já notificado e confirmar que a nova validade pode originar um novo aviso; editar apenas nome, quantidade ou notas não deve repetir a notificação.
- Confirmar os cálculos do agregado para adultos, crianças e adolescentes e que o racionamento só inclui adultos.
- Testar rotação, processo terminado, atualização da app, leitores de ecrã, letra grande, telemóveis pequenos e tablets.
- Terminar sessão e confirmar que nenhuma notificação apresenta nomes de produtos até existir nova autenticação; voltar a entrar e confirmar que os avisos já emitidos não se repetem.
- Atualizar uma instalação anterior e confirmar que as migrações internas `1 → 2 → 3 → 4 → 5 → 6` preservam todos os dados, classificam os produtos existentes como alimentos e acrescentam o peso opcional por unidade.
- Numa instalação antiga sem `profile_member_uuid`, confirmar que apenas uma correspondência única entre o nome do Perfil e o membro principal cria a ligação; vários membros ambíguos devem continuar editáveis e elimináveis.
- Criar vários membros e confirmar que aparecem pela ordem de criação; editar um membro não deve alterar a sua posição.
- Rever os cálculos e avisos com uma pessoa tecnicamente habilitada; não são aconselhamento médico ou de emergência.

O projeto fonte está preparado para compilação, mas um AAB só deve ser publicado depois destes testes em Android SDK e dispositivos reais.

Os esquemas Room `1.json` a `6.json` estão versionados em `app/schemas/pt.osvaldocipriano.survive.data.local.SurviveDatabase/`. Os históricos são reconstruções explícitas das variantes anteriormente distribuídas; o KSP deve voltar a exportar e validar o esquema atual durante a primeira build completa. A tarefa `connectedDebugAndroidTest` valida `1→3`, `2→3`, `3→4`, `4→5`, `5→6` e o percurso completo `1→6`, mas o teste autoritativo continua a ser instalar um APK anterior com dados reais e atualizar por cima com o novo APK. Mantém os JSON sob controlo de versões sem alterar a versão pública 1.0.

## Referências dos cálculos pediátricos

- National Academies, *Dietary Reference Intakes for Energy* (2023), tabela 5-15: equações por sexo, idade, peso, altura e atividade, incluindo o custo de crescimento.
- National Academies, tabelas DRI de macronutrientes e água: valores de referência de proteína e água por faixa etária e sexo.

As estimativas servem para planeamento geral. Necessidades individuais podem ser diferentes, sobretudo em doença, gravidez, alterações de peso ou atividade excecional.

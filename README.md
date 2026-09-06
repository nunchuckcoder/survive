<p align="center">
  <img src="assets/feature-graphic-pt.png" alt="SURVIVE — Prontidão Familiar" width="100%">
</p>

<p align="center">
  <strong>Planeia. Organiza. Prepara.</strong><br>
  Aplicação Android nativa para organizar a prontidão familiar, de forma privada e totalmente offline.
</p>

<p align="center">
  <a href="README.md">Português</a> · <a href="README.en.md">English</a>
</p>

# SURVIVE: Prontidão Familiar

SURVIVE reúne num único lugar a gestão da despensa, medicamentos armazenados, mochilas de emergência, agregado familiar e alertas de validade. A aplicação foi concebida para continuar disponível sem ligação à Internet e para manter os dados no dispositivo do utilizador.

> **Estado do projeto:** versão **1.0**, em preparação para testes fechados na Google Play.

## Funcionalidades

- **Resumo da preparação:** estimativas de autonomia alimentar, água disponível, prontidão das mochilas e alertas ativos.
- **Despensa por produtos e lotes:** quantidades, categorias, datas de compra e validade, informação nutricional e notas.
- **Rotação de stock por validade:** lotes equivalentes são agrupados e o consumo pode começar pelo que expira primeiro.
- **Cálculo nutricional:** calorias calculadas automaticamente a partir de proteína, hidratos e gordura, com totais de reservas.
- **Histórico de consumos:** consulta dos registos recentes ou do histórico completo, com opção de limpeza mediante confirmação.
- **Medicamentos armazenados:** controlo de stock e validade por lote, com categorias e unidades próprias.
- **Mochilas de emergência:** várias mochilas, atribuição a membros do agregado, categorias reorganizáveis, prioridades e checklists.
- **Agregado familiar:** estimativas indicativas de necessidades diárias e cenários de racionamento para planeamento.
- **Alertas locais:** antecedência configurável para produtos e medicamentos próximos da validade.
- **Personalização:** temas claro, escuro e do sistema, com interface em português e inglês.
- **Cópias de segurança:** exportação e restauro manual dos dados através de um ficheiro JSON.

## Capturas de ecrã

<table>
  <tr>
    <td align="center"><img src="assets/screenshots/01-resumo.png" alt="Resumo da prontidão" width="220"><br><strong>Resumo</strong></td>
    <td align="center"><img src="assets/screenshots/02-despensa.png" alt="Gestão da despensa" width="220"><br><strong>Despensa</strong></td>
    <td align="center"><img src="assets/screenshots/03-medicamentos.png" alt="Controlo de medicamentos armazenados" width="220"><br><strong>Medicamentos</strong></td>
    <td align="center"><img src="assets/screenshots/04-alertas.png" alt="Alertas locais" width="220"><br><strong>Alertas</strong></td>
  </tr>
</table>

## Privacidade por conceção

SURVIVE funciona integralmente no dispositivo:

- não possui permissão de Internet;
- não utiliza contas online, publicidade ou analytics;
- não envia dados pessoais, dados do agregado ou informação sobre medicamentos para o programador ou para terceiros;
- guarda a base de dados no armazenamento privado da aplicação;
- permite ao utilizador exportar e eliminar os seus próprios dados;
- apresenta notificações de medicamentos sem revelar o respetivo nome no ecrã bloqueado.

A password protege o acesso através da interface, mas a base de dados local não é cifrada pela password. Os backups JSON também não são cifrados e devem ser guardados num local privado.

Consulta a [Política de Privacidade](docs/index.md), a [versão inglesa](docs/en/index.md), o [Suporte](docs/support/index.md) e as [instruções para eliminação de dados](docs/delete-data/index.md).

## Avisos importantes

### Medicamentos

A área **Medicamentos** serve apenas para controlar o stock e o prazo de validade dos medicamentos armazenados. Não fornece aconselhamento médico ou farmacêutico, diagnóstico, prescrição, posologia, instruções ou lembretes de toma. A SURVIVE não é um dispositivo médico.

### Nutrição e preparação

As estimativas nutricionais, de autonomia e de racionamento destinam-se exclusivamente ao planeamento geral. Não constituem prescrição clínica, nutricional ou garantia de segurança ou sobrevivência. Crianças, gravidez, doença, necessidades especiais e animais exigem avaliação profissional adequada. Em situação de emergência, segue as orientações das autoridades competentes.

## Tecnologia

- Kotlin
- Jetpack Compose e Material 3
- Room
- DataStore
- Coroutines e Flow
- PBKDF2-HMAC-SHA-256 para derivação local da password
- Android 8.0 ou superior (`minSdk 26`)
- `targetSdk 36`, `compileSdk 37` e JDK 17

## Estrutura do projeto

```text
app/src/main/java/pt/osvaldocipriano/survive/
├── data/          # Room, entidades, DAO, sessão e repositório
├── domain/        # validação e cálculos de planeamento
├── notifications/ # alertas locais de validade
└── ui/            # ecrãs, componentes, localização e tema

app/schemas/       # esquemas Room usados nos testes de migração
docs/              # política de privacidade e páginas públicas
```

## Compilar o projeto

### Requisitos

- Android Studio compatível com AGP 9.2.1
- Android SDK 37
- JDK 17

Clona o repositório e executa:

```bash
git clone https://github.com/nunchuckcoder/survive.git
cd survive
./gradlew test lint assembleDebug
```

O APK de desenvolvimento é criado em:

```text
app/build/outputs/apk/debug/app-debug.apk
```

### AAB de release

Para criar um Android App Bundle assinado sem guardar credenciais no repositório:

```bash
./gradlew clean test lint bundleRelease \
  -PSURVIVE_STORE_FILE=/caminho/privado/upload.jks \
  -PSURVIVE_STORE_PASSWORD='...' \
  -PSURVIVE_KEY_ALIAS='upload' \
  -PSURVIVE_KEY_PASSWORD='...'
```

O ficheiro é criado em `app/build/outputs/bundle/release/app-release.aab`.

Nunca publiques o keystore, passwords, `local.properties` ou ficheiros com dados reais de utilizadores.

## Testes

```bash
./gradlew test
./gradlew lint
./gradlew connectedDebugAndroidTest
```

Os testes instrumentados incluem os percursos de migração da base Room. Antes de uma publicação, deve também ser testada a atualização por cima de uma instalação anterior com dados reais de teste, além dos fluxos de perfil, backup, despensa, medicamentos, mochilas, notificações, temas e idiomas.

## Idiomas

- Português (Portugal), idioma predefinido quando o sistema não usa um idioma suportado
- Inglês

Os dados escritos pelo utilizador — como nomes, produtos, categorias e notas — nunca são traduzidos nem alterados pela interface.

## Versão

- Versão pública: **1.0**
- `versionCode`: **1**
- Base de dados Room: versão interna independente da versão pública

O `versionCode` terá de aumentar em futuros envios para a Google Play, mesmo que o nome público da versão continue temporariamente em 1.0.

## Contacto

Desenvolvido por **Osvaldo Cipriano — NunchuckCoder**.

Para suporte ou questões de privacidade: [osvaldo@osvaldocipriano.dev](mailto:osvaldo@osvaldocipriano.dev)

---

SURVIVE é uma aplicação independente e não representa qualquer organismo público, serviço de emergência ou entidade médica.

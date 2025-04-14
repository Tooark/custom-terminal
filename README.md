# Customizando o Terminal

Configurações para customizar o Terminal do Windows e WSL

## Instale as Fontes

1. Instale as fontes necessárias para o Windows Terminal, como "FiraCode Nerd Font".

2. Acesse o site [Nerd Fonts](https://www.nerdfonts.com/font-downloads)

3. Procure por "FiraCode" e baixe a versão mais recente.

4. Extraia o arquivo ZIP e instale as fontes no seu sistema. Instale as variantes "FiraCode Nerd Font Mono".
   - `FiraCodeNerdFontMono-Bold.ttf`
   - `FiraCodeNerdFontMono-Light.ttf`
   - `FiraCodeNerdFontMono-Medium.ttf`
   - `FiraCodeNerdFontMono-Regular.ttf`
   - `FiraCodeNerdFontMono-Retina.ttf`
   - `FiraCodeNerdFontMono-SemiBold.ttf`

**Nota:**

- Para instalar as fontes, clique com o botão direito do mouse sobre cada arquivo de fonte e selecione "Instalar".
- Se o terminal estiver aberto, feche e reabra para que as fontes apareçam corretamente.

## Criar Esquema de Cores

1. Abra as Configurações do Windows Terminal pressionando `Ctrl + ,`.

2. Abra Configurações no Terminal do Windows e pressione o botão **"Abrir arquivo JSON"** no canto inferior esquerdo.

3. O arquivo `settings.json` será aberto no seu editor de texto padrão.

4. Localize a seção **"schemes"** no arquivo `settings.json`. Se não houver uma seção **"schemes"**, você pode adicioná-la logo após a chave de fechamento do perfil desejado.

5. Adicione o seguinte esquema de cores ao arquivo `settings.json`:

```json
{
  ... other settings
  "schemes": [
    {
      "background": "#101010",
      "black": "#101010",
      "blue": "#0070C0",
      "brightBlack": "#404040",
      "brightBlue": "#61CBF4",
      "brightCyan": "#8EE4F0",
      "brightGreen": "#75B070",
      "brightPurple": "#7B63A0",
      "brightRed": "#F86071",
      "brightWhite": "#E3E3E3",
      "brightYellow": "#FFCE66",
      "cursorColor": "#52F568",
      "cyan": "#00B0F0",
      "foreground": "#F0F0F0",
      "green": "#00B050",
      "name": "Custom color",
      "purple": "#7030A0",
      "red": "#F80A2F",
      "selectionBackground": "#52F568",
      "white": "#F1F1F1",
      "yellow": "#FFC000"
    },
    ...  other schemes
  ],
}
```

## Customize o perfil padrão

1. Localize a seção **"profiles"** no arquivo `settings.json`.

2. Configure o perfil padrão para usar o esquema de cores que você acabou de criar. Adicione ou modifique a seguinte linha dentro do perfil desejado:

   ```json
   {
     ... other settings
     "profiles": {
       "defaults": {
         "backgroundImage": "desktopWallpaper",
         "backgroundImageOpacity": 0.2,
         "colorScheme": "Custom color",
         "font": {
           "face": "FiraCode Nerd Font Mono"
         },
         "padding": "8"
       },
       ... other profiles
     }
   }
   ```

   **Nota:**

   - O valor de `backgroundImage` pode ser o caminho para a imagem que você deseja usar como plano de fundo. Você pode usar `"desktopWallpaper"` para definir a imagem de fundo como a imagem de área de trabalho atual.
   - O valor de `backgroundImageOpacity` controla a opacidade da imagem de fundo. Você pode ajustar esse valor conforme necessário (0.0 a 1.0).
   - O valor de `padding` controla o preenchimento em torno do texto no terminal. Você pode ajustar esse valor conforme necessário (em pixels).
   - Caso queria modificar outros perfis, altere dentro o `list` dentro de `profiles`.

3. Salve o arquivo `settings.json` e feche o editor de texto.

4. O Windows Terminal deve aplicar automaticamente as alterações. Se não, feche e reabra o terminal.

## Customize o tema com "Oh My Posh"

### Windows Terminal

1. Instale o "Oh My Posh" no seu terminal. Você pode usar o seguinte comando no PowerShell:

   ```powershell
   winget install JanDeDobbeleer.OhMyPosh -s winget
   ```

   ou

   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1'))
   ```

   **Nota:**

   - Reinicie o terminal após a instalação para que as alterações tenham efeito.

2. Após a instalação, você pode verificar se o "Oh My Posh" foi instalado corretamente executando o seguinte comando:

   ```powershell
   oh-my-posh --version
   ```

   Se o comando retornar a versão instalada, significa que a instalação foi bem-sucedida.

   Se você não conseguir encontrar o "Oh My Posh" após a instalação, verifique se o caminho foi adicionado corretamente ao seu `PATH`.

   Para adicionar o caminho do "Oh My Posh" ao `PATH`, você pode usar o seguinte comando no PowerShell:

   ```powershell
   $env:Path += ";C:\Users\<YOUR-USER>\AppData\Local\Programs\oh-my-posh\bin"
   ```

   **Nota:**

   - Substitua `<YOUR-USER>` pelo seu nome de usuário do Windows.
   - O caminho pode variar dependendo de onde o "Oh My Posh" foi instalado. Verifique o caminho correto no seu sistema.
   - Reinicie o terminal após a configuração do `PATH` para que as alterações tenham efeito.

3. Configure o seu `$PROFILE` para usar o "Oh My Posh". Abra o arquivo de perfil do PowerShell com o seguinte comando:

   ```powershell
   notepad $PROFILE
   ```

   **Nota:**

   - Se o arquivo não existir, o PowerShell solicitará que você crie um novo arquivo.

4. Adicione a seguinte linha ao arquivo de perfil:

   ```powershell
   oh-my-posh --init --shell pwsh | Invoke-Expression
   ```

5. Salve o arquivo e feche o editor de texto.

6. Reinicie o terminal para aplicar as alterações.

#### Utilizar tema customizado

1. Copie o arquivo [`custom.omp.json`](custom.omp.json) para o diretório `C:\Users\<YOUR-USER>\AppData\Local\Programs\oh-my-posh\themes`

   **Nota:**

   - Substitua `<YOUR-USER>` pelo seu nome de usuário do Windows.

2. Abra o arquivo de perfil do PowerShell novamente:

   ```powershell
   notepad $PROFILE
   ```

3. Altere a configuração do `oh-my-posh` para usar o tema customizado.

   ```powershell
   oh-my-posh --init --shell pwsh --config ~/AppData/Local/Programs/oh-my-posh/themes/custom.omp.json | Invoke-Expression
   ```

4. Salve o arquivo e feche o editor de texto.

5. Reinicie o terminal para aplicar as alterações.

**Nota:**

- O tema customizado pode ser modificado conforme necessário. Você pode personalizar as cores, ícones e outros elementos do tema de acordo com suas preferências.
- Dentro da pasta `themes`, você pode escolher outros temas prontos ou criar o seu próprio tema.
- Para mais informações sobre como personalizar o tema, consulte a [documentação do Oh My Posh](https://ohmyposh.dev/docs/).
- Você pode encontrar temas prontos na [galeria de temas do Oh My Posh](https://ohmyposh.dev/docs/themes/).

### WSL

As configurações para o **WSL** devem ser executadas após configurar o **Windows Terminal**.

1. Abra o WSL e instale o "Oh My Posh" com o seguinte comando:

   ```bash
   sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
   sudo chmod +x /usr/local/bin/oh-my-posh
   ```

2. Verifique se o "Oh My Posh" foi instalado corretamente executando o seguinte comando:

   ```bash
   oh-my-posh --version
   ```

3. Abra as configurações do seu shell. Por exemplo, se você estiver usando o `bash`, abra o arquivo `~/.bashrc`:

   ```bash
   nano ~/.bashrc
   ```

4. Adicione a seguinte linha ao final do arquivo:

   ```bash
   # Oh My Posh
   eval "$(oh-my-posh init bash --config /mnt/c/Users/<YOUR-USER>/AppData/Local/Programs/oh-my-posh/themes/custom.omp.json)"
   ```

   **Nota:**
   - Substitua `<YOUR-USER>` pelo seu nome de usuário do Windows.
   - O tema customizado pode ser modificado conforme necessário. Você pode personalizar as cores, ícones e outros elementos do tema de acordo com suas preferências.
   - Dentro da pasta `themes`, você pode escolher outros temas prontos ou criar o seu próprio tema.
   - Para mais informações sobre como personalizar o tema, consulte a [documentação do Oh My Posh](https://ohmyposh.dev/docs/).
   - Você pode encontrar temas prontos na [galeria de temas do Oh My Posh](https://ohmyposh.dev/docs/themes/).

5. Salve o arquivo e feche o editor de texto.

6. Reinicie o terminal para aplicar as alterações.

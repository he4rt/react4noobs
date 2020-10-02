<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/header-4noobs.svg">
</a>
</p>

# O que é WebPack?

O Webpack é um empacotador de código para projetos web sendo uma ferramenta usada no core do React.

Mas você deve esta se perguntando, mas qual a principal função do Webpack, simples imagine que você precise separar seu código em módulos sera o WebPack que ficara responsável por ler esses arquivos. Porem ele não fica apenas responsável pela leitura dos arquivos, ele também tem a função de converter seu código para javascript puro um grande exemplo disso é você escrever um código em TypeScript.

# Como utilizamos o Webpack com React?

Então chega de teoria e bora ver na prática como isso é aplicado no nosso cotidiano no Ecossistema do React.

Primeiramente, imagine um arquivo chamado index.js é ele que sera nosso principal arquivo de nossa aplicação,e pensando bem deixar todo o código em um unico arquivo pode se tornar problemático no futuro. Por isso iremos dividir em um componente chamado **Title** em outra pasta veja a abaixo o como nosso código ficara:

- **app.js**
'''js

import React from 'react'

export default function Home() {
return (
<div>
Hello World!
</div>

)
}
'''

- **components/title.js**

'''js
import React from 'react'

export default function Title() {
return (
<div>
Sou o Component Title
</div>

)
}

'''

A partir dessa simples separação pode utilizar o title.js em nosso index apenas com uma simples linha. Veja o código abaixo:

'''js
import React from 'react'
import Title from 'components/title.js'

export default function Home() {
return (
<div>
<Title />
</div>

)
}

'''

E pronto a partir de agora nosso componente sera renderizado na tela de maneira dinâmica e sem poluir o index.js.

<p align="center">Made with :purple_heart:</p>

<p align="center">
<a href="https://github.com/he4rt/4noobs" target="_blank">
<img src="../../assets/global/footer-4noobs.svg" width="380">
</a>
</p>
# Flutter vs. Kotlin vs. React Native

## Comparações

### Flutter

#### Vantagens Flutter

- `Cross-Platform`: a renderização de `.obj` em flutter funciona em Android e iOS sem precisar escrever códigos diferentes para cada sistema
- `Facilidade de Integração`: Bibliotecas como `flutter_cube` e `flutter_3d_obj` são fáceis de configurar e renderizar arquivos `.obj`
- `Curva de Aprendizado baixa`: Complexidades como sombras e renderizações são abstraídas de formas mais fáceis
- `Sicronização com UI`: Bem integrado com outros widgets em Flutter

#### Desvantagens Flutter

- `Performance`: Flutter renderiza arquivos `.obj` utilizando `Skia`, perdendo alguns fps em objetos com muitos polígonos
- `Limitação de Features avançadas`: sombras customizadas e efeitos volumétricos
- `Menos controle`: Realizar _Fine-Tuning_ ou modificar os modelos `.obj` em tempo real será mais complicado

#### Cenários ideais Flutter

- Se precisar de um aplicativo _Cross-Platform_ com requisitos de renderização 3d moderados
- Se preferir um desenvolvimento mais rápido do que uma performance maior

### Kotlin (Nativo)

#### Vantagens Kotlin (Nativo)

- `Performance`: Uso da GPU auxilia em uma renderização mais suave
- `Features avançadas`: sombras customizadas, iluminação volumétrica e controle mais preciso da renderização
- `Modificações em tempo real`: suporta modificações dinamicas em arquivos `.obj`, como ajustar texturas e modificar os vértices

#### Desvantagens Kotlin (Nativo)

- `Dependencias de plataforma`: Soluções utilizando `OpenGL ES` e `Vulkan` funcionam apenas em dispositivos Android, precisando de uma implementação separada para iOS (Ex: `Metal` ou `SceneKit`)
- `Alta complexidade`: Necessita de um conhecimento mais profundo em renderização 3d e suas bibliotecas necessárias, custando mais tempo
- `Despesas gerais de desenvolvimento`: A integração nativa com Kotlin vai necessitar de mais esforço em manutenção de código, principalmente lidando com multiplas plataformas

#### Cenários ideais Kotlin (Nativo)

- Quando a performance e qualidade de renderização são prioridades
- Quando é necessário técnicas avançadas de renderização para visualização médica, como cortar planos, transparência ou iluminação volumétrica

### Kotlin Multiplatform

#### Vantagens Kotlin Multiplatform

- `Logica compartilhada`: O carregamento, processamento e transformação de arquivos `.obj` podem ser implementados uma vez em Kotlin e reutilizados em várias plataformas
- `Escalabilidade`:O código está preparado para futuras expansões para outras plataformas, como desktop ou web
- `Integração com a UI`: A abordagem permite criar uma interface visual nativa, como Jetpack Compose no Android ou SwiftUI no iOS, oferecendo maior flexibilidade

#### Desvantagens Kotlin Multiplatform

- `Complexidade da Renderização`: A lógica de renderização nativa precisa ser implementada separadamente para cada plataforma.
- `Curva de Aprendizado`: Necessita de um conhecimento mais profundo em renderização 3d e suas bibliotecas necessárias, custando mais tempo
- `Ecossistema de Pacotes`: Flutter possui um ecossistema mais maduro para renderização 3D em comparação ao KMM.

#### Cenários ideais Kotlin Multiplatform

- Quando a performance e qualidade de renderização são prioridades
- Quando busca escalabilidade e flexibilidade a longo prazo

### React Native

#### Vantagens React Native

- Cross-Platform com grande comunidade e ecossistema.
- Desenvolvimento rápido com hot-reloading.
- Ótima integração com Three.js via react-three-fiber.

#### Desvantagens React Native

- Desempenho um pouco abaixo do nativo (em alguns casos).
- Dependência de bibliotecas de terceiros.
- Curva de aprendizado mais fácil no início, mas desafios em casos complexos.

#### Cenários Ideais React Native

- Desenvolvimento multiplataforma rápido com bom suporte 3D (via Three.js), ampla comunidade, prototipagem e implementação flexível.

## Principais Diferenças

| Feature                       | Flutter                                       | Kotlin (Nativo)                     | Kotlin Multiplatform                       | React Native                                |
| ----------------------------- | --------------------------------------------- | ----------------------------------- | ------------------------------------------ | ------------------------------------------- |
| Suporte de Plataforma         | Cross-platform (iOS e Android)                | Apenas Android                      | Lógica Compartilhada, UI nativa            | Cross-platform (iOS e Android)              |
| Facilidade de Uso             | Simples com pacotes e bibliotecas disponíveis | Curva de aprendizado mais alta      | Moderada a Alta                            | Moderada                                    |
| Performance                   | Moderado (Limitações da `Skia`)               | Alta (Otimização com GPU)           | Alta (APIs nativas)                        | Moderada (em alguns casos)                  |
| Velocidade de Desenvolvimento | Prototipação mais rápida                      | Tempo para implementação mais longo | Moderado (lógica compartilhada, UI nativa) | Prototipação e desenvolvimento mais rápidos |
| Integração com UI             | Boa Integração com a UI do Flutter            | Requer implementação customizada    | Controles nativos (Compose, SwiftUI)       | Boa integração com React UI                 |
| Integração 3D (Three.js)      | Moderada (pacotes específicos)                | Baixa (implementação customizada)   | Moderada (implementação customizada)       | Alta (via react-three-fiber)                |

## Recomendações

### Usar Flutter se

- Quiser priorizar compatibilidade entre plataformas
- Os arquivos `.obj` não forem extremamente complexos
- Preferir um desenvolvimento mais rápido com uma integração fácil ao aplicativo
- Features de renderização avançadas não for um ponto crítico

### Usar Kotlin com renderização nativa se

- Alta performance e renderização detalhada forem cruciais, especialmente em arquivos `.obj` maiores e mais complexos.
- Precisar de capacidades de renderização avançadas, como sombras e texturas customizadas e modificações em tempo real
- Se o aplicativo for apenas para android, ou otimizações em plataformas específicas forem aceitáveis

### Usar Kotlin Multiplatform se

- Deseja compartilhar a lógica de processamento de modelos entre várias plataformas.
- Precisa de alta performance com renderização nativa.
- Busca escalabilidade e flexibilidade a longo prazo.

## Workflow para Renderização de DICOM em arquivos `.obj`

1. **Pré-Processamento do DICOM:**
   - Converter a imagem DICOM em um arquivo `.obj` usando [3D Slicer](https://www.slicer.org/) ou Bibliotecas Python como `pydicom` e `vtk`
2. **Renderizando em Flutter:**
   - Usar `flutter_cube` para uma visualização básica de `.obj`
   - Otimizar o modelo `.obj` (por exemplo reduzir o número de polígonos) para uma renderização mais suave
3. **Renderizando em Kotlin (Nativo):**

   - Usar `Rajawali` ou implementar diretamente `OpenGL ES`
   - Customizar o pipeline de renderização para um controle mais preciso de texturas, iluminação e câmera

4. **Renderizando em Kotlin Multiplatform:**
   - Implemente a lógica comum para:
     - Carregar e processar arquivos `.obj`.
     - Realizar transformações, como escalonamento e rotação.
     - Gerenciar metadados e parâmetros adicionais de renderização.
   - Implemente a lógica de renderização separadamente para Android e iOS.
   - Integrar Com a UI (também separadamente)
   - Otimização de Performance

## Análise Expandida: Flutter vs. Kotlin vs. React Native

**Considerações Adicionais sobre React Native:**

- **Ecossistema 3D:** A biblioteca react-three-fiber facilita a integração do Three.js, sendo uma grande vantagem para MedSimVR que necessita de renderização 3D.

- **Comunidade:** A comunidade de React Native é enorme, o que garante acesso a vários tutoriais, bibliotecas e ajuda da comunidade.

- **Flexibilidade:** React Native possibilita criar interfaces de usuário com componentes nativos, sendo flexível para diferentes tipos de projetos.

- **Atualizações:** A comunidade ativa garante que a plataforma esteja sendo constantemente atualizada e otimizada, sendo uma boa escolha para projetos que precisam ser escaláveis no futuro.

**Minha Opinião e Recomendação Final:**

Considerando todas as informações, incluindo as novas sobre React Native, minha recomendação é:

**React Native para o MedSimVR:**

- **Melhor Integração 3D:** A facilidade de integrar o Three.js através do react-three-fiber é uma vantagem crítica, uma vez que a manipulação de modelos 3D é essencial para o projeto.

- **Velocidade de Desenvolvimento:** O React Native permite o desenvolvimento rápido e iterativo, o que facilita a prototipagem e a validação de ideias, sendo ideal para projetos com necessidade de iterações rápidas.

- **Ecossistema e Comunidade:** A grande comunidade e o ecossistema do React Native oferecem muitos recursos, tutoriais, bibliotecas, garantindo um suporte e desenvolvimento mais ágil.

- **Cross-Platform:** Atende à necessidade de alcançar usuários em Android e iOS com uma base de código compartilhada, otimizando tempo de desenvolvimento e manutenção.

- **Flexibilidade:** É possível ter interfaces de usuários bem definidas e componentes nativos por meio do React Native, com a possibilidade de adicionar novos recursos no futuro.

**Por que não as outras opções:**

- **Flutter:** Apesar de ser bom para cross-platform, a limitação na performance e falta de controle na renderização 3D podem ser um problema, especialmente se a manipulação dos modelos DICOM for crucial.

- **Kotlin Nativo:** É excelente para performance, mas a necessidade de criar uma base de código separada para iOS e a complexidade na configuração e manutenção não se alinham com a necessidade de agilidade e produtividade, além de não possuir a integração do Three.js.

- **Kotlin Multiplatform:** Apesar de ótimo para compartilhamento de código, a complexidade na integração da renderização 3D (implementar nativo para Android e iOS) faz com que não seja a opção mais adequada para o projeto, especialmente na fase inicial.

## Integração multiplataforma do ReactNative

| React Native UI Component | Android View   | iOS View         | Web Analog              | Description                                                                                           |
| ------------------------- | -------------- | ---------------- | ----------------------- | ----------------------------------------------------------------------------------------------------- |
| `<View>`                  | `<ViewGroup>`  | `<UIView>`       | A non-scrolling `<div>` | A container that supports layout with flexbox, style, some touch handling, and accessibility controls |
| `<Text>`                  | `<TextView>`   | `<UITextView>`   | `<p>`                   | Displays, styles, and nests strings of text and even handles touch events                             |
| `<Image>`                 | `<ImageView>`  | `<UIImageView>`  | `<img>`                 | Displays different types of images                                                                    |
| `<ScrollView>`            | `<ScrollView>` | `<UIScrollView>` | `<div>`                 | A generic scrolling container that can contain multiple components and views                          |
| `<TextInput>`             | `<EditText>`   | `<UITextField>`  | `<input type="text">`   | Allows the user to enter text                                                                         |

### Links React Native

- [Documentação](https://reactnative.dev/docs/getting-started)
- [Playlist OneBitCode Curso React Native (aprendiz)](https://www.youtube.com/playlist?list=PLdDT8if5attEd4sRnZBIkNihR-_tE612_)
- [Como gerar o APK e AAB do App com EXPO 2023](https://www.youtube.com/watch?v=bIMk6iaPOBE)
  - Naturalmente, o expo gera um arquivo .AAB (appBundle), que é necessário para enviar para a Play Store
  - Para gerar um .apk e testar no android sem precisar publicar o app, apenas é necessário mudar o `buildType` no arquivo `eas.json`

```json
{
  "build": {
    "preview": {
      "android": {
        "buildType": "apk"
      }
    }
  }
}
```

E fazer o build do preview

```bash
eas build --platform android --profile preview
```

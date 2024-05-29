# Recriando-o-Flappy-Bird-com-Unity

Vou criar um guia detalhado para recriar o Flappy Bird com Unity. Vou dividir o processo em módulos para facilitar o entendimento. Lembre-se de personalizar o jogo com sua própria identidade e criatividade. Vamos lá!

## Módulo 1: Configuração do Projeto
1. **Instalação do Unity:**
   - Se você ainda não tem o Unity instalado, baixe a versão mais recente no site oficial.
   - Abra o Unity Hub e crie um novo projeto 2D.

2. **Configuração Inicial:**
   - Defina a resolução do jogo (por exemplo, 720x1280).
   - Importe os sprites do Flappy Bird (pássaro, canos, fundo etc.).

## Módulo 2: Criando o Pássaro
1. **Criando o GameObject do Pássaro:**
   - Crie um novo GameObject chamado "Bird".
   - Adicione um componente Rigidbody2D para simular a física do pássaro.
   - Adicione um componente Collider2D (por exemplo, Circle Collider) para detecção de colisões.

2. **Script de Controle do Pássaro:**
   - Crie um novo script chamado "BirdController".
   - Implemente o movimento do pássaro (pulo) usando `Rigidbody2D.AddForce()` ou `Rigidbody2D.velocity`.
   - Detecte o clique do mouse ou toque na tela para fazer o pássaro pular.

## Módulo 3: Criando os Canos
1. **Criando o Prefab dos Canos:**
   - Crie um novo GameObject chamado "Pipe".
   - Adicione dois sprites (cano superior e inferior) como filhos do GameObject.
   - Posicione-os corretamente para formar um cano completo.

2. **Gerando os Canos:**
   - Crie um script chamado "PipeSpawner".
   - Use `Instantiate()` para criar os canos em intervalos regulares.
   - Ajuste a altura dos canos aleatoriamente para criar variação.

## Módulo 4: Pontuação e Colisões
1. **Pontuação:**
   - Crie um objeto vazio chamado "ScoreManager".
   - Detecte quando o pássaro passa pelos canos e atualize a pontuação.

2. **Colisões:**
   - No script do pássaro, detecte colisões com os canos e com o chão.
   - Reinicie o jogo quando o pássaro colidir com um cano ou o chão.

## Módulo 5: Interface do Jogo
1. **Canvas e Texto:**
   - Crie um Canvas para a interface do jogo.
   - Adicione um Text para exibir a pontuação.

2. **Atualização da Pontuação:**
   - No script do ScoreManager, atualize o Text com a pontuação atual.

## Módulo 6: Polimento e Detalhes
1. **Animações:**
   - Adicione animações ao pássaro (bater asas, cair etc.).
   - Crie animações para os canos (subindo, descendo).

2. **Efeitos Sonoros:**
   - Adicione sons para o pulo do pássaro, colisões e pontuação.

Lembre-se de testar o jogo regularmente e ajustar os valores conforme necessário.

Claro! Vou fornecer um exemplo básico de como implementar o movimento do pássaro e a geração dos canos no Flappy Bird usando C# no Unity. Lembre-se de adaptar o código ao seu projeto e adicionar mais funcionalidades conforme necessário.

### Script do Pássaro (BirdController.cs)
```csharp
using UnityEngine;

public class BirdController : MonoBehaviour
{
    public float jumpForce = 5f;
    private Rigidbody2D rb;

    private void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        if (Input.GetMouseButtonDown(0)) // Detecta clique do mouse
        {
            Jump();
        }
    }

    private void Jump()
    {
        rb.velocity = Vector2.up * jumpForce;
    }
}
```

### Script de Geração dos Canos (PipeSpawner.cs)
```csharp
using UnityEngine;

public class PipeSpawner : MonoBehaviour
{
    public GameObject pipePrefab;
    public float spawnInterval = 2f;
    public float pipeHeightVariation = 2f;

    private float nextSpawnTime;

    private void Start()
    {
        nextSpawnTime = Time.time + spawnInterval;
    }

    private void Update()
    {
        if (Time.time >= nextSpawnTime)
        {
            SpawnPipe();
            nextSpawnTime = Time.time + spawnInterval;
        }
    }

    private void SpawnPipe()
    {
        float randomY = Random.Range(-pipeHeightVariation, pipeHeightVariation);
        Vector3 spawnPosition = new Vector3(transform.position.x, randomY, 0);
        Instantiate(pipePrefab, spawnPosition, Quaternion.identity);
    }
}
```

Lembre-se de criar os GameObjects "Bird" e "Pipe" no Unity, adicionar os componentes necessários e vincular os scripts aos objetos corretos. Além disso, ajuste os valores das variáveis conforme sua preferência.

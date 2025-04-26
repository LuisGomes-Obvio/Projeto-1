# Projeto 1
Neste jogo, o jogador assume o papel de um papa-formigas que persegue uma formiga enquanto ela tenta recolher folhas para a sua casa, ao mesmo tempo que tenta evitar o inimigo. O jogador controla o papa-formigas com o cursor do rato e tenta apanhar a formiga, que possui um comportamento automático e é controlada pelo programa, fazendo com que por exemplo ela se mova mais rapidamente caso o papa-formigas se aproxime dela.

se eu fizer isto o que acontece?


![image](https://github.com/user-attachments/assets/e8251d6c-7445-4063-97a2-f2c5a497afd6)

 

- MonoGame SDK
- Visual Studio 2022 (ou superior)
- .NET Framework/Core

Repositório do jogo: https://github.com/itivadar/LilAnt-Game

- Luís Gomes - 31473
- Samuel Fernandes - 31470
- David Barbosa - 31461

lalalalala ```scharp   Vector2 Origin { get; set; } ```

IGameObject é uma interface que permite, individualmente, atribuir a todos os objetos do uma jogo os mesmos tipos de características representados em baixo:
- Posição;    ```csharp   Vector2 Position { get; set; } ```
- Velocidade;    ```Vector2 Velocity { get; set; }```
- Direção;    ```Vector2 Direction { get; set; } ```
- Rotação;    ```float Rotation { get;} ```
- Ponto de Origem;    ```Vector2 Origin { get; set; } ```
- Tamanho do Sprite;   ```int Height { get; } 
                          int Width { get; }```
- Visibilidade;    ```bool Visible { get; set; }```

Além disso possui uma série de métodos ou instruções que permitem carregar conteúdos, atualizar o estado dos objetos, desenhá-los no ecrã e lidar com comandos do jogador.

Isto facilita a organização do código e permite que os objetos do jogo funcionem de uma maneira consistente.

<details>
  <summary>Clica aqui para ver o código do GameManager</summary>

```csharp
﻿using ExampleGame;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Content;
using Microsoft.Xna.Framework.Graphics;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TheTirelessLilAnt.Components
{
    public class GameManager : IGameManager
    {
        private List<IGameObject> _objects;

        /// <summary>
        /// Lists of all object in the game. 
        /// </summary>
        public IEnumerable<IGameObject> GameObjects => _objects;
        
        public GameManager()
        {
            _objects = new List<IGameObject>();
        }

        /// <summary>
        /// Adds an new entity to the game objects collection. 
        /// </summary>
        public void AddObject(IGameObject gameObject)
        {
            if (gameObject is null) return;
            _objects.Add(gameObject);
        }

        /// <summary>
        /// Calls the Update() of every visible game object.
        /// </summary>
        public void DrawObjects(SpriteBatch spritebatch)
        {
            var visibleObjects = GameObjects.Where(gameObject => gameObject.Visible);
            foreach (IGameObject gameObject in visibleObjects)
            {
                gameObject.Draw(spritebatch);
            }
        }

        /// <summary>
        /// Calls the Update() of every game objects. 
        /// </summary>
        public void UpdateObjects(GameTime gameTime)
        {
            foreach (IGameObject gameObject in GameObjects)
            {
                gameObject.HandleInput();
                gameObject.Update(gameTime);
            }
        }

        /// <summary>
        /// Unloads the content of the game objects.
        /// </summary>
        public void UnloadObjects()
        {
            foreach (IGameObject gameObject in GameObjects)
            {
                gameObject.UnloadContent();
            }
        }

        /// <summary>
        /// Loads resources of every game object.
        /// </summary>
        public void LoadObjects(ContentManager contentManager)
        {
            foreach (IGameObject gameObject in GameObjects)
            {
                gameObject.LoadContent(contentManager);
            }
        }       
    }
}

```
</details>
lalalala

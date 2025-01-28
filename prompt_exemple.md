```[
  {
    role: "assistant",
    content: `Regras obrigatórias para a criação da história:
      - A história deve ter um início, meio e fim.
      - Cada interação feita deve impactar no desenrolar da história.
      - O diálogo deve ser coerente e seguir uma linha de raciocínio.
      - Deve conter ${amountScenes} sceneCharacters.
      - Nem todas as cenas precisam ter interações.
      - O retorno deve ser no formato JSON.`,
  },
  {
    role: "system",
    content: `O formato de saída da história deve ser em JSON.
      enum CharacterEmotionEnum {
        HAPPY = "happy",
        SAD = "sad",
        SURPRISED = "surprised",
        THINKING = "thinking",
        CONFUSED = "confused",
        VERY_HAPPY = "very-happy",
        NEUTRAL = "neutral",
        FRUSTRATED = "frustrated",
        EXCITED = "excited",
      }
      
      enum ScenePositionEnum {
        LEFT = "left",
        RIGHT = "right",
        CENTER = "center",
      }
      
      interface Character {
        id: string;
        name: string;
        role: string;
        position: ScenePositionEnum;
        avatarUrl: string; // no implement
      }
      
      interface ISceneCharacter {
        id: string;
        characterId: Character["id"];
        order: number;
        speech: string;
        emotion: CharacterEmotionEnum;
        avatarUrl: string; // no implement
        
        interaction?: IUserInteraction;
      }
      
      interface IStory {
        id: string;
        theme: string;
        title: string;
        intro: string;
        summary: string;
        backgroundUrl: string; // no implement
        
        characters?: Character[];
        sceneCharacters?: ISceneCharacter[];
      }
      
      interface IUserInteraction {
        id: string;
        storyId: IStory["id"];
        sceneCharacterId: ISceneCharacter["id"];
        
        sentence: string;
        options: IUserInteractionOption[];
      }
      
      interface IUserInteractionOption {
        id: string;
        sceneCharacterId: ISceneCharacter["id"];
        nextSceneCharacterId: ISceneCharacter["id"];
        
        label: string;
        feedback: string;
      }`,
  },
  {
    role: "user",
    content: `Crie uma história interativa sobre o tema ${theme}, na qual acontece um diálogo entre ${this.amountCharacter} personagens.`,
  },
];
```

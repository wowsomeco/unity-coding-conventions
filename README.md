# C# Coding Conventions for Wowsome Unity projects

## Naming Conventions

#### 1. Do use PascalCasing for class names and method names:

```csharp
public class GameController {
  public void Play() {
    // ...
  }
  
  public void GameOver() {
    // ...
  }
}
```

***Why: consistent with the Microsoft's .NET Framework and easy to read.***

#### 2. Do use camelCasing for method arguments and local variables:

```csharp
public class PlayerEntity {
  public void OnAttacked(EnemyEntity enemyEntity) {
    int damage = enemyEntity.damage;
    // ...
  }
}
```

#### 3. Do use camelCasing for public fields

```csharp
public class EnemyEntity {
  // Correct
  public int damage;
  // Avoid
  public int Damage;
  public int _damage;
}
```

***Why: consistent with the Microsoft's .NET Framework. It's also consistent with json naming conventions so no conversion needs to be done when it gets (de)serialized from / to json data***

I know it's [not recommended](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/field?redirectedfrom=MSDN) to provide instance fields that are public or protected. However in Unity it's inevitable since accessors won't get serialized in the Editor. Also accessors is somehow tricky when it comes to Unity JsonUtility serialization e.g. you need to define SerializeField attribute to make it work, hence more steps to do.

#### 4. Do use prefix `_` followed by camelCasing for private fields

```csharp
public class EnemyEntity {
  // Correct
  private int _counter;
  // Avoid
  private int m_counter;
  private int m_Counter;
  private int _Counter;
}
```

***Why: consistent with the Microsoft's .NET Framework. Easy to read, shorter to type***

#### 5. Do use PascalCasing for accessors (getters & setters)

```csharp
public class Dimension {
  // Correct
  public double Distance { get; private set; }
  // Avoid
  public double distance { get; private set; }
}
```

***Why: consistent with the Microsoft's .NET Framework.***

#### 6. Do not use Screaming Caps for constants or readonly variables:

```csharp
// Correct
public const string ShippingType = "DropShip";
// Avoid
public const string SHIPPINGTYPE = "DropShip";
```

***Why: consistent with the Microsoft's .NET Framework. Caps grab too much attention.***

#### 7. Do prefix interfaces with the letter I. Interface names are noun (phrases) or adjectives.

```csharp     
public interface IShape {
}

public interface IShapeCollection {
}

public interface IGroupable {
}
```

***Why: consistent with the Microsoft's .NET Framework.***

#### 8. Do use PascalCasing for Enum. Do not use an "Enum" suffix in enum type names

```csharp 
// Correct
public enum Color
{
  Red,
  Green,
  Blue,
  Yellow,
  Magenta,
  Cyan
}

// Don't
public enum ColorEnum
{
  RED,
  GREEN,
  BLUE,
  YELLOW,
  MAGENTA,
  CYAN
}
```

***Why: consistent with the Microsoft's .NET Framework. Caps grab too much attention.***

#### 9. Do declare all static variables at the very top of a class, followed by accessors, member variables, and lastly the methods respectively. Separate each of them with new line.

```csharp 
public class MenuController {
  public static string ScreenMain = "main";
  public static string ScreenSelectLevel = "select_level";
  
  public string SelectedScreen { get; set; }     
  public bool IsTransitioning { get; private set; }  
  
  public bool shouldAnimate;
  
  bool _counter = 0;
  
  public void PublicMethod() {
    // ...
  }
  
  protected void ProtectedMethod() {
    // ...
  }
  
  private void PrivateMethod() {
    // ...
  }
}
```

***Why: generally accepted practice that prevents the need to hunt for variable declarations e.g. public stuffs reside at the very top since those are normally the things that another programmers are interested in the most***

## Formatting

#### 1. Do not put open-braces on a new line for everything i.e. class, interface, methods, accessors, etc.

```csharp 
// Correct
public class GameController : IGameController {
  public interface IGameObject {
    void InitGameObject(IGameController controller);
  }

  public bool IsGameOver {
    get {
      return _isGameOver;
    }
    set {
      _isGameOver = value;
      // do something else here ...
    }
  }
  
  private bool _isGameOver = false;
  
  public void SomeMethod() {
    // ...
  }
}

// Avoid
public class GameController : IGameController 
{
  public interface IGameObject 
  {
    void InitGameObject(IGameController controller);
  }

  public bool IsGameOver 
  {
    get 
    {
      return _isGameOver;
    }
    set 
    {
      _isGameOver = value;
      // do something else here ...
    }
  }
  
  private bool _isGameOver = false;
  
  public void SomeMethod() 
  {
    // ...
  }
}
```

***Why: This might be debatable since the .NET standard is the open-braces-on-a-new-line one. However, doing so will waste more vertical lines for you which results in less readability esp. for other team members that read your code for the first time and need to scroll up and down frequently.***

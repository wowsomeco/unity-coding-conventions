# C# Coding Standards and Naming Conventions for Unity

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

More Coming Soon...

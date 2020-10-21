# How to Implement IGameObject

If you want to implement `IGameObject` directly, you might be interested in setting the `GameObject.Position` safely. Here is an example property which changes the position safely:

```
    public TheSadRogue.Point Position
    {
        get => _position;
        set
        {
            if (_position != value)
            {
                var oldValue = _position;
                _position = value;
                Moved?.Invoke(this, new MovedEventArgs(oldValue, _position);
            }
        }
    }
```
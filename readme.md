thread-safe-lazy
====

```c#
class Foo : LazyObject<Dictionary<string, string>>
{
  public override Dictionary<string, string> Fetch()
  {
    /* fetch data from network.... */

    return data;
  }

  public string name
  {
    get
    {
      EnsureDataInLocal();

      return data[nameof(name)];
    }
  }
  public string description
  {
    get
    {
      EnsureDataInLocal();

      return data[nameof(description)];
    }
  }
}
```
```c#
Foo foo = FooFactory.Create();

/* 실제 foo 객체를 이용해야 하는 메소드 */
void PlayingWithFoo()
{
  foo.FetchAsync(); // 중간 로직이 실행되는 동안 미리 fetch

  /* .... 중간 로직 .... */

  Console.WriteLine(foo.name); // 출력은 fetch가 완료되면 실행된다.
}
```
```c#
Foo foo = FooFactory.Create();

Console.WriteLine(foo.name); // 출력은 fetch가 완료될 때 까지 블럭된 후 실행된다.
```

Usage
----
* [jenkins-client.net](https://github.com/pjc0247/jenkins-client.net)
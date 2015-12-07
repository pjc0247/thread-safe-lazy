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

/* ���� foo ��ü�� �̿��ؾ� �ϴ� �޼ҵ� */
void PlayingWithFoo()
{
  foo.FetchAsync(); // �߰� ������ ����Ǵ� ���� �̸� fetch

  /* .... �߰� ���� .... */

  Console.WriteLine(foo.name); // ����� fetch�� �Ϸ�Ǹ� ����ȴ�.
}
```
```c#
Foo foo = FooFactory.Create();

Console.WriteLine(foo.name); // ����� fetch�� �Ϸ�� �� ���� ���� �� ����ȴ�.
```

Usage
----
* [jenkins-client.net](https://github.com/pjc0247/jenkins-client.net)
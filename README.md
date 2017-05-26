# Fluent Validator
### A .NET Core library that uses lambda expressions to build validations rules.

## Nuget Package
```
Install-Package FluentValidator.Core
```

## Example Usage
### Initializing validations from a constructor
```
public class Person : Notifiable
{
    public string Name { get; set; }
    public string Email { get; set; }
    public int Age { get; set; }
    
    public Person(){}

    public Person(string name, string email, int age)
    {
        this.Name = name;
        this.Email = email;
        this.Age = age;

        new ValidationContract<Person>(this).IsRequired(x => x.Name);
        new ValidationContract<Person>(this).IsRequired(x => x.Email);
        new ValidationContract<Person>(this).IsGreaterThan(x => x.Age, 18);
        new ValidationContract<Person>(this).IsEmail(x => x.Email);
    }
}
```
### Initializing validations from an existing object instance
```
public class Person : Notifiable
{
    public string Name { get; set; }
    public string Email { get; set; }
    public int Age { get; set; }
    
    public Person()
    {

    }
}

class Program 
{
    static void Main(string[] args)
    {
        Person newPerson = new Person();
        newPerson.Name = "Milton";
        newPerson.Email = "miltomcamara@gmail.com";
        newPerson.Age = 15;

        new ValidationContract<Person>(newPerson).IsRequired(x => x.Name);
        new ValidationContract<Person>(newPerson).IsRequired(x => x.Email);
        new ValidationContract<Person>(newPerson).IsGreaterThan(x => x.Age, 18);
        new ValidationContract<Person>(newPerson).IsEmail(x => x.Email);            

        Console.WriteLine(newPerson.IsValid());
        
        foreach(var message in newPerson.Notifications)
        {
            Console.WriteLine(message.Message);
        }
    }
}
```
## Availble validators
- IsRequired(Expression<Func<T, string>> selector, string message = "")
- HasMinLenght(Expression<Func<T, string>> selector, int min, string message = "")
- HasMaxLenght(Expression<Func<T, string>> selector, int max, string message = "")
- IsFixedLenght(Expression<Func<T, string>> selector, int length, string message = "")
- IsEmail(Expression<Func<T, string>> selector, string message = "")
- IsUrl(Expression<Func<T, string>> selector, string message = "")
- IsGreaterThan(Expression<Func<T, int>> selector, int number, string message = "")
- IsGreaterOrEqualsThan(Expression<Func<T, int>> selector, int number, string message = "")
- IsGreaterThan(Expression<Func<T, decimal>> selector, decimal number, string message = "")
- IsGreaterOrEqualsThan(Expression<Func<T, decimal>> selector, decimal number, string message = "")
- IsGreaterThan(Expression<Func<T, double>> selector, double number, string message = "")
- IsGreaterOrEqualsThan(Expression<Func<T, double>> selector, double number, string message = "")
- IsGreaterThan(Expression<Func<T, DateTime>> selector, DateTime date, string message = "")
- IsGreaterOrEqualsThan(Expression<Func<T, DateTime>> selector, DateTime date, string message = "")
- IsLowerThan(Expression<Func<T, int>> selector, int number, string message = "")
- IsLowerOrEqualsThan(Expression<Func<T, int>> selector, int number, string message = "")
- IsLowerThan(Expression<Func<T, decimal>> selector, decimal number, string message = "")
- IsLowerOrEqualsThan(Expression<Func<T, decimal>> selector, decimal number, string message = "")
- IsLowerThan(Expression<Func<T, double>> selector, double number, string message = "")
- IsLowerOrEqualsThan(Expression<Func<T, double>> selector, double number, string message = "")
- IsLowerThan(Expression<Func<T, DateTime>> selector, DateTime date, string message = "")
- IsLowerOrEqualsThan(Expression<Func<T, DateTime>> selector, DateTime date, string message = "")
- IsBetween(Expression<Func<T, int>> selector, int a, int b, string message = "")
- IsBetween(Expression<Func<T, decimal>> selector, decimal a, decimal b, string message = "")
- IsBetween(Expression<Func<T, double>> selector, double a, double b, string message = "")
- IsBetween(Expression<Func<T, DateTime>> selector, DateTime a, DateTime b, string message = "")
- Contains(Expression<Func<T, string>> selector, string text, string message = "")
- IsNull(object obj, string message)
- IsNotNull(object obj, string message)
- AreEquals(Expression<Func<T, string>> selector, string text, string message = "")
- AreEquals(Expression<Func<T, int>> selector, int val, string message = "")
- AreEquals(Expression<Func<T, decimal>> selector, decimal val, string message = "")
- AreEquals(Expression<Func<T, double>> selector, double val, string message = "")
- AreEquals(Expression<Func<T, bool>> selector, bool val, string message = "")
- AreEquals(Expression<Func<T, DateTime>> selector, DateTime val, string message = "")
- AreNotEquals(Expression<Func<T, string>> selector, string text, string message = "")
- AreNotEquals(Expression<Func<T, int>> selector, int val, string message = "")
- AreNotEquals(Expression<Func<T, decimal>> selector, decimal val, string message = "")
- AreNotEquals(Expression<Func<T, double>> selector, double val, string message = "")
- AreNotEquals(Expression<Func<T, bool>> selector, bool val, string message = "")
- AreNotEquals(Expression<Func<T, DateTime>> selector, DateTime val, string message = "")
- IsTrue(Expression<Func<T, bool>> selector, string message = "")
- IsFalse(Expression<Func<T, bool>> selector, string message = "")
- IsTrue(bool value, string field, string message = "")
- IsFalse(bool value, string field, string message = "")

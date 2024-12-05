# Demos

## DI mit Singleton und Transient

```csharp
using Microsoft.Extensions.DependencyInjection;
using System;

namespace ConsoleAppDI
{
    public interface IMessageWriter
    {
        void Write(string message);
    }

    public class ConsoleMessageWriter : IMessageWriter
    {
        public void Write(string message)
        {
            Console.WriteLine(message);
        }
    }

    public class MessageProcessor
    {
        private readonly IMessageWriter _writer;

        public MessageProcessor(IMessageWriter writer)
        {
            _writer = writer;
        }

        public void Process()
        {
            _writer.Write("Processing message...");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Configure services
            var serviceCollection = new ServiceCollection();
            ConfigureServices(serviceCollection);

            // Build service provider
            var serviceProvider = serviceCollection.BuildServiceProvider();

            // Get and use the singleton service (same instance)
            var singletonProcessor1 = serviceProvider.GetService<MessageProcessor>();
            singletonProcessor1.Process();

            var singletonProcessor2 = serviceProvider.GetService<MessageProcessor>();
            singletonProcessor2.Process();

            // Get and use the transient service (different instances)
            var transientWriter1 = serviceProvider.GetService<IMessageWriter>();
            transientWriter1.Write("This is a transient instance.");

            var transientWriter2 = serviceProvider.GetService<IMessageWriter>();
            transientWriter2.Write("This is another transient instance.");
        }

        private static void ConfigureServices(IServiceCollection services)
        {
            // Register MessageProcessor as a singleton
            services.AddSingleton<MessageProcessor>();

            // Register IMessageWriter as a transient
            services.AddTransient<IMessageWriter, ConsoleMessageWriter>();
        }
    }
}
```

## DI mit Property Injection

```csharp
using Microsoft.Extensions.DependencyInjection;
using System;

namespace ConsoleAppDIPropertyInjection
{
    public interface IMessageWriter
    {
        void Write(string message);
    }

    public class ConsoleMessageWriter : IMessageWriter
    {
        public void Write(string message)
        {
            Console.WriteLine(message);
        }
    }

    public class MessageProcessor
    {
        // Property Injection
        public IMessageWriter MessageWriter { get; set; }

        public void Process()
        {
            if (MessageWriter != null)
            {
                MessageWriter.Write("Processing message with property injection...");
            }
            else
            {
                Console.WriteLine("MessageWriter is not set.");
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Configure services
            var serviceCollection = new ServiceCollection();
            ConfigureServices(serviceCollection);

            // Build service provider
            var serviceProvider = serviceCollection.BuildServiceProvider();

            // Get a new instance of MessageProcessor
            var processor = serviceProvider.GetService<MessageProcessor>();

            // Property Injection: Manually set the property
            processor.MessageWriter = serviceProvider.GetService<IMessageWriter>();

            // Use the service
            processor.Process();
        }

        private static void ConfigureServices(IServiceCollection services)
        {
            // Register services
            services.AddTransient<MessageProcessor>();
            services.AddTransient<IMessageWriter, ConsoleMessageWriter>();
        }
    }
}
```

## Transient vs Scoped

```csharp
using Microsoft.Extensions.DependencyInjection;
using System;

namespace ConsoleAppDI
{
    public interface ITransientOperation 
    {
        Guid OperationId { get; }
    }

    public interface IScopedOperation
    {
        Guid OperationId { get; }
    }

    public class Operation : ITransientOperation, IScopedOperation
    {
        public Guid OperationId { get; } = Guid.NewGuid();
    }

    public class OperationService
    {
        private readonly ITransientOperation _transientOperation;
        private readonly IScopedOperation _scopedOperation;

        public OperationService(ITransientOperation transientOperation, IScopedOperation scopedOperation)
        {
            _transientOperation = transientOperation;
            _scopedOperation = scopedOperation;
        }

        public void DisplayOperationIds()
        {
            Console.WriteLine($"Transient Operation ID: {_transientOperation.OperationId}");
            Console.WriteLine($"Scoped Operation ID: {_scopedOperation.OperationId}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // Configure services
            var serviceCollection = new ServiceCollection();
            ConfigureServices(serviceCollection);

            // Build service provider
            var serviceProvider = serviceCollection.BuildServiceProvider();

            // Simulate multiple scopes
            Console.WriteLine("Scope 1:");
            using (var scope1 = serviceProvider.CreateScope())
            {
                var scopedProvider = scope1.ServiceProvider;
                var service1 = scopedProvider.GetRequiredService<OperationService>();
                var service2 = scopedProvider.GetRequiredService<OperationService>();

                service1.DisplayOperationIds();
                service2.DisplayOperationIds(); // Scoped ID should be same as service1's Scoped ID
            }

            Console.WriteLine("Scope 2:");
            using (var scope2 = serviceProvider.CreateScope())
            {
                var scopedProvider = scope2.ServiceProvider;
                var service3 = scopedProvider.GetRequiredService<OperationService>();

                service3.DisplayOperationIds(); // New Scoped ID
            }
        }

        private static void ConfigureServices(IServiceCollection services)
        {
           // Register services
            services.AddTransient<OperationService>();
            services.AddTransient<ITransientOperation, Operation>(); // For Transient
            services.AddScoped<IScopedOperation, Operation>();    // For Scoped
        }
    }
}
```

## Singleton Pattern

```csharp
using System;
using System.IO;

public sealed class Logger
{
    private static readonly Lazy<Logger> _instance = 
        new Lazy<Logger>(() => new Logger());

    private readonly string _logFilePath;

    private Logger()
    {
        // Specify the log file path
        _logFilePath = "log.txt";

        // Initialize the log file
        if (!File.Exists(_logFilePath))
        {
            using (var stream = File.Create(_logFilePath))
            {
            }
        }
    }

    public static Logger Instance => _instance.Value;

    public void Log(string message)
    {
        // Append log message to the log file
        using (var writer = File.AppendText(_logFilePath))
        {
            writer.WriteLine($"{DateTime.Now}: {message}");
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Log some messages using the singleton logger
        Logger log = Logger.Instance;
        log.Log("Application started.");
        log.Log("Performing some operations...");
        log.Log("Application ended.");
        
        Console.WriteLine("Logs have been written to the log file.");
    }
}
```

## Factory Pattern

```csharp
using System;

namespace FactoryPatternDemo
{
    // Product Interface
    public interface ICreditCard
    {
        string GetCardType();
        int GetCreditLimit();
        int GetAnnualCharge();
    }

    // Concrete Products
    public class StandardCard : ICreditCard
    {
        public string GetCardType() => "Standard Card";

        public int GetCreditLimit() => 5000;

        public int GetAnnualCharge() => 100;
    }

    public class GoldCard : ICreditCard
    {
        public string GetCardType() => "Gold Card";

        public int GetCreditLimit() => 10000;

        public int GetAnnualCharge() => 300;
    }

    public class PlatinumCard : ICreditCard
    {
        public string GetCardType() => "Platinum Card";

        public int GetCreditLimit() => 20000;

        public int GetAnnualCharge() => 500;
    }

    // Factory
    public class CreditCardFactory
    {
        public ICreditCard GetCreditCard(string cardType)
        {
            return cardType.ToLower() switch
            {
                "standard" => new StandardCard(),
                "gold" => new GoldCard(),
                "platinum" => new PlatinumCard(),
                _ => throw new ArgumentException("Invalid card type")
            };
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            var factory = new CreditCardFactory();

            ICreditCard standardCard = factory.GetCreditCard("standard");
            Console.WriteLine($"Card Type: {standardCard.GetCardType()}, " +
                              $"Limit: {standardCard.GetCreditLimit()}, " +
                              $"Annual Charge: {standardCard.GetAnnualCharge()}");

            ICreditCard goldCard = factory.GetCreditCard("gold");
            Console.WriteLine($"Card Type: {goldCard.GetCardType()}, " +
                              $"Limit: {goldCard.GetCreditLimit()}, " +
                              $"Annual Charge: {goldCard.GetAnnualCharge()}");

            ICreditCard platinumCard = factory.GetCreditCard("platinum");
            Console.WriteLine($"Card Type: {platinumCard.GetCardType()}, " +
                              $"Limit: {platinumCard.GetCreditLimit()}, " +
                              $"Annual Charge: {platinumCard.GetAnnualCharge()}");
        }
    }
}
```

## Observer

```csharp
using System;
using System.Collections.Generic;

// The subject interface
public interface IStock
{
    void AddWatcher(IStockWatcher watcher);
    void RemoveWatcher(IStockWatcher watcher);
    void NotifyWatchers();
}

// Concrete subject
public class Stock : IStock
{
    private readonly List<IStockWatcher> _watchers;
    private string _tickerSymbol;
    private decimal _price;

    public Stock(string tickerSymbol, decimal initialPrice)
    {
        _tickerSymbol = tickerSymbol;
        _price = initialPrice;
        _watchers = new List<IStockWatcher>();
    }

    public void UpdatePrice(decimal newPrice)
    {
        _price = newPrice;
        NotifyWatchers();
    }

    public void AddWatcher(IStockWatcher watcher)
    {
        _watchers.Add(watcher);
    }

    public void RemoveWatcher(IStockWatcher watcher)
    {
        _watchers.Remove(watcher);
    }

    public void NotifyWatchers()
    {
        foreach (var watcher in _watchers)
        {
            watcher.Update(_tickerSymbol, _price);
        }
    }
}

// Observer interface
public interface IStockWatcher
{
    void Update(string tickerSymbol, decimal newPrice);
}

// Concrete observer
public class StockInvestor : IStockWatcher
{
    private readonly string _name;

    public StockInvestor(string name)
    {
        _name = name;
    }

    public void Update(string tickerSymbol, decimal newPrice)
    {
        Console.WriteLine($"{_name} notified: {tickerSymbol} price has changed to {newPrice:C}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create a stock (subject)
        var appleStock = new Stock("AAPL", 150.00m);

        // Create stock watchers (observers)
        var investor1 = new StockInvestor("John Doe");
        var investor2 = new StockInvestor("Jane Smith");

        // Subscribe to the stock updates
        appleStock.AddWatcher(investor1);
        appleStock.AddWatcher(investor2);

        // Update stock price
        appleStock.UpdatePrice(155.00m);

        // One investor decides not to follow the stock anymore
        appleStock.RemoveWatcher(investor1);

        // Update stock price again
        appleStock.UpdatePrice(160.00m);
    }
}
```

## Oberserver mit delegate und events

```csharp
using System;

// Der Vertreter
public delegate void StockPriceChangedHandler(string tickerSymbol, decimal newPrice);

// Das Subjekt
public class Stock
{
    public event StockPriceChangedHandler StockPriceChanged;

    private readonly string _tickerSymbol;
    private decimal _price;

    public Stock(string tickerSymbol, decimal initialPrice)
    {
        _tickerSymbol = tickerSymbol;
        _price = initialPrice;
    }

    public void UpdatePrice(decimal newPrice)
    {
        if (_price != newPrice)
        {
            _price = newPrice;
            OnStockPriceChanged();
        }
    }

    protected virtual void OnStockPriceChanged()
    {
        StockPriceChanged?.Invoke(_tickerSymbol, _price);
    }
}

// Das Observer
public class StockInvestor
{
    private readonly string _name;

    public StockInvestor(string name)
    {
        _name = name;
    }

    public void StockPriceNotification(string tickerSymbol, decimal newPrice)
    {
        Console.WriteLine($"{_name} notified: {tickerSymbol} price has changed to {newPrice:C}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Create a stock (subject)
        var appleStock = new Stock("AAPL", 150.00m);

        // Create stock watchers (observers)
        var investor1 = new StockInvestor("John Doe");
        var investor2 = new StockInvestor("Jane Smith");

        // Subscribe to the stock events
        appleStock.StockPriceChanged += investor1.StockPriceNotification;
        appleStock.StockPriceChanged += investor2.StockPriceNotification;

        // Update stock price
        appleStock.UpdatePrice(155.00m);

        // One investor decides not to follow the stock anymore
        appleStock.StockPriceChanged -= investor1.StockPriceNotification;

        // Update stock price again
        appleStock.UpdatePrice(160.00m);
    }
}
```

## Strategy Pattern

```csharp
using System;

// Strategy interface
public interface IPaymentStrategy
{
    void Pay(decimal amount);
}

// Concrete strategies
public class CreditCardPayment : IPaymentStrategy
{
    private readonly string _cardNumber;

    public CreditCardPayment(string cardNumber)
    {
        _cardNumber = cardNumber;
    }

    public void Pay(decimal amount)
    {
        Console.WriteLine($"Paid {amount:C} using Credit Card with card number {_cardNumber}.");
    }
}

public class PayPalPayment : IPaymentStrategy
{
    private readonly string _email;

    public PayPalPayment(string email)
    {
        _email = email;
    }

    public void Pay(decimal amount)
    {
        Console.WriteLine($"Paid {amount:C} using PayPal with email {_email}.");
    }
}

// Context class
public class ShoppingCart
{
    private IPaymentStrategy _paymentStrategy;

    public void SetPaymentStrategy(IPaymentStrategy paymentStrategy)
    {
        _paymentStrategy = paymentStrategy;
    }

    public void Checkout(decimal amount)
    {
        if (_paymentStrategy == null)
        {
            throw new InvalidOperationException("Payment strategy not set.");
        }
        
        _paymentStrategy.Pay(amount);
    }
}

class Program
{
    static void Main(string[] args)
    {
        var cart = new ShoppingCart();

        // Client chooses a payment strategy at runtime
        cart.SetPaymentStrategy(new CreditCardPayment("1234-5678-9876"));
        cart.Checkout(120.00m);

        cart.SetPaymentStrategy(new PayPalPayment("user@example.com"));
        cart.Checkout(75.50m);
    }
}
```
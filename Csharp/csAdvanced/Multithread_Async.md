# Mulithreading
Include `using System.Threading;` at the top of the file.

Essentially there's 2 ways to create a multi-threaded process.
1. First is by the example shown below
2. Second is to do the exact same but use the `Task` class

Note however that when you're using Tasks, mixing thread-objects within task-objects like: `Thread.Sleep(500);` could cause several issues.


```cs
class Source
{
    public static void Main()
    {
        Thread mainThread = Thread.CurrentThread;
        mainThread.Name = "___MAIN__THREAD__";
        //Console.WriteLine(mainThread.Name);
        Thread thread1 = new Thread(CountDown);
        Thread thread2 = new Thread(CountUp);
        Console.WriteLine(mainThread.Name + " is complete!");
    }
    public static void CountDown()
    {
        for (int i = 10; i >= 0; i--)
        {
            Console.WriteLine("Timer #1 : " + i + " seconds");
        }
        Console.WriteLine("Timer #1 is complete!");
    }
    public static void CountUp()
    {
        for (int i = 0; i <= 10; i++)
        {
            Console.WriteLine("Timer #2 : " + i + " seconds");
        }
        Console.WriteLine("Timer #2 is complete!");
    }
}
```

# Async
Here we have an example of a console app making "tea".

## Sync programming
1. Started the kettle.
2. Waiting for the kettle.
3. The kettle finished boiling.
4. Taking the cups out.
5. Putting teabags into the cups.
6. Pouring hot water in the cups.

```cs
    class Source
    {
        public static void Main()
        {
            MakeTea();
        }

        public static void MakeTea()
        {
            string water = BoilWater();

            Console.WriteLine("Taking the cups out.");
            Console.WriteLine("Putting teabags into the cups.");

            Console.WriteLine($"Pouring {water} in cups.");
        }

        public static string BoilWater()
        {
            Console.WriteLine("Started the kettle.");
            Console.WriteLine("Waiting for the kettle.");
            Task.Delay(2000).GetAwaiter().GetResult();
            Console.WriteLine("The kettle finished boiling.");

            return "hot water";
        }
    }
```

## Async programming
1. Started the kettle.
2. Waiting for the kettle.
3. Taking the cups out.
4. Putting teabags into the cups.
5. The kettle finished boiling.
6. Pouring hot water in the cups.

```cs
class Source
{
    public static async Task Main()
    {
        await MakeTeaAsync();
    }

    public static async Task MakeTeaAsync()
    {
        Task<string> boilingWater = BoilWaterAsync(); // This is now a task

        Console.WriteLine("Taking the cups out.");
        Console.WriteLine("Putting teabags into the cups.");

        string water = await boilingWater; // Thread awaits the boilingWater task to be done to get the return value.

        Console.WriteLine($"Pouring {water} in cups.");
    }

    public static async Task<string> BoilWaterAsync()
    {
        Console.WriteLine("Started the kettle.");
        Console.WriteLine("Waiting for the kettle.");
        await Task.Delay(2000); // Thread waits till this is done in order to resume
        Console.WriteLine("The kettle finished boiling.");

        return "hot water";
    }
}
```

https://www.javatpoint.com/c-sharp-multithreading

https://www.javatpoint.com/c-sharp-thread-synchronization

https://www.tutorialspoint.com/csharp/csharp_multithreading.htm

https://www.geeksforgeeks.org/c-sharp-multithreading/

https://www.youtube.com/watch?v=il9gl8MH17s
# 🐈 requests > *;

```cs
using System;
using System.Collections.Generic;
using System.Threading;

namespace practice
{
    internal class Program
    {
        static void Main(string[] args)
        {
            var threads = new List<Thread>();

            for(int i =0; i < 12000; i++)
            {
                threads.Add(new Thread(() =>
                {
                    Console.WriteLine($"Lunarian is better {Thread.CurrentThread.ManagedThreadId} times!");
                }));
            }
            
            threads.ForEach(t => t.Start());
            threads.ForEach(t => t.Join());
        }
    }
}
```

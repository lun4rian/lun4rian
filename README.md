# 🐈 requests > *;

```cs
using System;
using System.Net;
using System.Net.Http;

namespace TestAndPractice
{
    internal class Program
    {
        static void Main(string[] args)
        {
            /// <summary>
            /// .NET MeatRider
            /// </summary>

            ServicePointManager.DefaultConnectionLimit = 1000;
            ServicePointManager.Expect100Continue = false;
            
            using(var client = new HttpClient())
            {
                client.DefaultRequestHeaders.Add("Authorization", "no token for u");
                var response = client.PostAsync("https://discord.com/api/v9/invites/love", null).Result;
                Console.WriteLine(response.Content.Headers);
                client.Dispose();

                /// Don't even bother using this, it doesn't work.
            }
        }
    }
}
```
